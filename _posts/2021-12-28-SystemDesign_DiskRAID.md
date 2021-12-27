---
title: "System Design - Disk RAID"
categories:
  - System Design
tags:
  - System Design
---



### Disk RAID
> RAID : Redundant Array of Independent Disks  


- RAID 
    - 여러개의 디스크를 하나의 디스크처럼 사용함
    - 비용절감 + 신뢰성 향상 + 성능향상

- 하드웨어 RAID
    - 하드웨어 제조업체에서 여러개의 하드디스크를 가지고 장비를 만들어서 그 자체를 공급
    - 좀 더 안정적이지만 고가임

- **소프트웨어 RAID** 
    - 고가의 하드웨어 RAID의 대안
    - 운영체제에서 지원하는 방식
    - 저렴한 비용으로 좀 더 안전한 데이터의 저장이 가능


### RAID 종류
> raid 종류


- hdd 추가 : 단순 볼륨, hdd 1개 추가
- Linear raid : 최소 2개 hdd, 2개 붙여 1개로 사용, 순차적 자료 저장, 100% 공간 활용
- raid 0 : 최소 2개, 모든 디스크에 동시 저장, 100% 공간 활용
    - RAID 0 : 최소 2개의 하드디스크가 필요하며, 모든 디스크에 동시에 저장된다. 100%의 공간 효율성을 가지며 빠른 성능을 가지고 있다. 그러나 하나의 디스크가 고장나면 모든 정보를 사용 할 수 없게 되므로 신뢰성이 낮다.

- raid 1 : mirroring - 공간 1/2, 공간 효율 낮음, 중요한 데이터 저장, 신뢰성 높다.
    - RAID 1 : 미러링 방식이라고도 부르며 동일한 데이터를 2개 이상의 하드디스크에 동일하게 저장한다. 즉, 공간효율은 1/2로 줄게된다. 공간효율이 줄어든 대신 동일한 데이터가 다른 하드디스크에도 저장되어 있으니 한 장비에 결함이 있어도 문제없이 사용이 가능한 정점을 가지고 있다.  저장속도는 서로 다른 디스크에 같은 정보를 입력하는 것이기 때문에 차이가 없다.


- raid 5 : hdd 3개 이상, hdd2개는 data, 1개는 parity 값 저장, data 안정성이 좋음, 공간 효율이 좋음
    - RAID 5 : RAID 0의 공간 효율성(100%)와 RAID 1 의 데이터 안정성을 조합하여 사용하는 방식으로 Parity를 사용하여 결함이 있는 데이터를 복구할 수 있다. 하지만 디스크가 2개 이상 고장나면 패리티로도 복구가 불가능하다.
    - parity 비트 사용한다는게 예를들어, disk 1, disk2, disk3 이 있을때 disk1 데이터가 `0` 이고 disk2 데이터가 `1` 하면 disk3은 0과 1의 XOR 연산으로 Parity 비트를 갖게되고 `1` 값을 저장
        - 참고로, XOR 연산은 (같으면 0 다르면 1)

- raid 6 : raid5의 개선, hdd 4개 이상, parity 2개, 중복 parity 정보 사용
    - RAID 6 : RAID 5 방식을 좀더 개선한 것으로 공간 효율은 RAID 5 보다 떨어지지만 디스크 2개가 동시에 고장나도 데이터에는 이상이 없도록 만든 방식이다.

<!--
### Disk RAID
> RAID : Redundant Array of Independent Disks


- RAID
    - Multiple disks are used as one disk
    - Cost reduction + reliability improvement + performance improvement

- Hardware RAID
    - Hardware manufacturer makes equipment with several hard disks and supplies itself
    - A bit more stable but expensive

- **Software RAID**
    - Alternative to expensive hardware RAID
    - The method supported by the operating system
    - More secure data storage at low cost


### RAID type
> RAID type


- **Add hdd** : Add simple volume, 1 hdd
- **Linear raid**: At least 2 HDDs, 2 HDDs attached to use as 1, sequential data storage, 100% space utilization
- **raid 0**: at least 2, simultaneous storage on all disks, 100% space utilization
    - RAID 0: A minimum of two hard disks are required, and all disks are simultaneously saved. It has 100% space efficiency and has fast performance. However, if one disk fails, all information becomes unavailable, so reliability is low.

- **raid 1** : mirroring - 1/2 space, low space efficiency, important data storage, high reliability.
    - RAID 1 : Also called mirroring method, the same data is stored equally on two or more hard disks. That is, the space efficiency is reduced by 1/2. Instead of reducing space efficiency, the same data is stored on other hard disks, so even if one device has a defect, it can be used without any problem. There is no difference in storage speed because the same information is input to different disks.


- **raid 5** : 3 or more hdd, 2 HDDs for data, 1 for storing parity values, good data stability, good space efficiency
    - RAID 5: By using a combination of the space efficiency of RAID 0 (100%) and the data stability of RAID 1, you can use Parity to recover defective data. However, if two or more disks fail, recovery is impossible even with parity.
    - Using the parity bit means that, for example, when there are disk 1, disk2, and disk3, if disk1 data is ‘0’ and disk2 data is ‘1’, disk3 has a parity bit by XORing 0 and 1 and returns a value of ‘1’. save
        - For reference, the XOR operation is (0 if equal, 1 if different)

- **raid 6** : improvement of raid5, 4 or more hdd, 2 parity, use of redundant parity information
    - RAID 6 : This is a further improvement of the RAID 5 method, and although the space efficiency is lower than that of RAID 5, the data is not damaged even if two disks fail at the same time.


-->