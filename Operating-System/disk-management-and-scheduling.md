# Chap12. Disk Management and Scheduling

## Disk Structure

- **Logical block**
  - 디스크의 외부에서 보는 디스크의 단위 정보 저장 공간들
  - 주소를 가진 1차원 배열처럼 취금
  - 정보를 전송하는 최소단위
- **Sector**
  - 디스크 내부에서 디스크를 관리하는 최소단위
  - logical block이 물리적인 디스크에 매핑된 위치
  - Sector 0은 최외곽 실린더의 첫 트랙에 있는 첫 번째 섹터이다. 



## Disk Scheduling

- Access time의 구성
  - Seek time
    - 헤드를 해당 실린더로 움직이는데 걸리는 시간
  - Roational latency
    - 헤드가 원하는 섹터에 도달하기까지 걸리는 회전지연시간
  - Transfer time
    - 실제 데이터의 전송시간
- Disk bandwidth
  - 단위시간 당 전송된 바이트의 수
- Disk Scheduling
  - Seek time을 최소화하는 것이 목표
  - Seek time ≈ seek distance



## Disk Management

- **physical formatting(low-level formatting)**
  - 디스크를 컨트롤러가 읽고 쓸 수 있도록 섹터들로 나누는 과정
  - 각 섹터는 **header** + **실제 data** + **trailer**로 구성
  - header와 trailer는 sector number, ECC(Error- Correcting Code) 등의 정보가 저장되며 controller가 직접 접근 및 운영
- **Partitioning**
  - 디스크를 하나 이상의 실린더 그룹으로 나누는 과정
  - OS는 이것을 독립적 disk로 취급 ( logical disk)
- **Logical formatting**
  - 파일시스템을 만드는 것
  - FAT, inode, free space 등의 구조 포함
- **Booting**
  - ROM에 있는 "smalll bootstrap loader"의 실행
  - Sector 0을 load하여 실행
  - Sector 0은 "full Bootstrap loader program"
  - OS를 디스크에서 load하여 실행



## Disk Scheduling Algorithms

- 큐에서 다음과 같은 실린더 위치의 요청이 존재하는 경우 디스크 헤드 53번에서 시작한 각 알고리즘의 수행 결과는? (실린더 위치는 0-199)

  98, 183, 37,122,14,124,65,67

### FCFS

들어온 순으로 처리하는 알고리즘

![스크린샷 2021-05-14 오전 11.41.35](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-14 오전 11.41.35.png)

### SSTF(Shortest Seek Time First)

- 큐에 있는 것 중 현재 head의 요청과 가장 가까운 순으로 처리

- Starvation문제

![스크린샷 2021-05-14 오전 11.42.45](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-14 오전 11.42.45.png)

### SCAN

- Disk arm이 디스크의 한쪽 끝에서 다른쪽 끝으로 이동하며 가는 길목에 있는 모든 요청을 처리한다.
- 다른 한쪽 끝에 도달하면 역방향으로 이동하며 오는 길목에 있는 모든 요청을 처리하며 다시 반대쪽 끝으로 이동한다
- 문제점: 실린더 위치에 따라 대기시간이 다르다.

### C-SCAN(Circular-SCAN)

- 헤드가 한쪽 끝에서 다른 쪽 끝으로 이동하며 가는 길목에 있는 모든 요청을 처리
- 다른 쪽 끝에 도달했으면 요청을 처리하지 않고 곧바로 출발점으로 다시 이동
- SCAN보다 균일한 대기시간을 제공한다.

### N-SCAN

- SCAN의 변형 알고리즘
- 일단 arm이 한 방향으로 움직이기 시작하면 그 시점 이후에 도착한  job은 되돌아올때 service

### LOOK and C-LOOK

- SCAN이나 C-SCAN은 헤드가 디스크 끝에서 끝으로 이동
- LOOK과 C-LOOK은 헤드가 진행 중이다가 **그 방향에 더 이상 기다리는 요청이 없으면** 헤드의 이동방향을 즉시 그 반대로 이동한다.

![스크린샷 2021-05-14 오전 11.54.17](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-14 오전 11.54.17.png)



## Disk-Scheduling Algorithm의 결정

- SCAN, C-SCAN 및 그 응용 알고리즘은 LOOK, C-LOOK 등이 일반적으로 디스크 입출력이 많은 시스템에서 효율적인 것으로 알려져있음
- File의 할당 방법에 따라 디스크 요청이 영향을 받음
- 디스크 스케줄링 알고리즘은 필요할 경우 다른 알고리즘으로 쉽게 교체할 수 있도록 OS와 별도의 모듈로 작성되는 것이 바람직하다. 



## Swap-Space Management

- Disk를 사용하는 두 가지 이유
  - memory의 volatile(휘발성)한 특성 -> file system
  - 프로그램 실행을 위한 메모리공간부족 -> swap space(swap area)
- Swap-space
  - Virtual memory system에서는 디스크를 memory의 연장공간으로 사용
  - 파일시스템 내부에 둘 수도 있으나 별도 partition 사용이 일반적
    - 공간 효율보다는 속도 효율성이 우선
    - 일반 파일보다 훨씬 짧은 시간만 존재하고 자주 참조됨
    - 따라서 block의 크기 및 저장방식이 일반 파일시스템과 다름

![스크린샷 2021-05-14 오후 12.05.23](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-14 오후 12.05.23.png)





## RAID

- RAID(Redundant Array of Independent Disks)
  - 여러 개의 디스크를 묶어서 사용
- RAID의 사용 목적
  - 디스크 처리 속도 향상
    - 여러 디스크에 block의 내용을 분산저장
    - 병렬적으로 읽어옴(interleaving, striping)
  - 신뢰성(reliability) 향상
    - 동일 정보를 여러 디스크에 중복저장
    - 하나의 디스크가 고장 시 다른 디스크에서 읽어옴(Mirroring, shadowing)
    - 단순한 중복 저장이 아니라 일부 디스크에 parity를 저장하여 공간의 효율성을 높일 수 있다.