---
title: "Code update and Using Lambda function with find_if()"
categories:
  - C++
tags:
  - C++
---

## Code Comment(09/03/2021)

- remove redundant signal routing

```c++
void AA::handleMessage(Message* internalMessage)
{
  switch(Message->getMessageType())
  {
    case MessageType::INTERNAL_MESSAGE_A:
    {
      auto InternalMessageA = static_cast<const messages2::InternalMessageA*>(Message);
      for(const auto& item : InternalMessageA->m_items)
      {
        const U32 id = item.itemId;
        LocalbbInstanceBaseImpl* localBBInstance = m_localDispatcherApi->getBB(id);
        if (localBBInstance)
        {
          std::vector<AInfoS> infoList;
          for(U16 i = 0; i < item.noOfAInfos; i++)
          {
            AInfoS aInfo;
            aInfo.m_aId = item.aInfos[i].aId;
            aInfo.m_aPwr = item.aInfos[i].power;
            infoList.emplace_back(aInfo);
          }
          localBBInstance->handleAData(infoList);
        }
        else
        {
          TRACE_ABNORMAL("localBBInstance is not exist");
        }
      }
      break;
    }
    default:
      ;
  }
}

```

> **Comment**

- It seems that received internal message has all data needed by BB class. Why not simply pass internal message to localBBInstance via localBBInstance->handleMessage and then extract all needed data there. In my opinion handleAData is redundant

- all localBBInstances will use the same memory allocated for single message
    - pseudo code

    ```c++
    for(localBBInstance in message->items)
    {​​​​​
        fetch item localBBInstance object using localBBInstanceId
        pass message to given localBBInstance
    }​​​​​
    ```

​- in this case all bbInstance will receive exactly the same message, an then it can extract info which is related to given bbInstance
- with **find** of **find_if** function.

## Lamda function
- 람다는 람다 함수 또는 이름없는 함수라고 부르며 함수 object
- 람다를 정의한 곳의 외부 변수를 람다 내부에서 사용하고 싶을때는 캡쳐
- 외부 변수를 참조 또는 복사로 캡쳐할 수 있음
- 클래스에서도 람다를 사용할 수 있음


- [find_if](https://en.cppreference.com/w/cpp/algorithm/find)
- [람다](https://skstormdummy.tistory.com/entry/%EB%9E%8C%EB%8B%A4lamda)

> **캡쳐기능**

- 람다 함수 외의 변수를 람다 함수에 가져와 사용하는 것을 **캡쳐** 라고 함

```c++
int main()
{
  int n1, n2, n3, n4, n5;
  [&, n1, n2]{} // n3, n4, n5는 참고, n1, n2는 복사
  [=, &n1, &n2]{} // n3, n4, n5는 복사, n1, n2는 참조

  //[&, &n1]{} // ERROR --> n1을 이미 default 참조로 사용
  //[=, n1]{} // ERROR --> n1을 이미 default 복사로 사용
}
```

- 클래스에서의 람다 사용
  - 클래스 멤버 내의 람다 식은 해당 클래스에서 friend로 인식하므로 람다식에서 private멤버의 접근도 가능
  - **this** 를 캡쳐

```c++
[this]{} // this capture--> allow access to member data of the class/Instance
```

- find_if와 람다함수
  - find_if함수는 세개의 인자를 가지고 있음
  - 세번 째 인자인 Functor (또는 람다) 의 반환 값이 true 인 경우 검색을 중단


## Code update


```c++
void AA::handleMessage(Message* internalMessage)
{
  switch(Message->getMessageType())
  {
    case MessageType::INTERNAL_MESSAGE_A:
    {
      auto InternalMessageA = static_cast<const messages2::InternalMessageA*>(Message);
      for(const auto& item : InternalMessageA->m_items)
      {
        const U32 id = item.itemId;
        LocalbbInstanceBaseImpl* localBBInstance = m_localDispatcherApi->getBB(id);
        if (localBBInstance)
        {
          std::vector<AInfoS> infoList;
          for(U16 i = 0; i < item.noOfAInfos; i++)
          {
            AInfoS aInfo;
            aInfo.m_aId = item.aInfos[i].aId;
            aInfo.m_aPwr = item.aInfos[i].power;
            infoList.emplace_back(aInfo);
          }
          localBBInstance->handleMessage(Message);
        }
        else
        {
          TRACE_ABNORMAL("localBBInstance is not exist");
        }
      }
      break;
    }
    default:
      ;
  }
}

```


```c++
void LocalbbInstanceBaseImpl::handleMessage(const Message* message)
{
  case MessageType::_PIM_MITIGATION_MEAS_DATA_IND:
  {
    if(m_bbInstanceData->m_localbbInstanceState == LocalbbInstanceStateE::ACTIVATED)
    {
      m_bbInstanceData->m_measuredAInfo.clear();

      auto InternalMessageA = static_cast<const messages2::InternalMessageA*>(message);
      auto aInfo = std::find_if(InternalMessageA->m_items.begin(),
                                InternalMessageA->m_items.end(),
                                [this](ItemS item){
        return item.itemId == this->m_bbInstanceData->m_bbInstanceId;
      });
      for(U16 i = 0; i < aInfo->noOfAInfos; i++)
      {
        m_bbInstanceData->m_measuredAInfo.emplace_back(AInfoS{aInfo->aInfos[i].aId,
                                                              aInfo->aInfos[i].power});
      }
    }
    break;
  }
}
```


<!--

```c++
void CellEqRH::handlePimciMessage(lrh::messages::PimciMessage* pimciMessage)
{
  switch(pimciMessage->getMessageType())
  {
    case lrh::MessageType::PIMCI_PIM_MITIGATION_MEAS_DATA_IND:
    {
      auto pimciPimMitigationMeasDataInd = static_cast<const lrh::messages2::PimciPimMitigationMeasDataInd*>(pimciMessage);
      for(const auto& victimCell : pimciPimMitigationMeasDataInd->m_victims)
      {
        const CellIdT cellId = victimCell.victimCellId;
        LocalCell* localCell = m_localCellDispatcherApi->getLocalCell(cellId);
        if (localCell)
        {
          std::vector<PimMitigAggressorsInfoS> pimMitigAggressorsInfoList;
          for(U16 i = 0; i < victimCell.noOfAggressors; i++)
          {
            PimMitigAggressorsInfoS AggressorInfo;
            AggressorInfo.m_aggressorCellId = victimCell.aggressors[i].aggressorCellId;
            AggressorInfo.m_pim = victimCell.aggressors[i].pim;
            pimMitigAggressorsInfoList.emplace_back(AggressorInfo);
          }
          localCell->handlePimMitigationMeasData(pimMitigAggressorsInfoList);
        }
        else
        {
          TRACE_ABNORMAL(Ft_CELL_CONFIG, STR("CellId=%d, cell not found", cellId));
        }
      }
      break;
    }
    default:
      ;
  }
}

```

```c++
void CellEqRH::handlePimciMessage(lrh::messages::PimciMessage* pimciMessage)
{
  switch(pimciMessage->getMessageType())
  {
    case lrh::MessageType::PIMCI_PIM_MITIGATION_MEAS_DATA_IND:
    {
      auto pimciPimMitigationMeasDataInd = static_cast<const lrh::messages2::PimciPimMitigationMeasDataInd*>(pimciMessage);
      for(const auto& victimCell : pimciPimMitigationMeasDataInd->m_victims)
      {
        const CellIdT cellId = victimCell.victimCellId;
        LocalCell* localCell = m_localCellDispatcherApi->getLocalCell(cellId);
        if (localCell)
        {
          localCell->handleMessage(pimciMessage);
        }
        else
        {
          TRACE_ABNORMAL(Ft_CELL_CONFIG, STR("CellId=%d, cell not found", cellId));
        }
      }
      break;
    }
    default:
      ;
  }
}
```

```c++
void LocalCellBaseImpl::handleMessage(const lrh::Message* message)
{
  case lrh::MessageType::PIMCI_PIM_MITIGATION_MEAS_DATA_IND:
  {
    if(m_cellData->m_localCellState == LocalCellStateE::ACTIVATED)
    {
      m_cellData->m_measuredPimMitigAggressorsInfo.clear();

      auto pimciPimMitigationMeasDataInd = static_cast<const lrh::messages2::PimciPimMitigationMeasDataInd*>(message);
      auto aggressorInfo = std::find_if(pimciPimMitigationMeasDataInd->m_victims.begin(),
                                        pimciPimMitigationMeasDataInd->m_victims.end(),
                                        [this](PimVictimAggressorsS victim){
        return victim.victimCellId == this->m_cellData->m_cellId;
      });
      for(U16 i = 0; i < aggressorInfo->noOfAggressors; i++)
      {
        m_cellData->m_measuredPimMitigAggressorsInfo.emplace_back(PimMitigAggressorsInfoS
                                                                  {aggressorInfo->aggressors[i].aggressorCellId,
                                                                   aggressorInfo->aggressors[i].pim});
      }

      FeatureTaskMsgD reqMsg(FEAT_TASK_PIM_MITIG_MEAS_DATA_IND);
      FeatureHandlerBase* pimMitigAutoConfigTaskHandler = getFeatureHandler(FEAT_TYPE_PIM_MITIG_AUTO_CONFIG);
      pimMitigAutoConfigTaskHandler->executeTask(&reqMsg);
    }
    break;
  }

  default:
    TRACE_ERROR(STR("CellId=%d: handleMessage(): invalid message received.", m_cellData->m_cellId));
    break;
  }
}
```

-->
