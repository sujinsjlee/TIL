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
