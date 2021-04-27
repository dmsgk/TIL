# Chap 8. Memory Management

## Logical vs Physical Address

- Logical address(= virtual address)
  - 프로세스마다 독립적으로 가지는 주소 공간
  - 각 프로세스마다 0번지부터 시작
  - **cpu가 보는 주소는 logical address임**
- Physical address
  - 메모리에 실제 올라가는 위치

- 주소 바인딩 : 주소를 결정하는 것

  **Symbolic Address -> Logical Address -> Physical Address**

  (프로그래머는 숫자가 아닌 심볼로 된 주소를 사용하게 되고, 컴파일이 되면 논리적 주소로, 실행이 되려면 물리적 주소로 변환이 되어야 한다. )

  - 주소는 언제 결정되는가? 각 프로그램이 가지고 있는 논리적 주소가 물리적 메모리 주소로 언제 결졍되는가. 이를 결정하는 방식 3가지를 살펴본다. 

## 주소 바인딩(Address Binding)

- **Compile time binding**
  - 물리적 메모리 주소가 **컴파일 시** 알려짐
    - 따라서 논리적 주소가 곧 물리적 주소가 된다. 
    - 물리적 주소가 미리 결정되어야 하므로 매우 비효율적이므로 지금의 컴퓨터 시스템에서는 잘 사용하지 않는다. 
  - 시작 위치 변경시 재컴파일
  - 컴파일러는 절대코드(**absolute code**)생성!
- **Load time binding**
  - **실행시작**될 때 주소변환
  - loader의 책임하에 물리적 메모리 주소 부여
  - 컴파일러가 재배치가능코드(relocatable code)를 생성한 경우 가능
- **Execution time binding(= Run time binding)**
  - 수행이 시작된 이후에도 프로세스의 메모리 상 위치를 옮길 수 있음
  - cpu가 주소를 참조할 때마다 binding을 점검(address mapping table)
    - 위 두 방식과 다르게 프로그램이 실행 중일 때에도 주소가 계속 바뀌므로.
  - 하드웨어적인 지원이 필요(e.g. base and limit registers, **MMU**)

<img width="510" alt="스크린샷 2021-04-27 오후 5 06 09" src="https://user-images.githubusercontent.com/72622744/116235287-a0d34500-a798-11eb-91ac-ecd39bf51320.png">



## Memory-Management Unit(MMU)

- MMU(Memory-Management Unit)

  -  logical address를 physical address로 매핑해주는(= 주소변환을 해 주는) **Hardware Device**

- MMU scheme

  - 사용자 프로세스가 cpu에서 수행되며 생성해내는 모든 주소값에 대해 base register( = relocation register)의 값을 더한다.

- User program

  - **local address만을 다룬다.**

  - 실제 physical address를 볼 수 없으며 알 필요가 없다.

    

<img width="512" alt="스크린샷 2021-04-27 오후 5 26 47" src="https://user-images.githubusercontent.com/72622744/116235396-c5c7b800-a798-11eb-9c57-4481e9502256.png">

- 가장 간단한 MMU는 base register와 limit register를 이용한 방법
  - base register(=relocation register)에는 프로그램의 시작위치를 저장해둔다.(14000) 주소변환을 할 때는 논리적 주소에 시작위치를 더해서 물리적 주소로 변환한다. 
  - limit register는 프로그램의 크기를 담고 있음. 프로그램 크기보다 더 큰 논리주소를 요청하여 다른 프로세스의 메모리를 보려는 악의적인 프로그램인지 확인하는 용도로 사용한다. 벗어나는 요청이면 trap이 걸려 cpu제어권이 운영체제에게 넘어감. 프로그램 크기 이내의 요청이라면 주소변환이 이루어진다. 

<img width="512" alt="스크린샷 2021-04-27 오후 5 33 15" src="https://user-images.githubusercontent.com/72622744/116235534-f3146600-a798-11eb-8da5-237f5dd6e4f0.png">


## Some Terminologies

### Dynamic Loading

** loading : 메모리로 올리는 것

- 프로세스 전체를 메모리에 미리 다 올리는 것이 아니라 해당 루틴이 불려질 때 메모리에 load하는 것
- memory utilization의 향상
- 가끔씩 사용되는 많은 양의 코드일 경우 유용
  - 예- 오류처리 루틴
- **운영체제의 특별한 지원 없이** 프로그램 자체에서 구현 가능(OS는 라이브러리를 통해 지원 가능)
  - OS의 paging 기법과 구분되는 개념. 그러나 최근 혼용되어 사용되기도 한다.

### Dynamic Linking

- Linking을 실행시간(execution time)까지 미루는 기법
- **Static linking**
  - 라이브러리가 프로그램의 실행 파일 코드에 포함됨
  - 실행파일의 크기가 커짐
  - 동일한 라이브러리를 각각의 프로세스가 메모리에 올리므로 메모리낭비(eg. `printf` 함수의 라이브러리코드)
- **Dynamic linking**
  - 라이브러리 실행 시 연결(link)됨
  - 별도의 위치에 라이브러리 존재함
  - 라이브러리 호출 부분에 라이브러리 루틴의 위치를 찾기 위한 **stub**이라는 작은 코드를 둠
  - 라이브러리가 이미 메모리에 있으면 그 루틴의 주소로 가고 없으면 디스크에서 읽어옴
  - 운영체제의 도움이 필요

### Overlays

- 메모리에 프로세스의 부분 중 실제 필요한 정보만을 올림
- 프로세스의 크기가 메모리보다 클 때 유용
- 운영체제의 지원없이 사용자에 의해 구현
- 작은 공간의 메모리를 사용하던 초창기 시스템에서 수작업으로 프로그래머가 구현

### Swapping

- **Swapping**
  - 프로세스를 일시적으로 메모리에서 backing store로 쫓아내는 것
- **Backing store(=swap area)**
  - 디스크
    - 많은 사용자의 프로세스 이미지를 담을 만큼 충분히 빠르고 큰 저장공간
- **Swap in / Swap out**
  - 일반적으로 중기 스케줄러(swapper)에 의해 swap out 시킬 프로세스 선정
  - Prioirty-based CPU scheduling algorithm
    - Priority가 낮은 프로세스를 swapped out 시킴
    - prioirity가 높은 프로세스를 메모리에 올려놓음
  - Compile time 혹은 load time binding에서는 원래 메로리 위치로 swap in해야 함
  - **Execution time binding**에서는 추후 빈 메모리 영역 아무 곳에나 올릴 수 있음
  - Swap time은 대부분 transfer time(swap되는 양에 비례하는 시간)임 



## Allocationi of Physical Memory

- 메모리는 일반적으로 두 영역으로 나뉘어 사용

  - <u>**os 상주영역**</u>
    - Interrpt vector와 함께 낮은 주소영역 사용
  - <u>**사용자 프로세스 영역**</u>
    - 높은 주소영역 사용

- 사용자 프로세스 영역의 할당방법

  - **Contiguous allocation**

    각각의 프로세스가 메모리의 연속적인 공간에 적재되도록 하는 것. 통째로 올라가는 것. 

    - **Fixed partition allocation**
    - **Variable partition allocation**

  - **Noncontiguous allocation**

    하나의 프로세스가 메모리의 여러 영역에 분산되어 올라갈 수 있음

    - **Paging**
    - **Segmentation**
    - **Paged Segmentation**

### Contiguous Allocation

- **고정분할(Fixed partition)방식**
  - 물리적 메모리를 몇 개의 영구적 분할(Partition)로 나눔
  - 분할의 크기가 모두 동일한 방식과 서로 다른 방식이 존재
  - 분할 당 하나의 프로그램 적재
  - 융통성이 없음
    - 동시에 메모리에 load되는 프로그램의 수가 고정됨
    - 최대 수행 가능 프로그램 크기 제한
  - Internal fragmentation 발생(external fragmentation도 발생)
- **가변분할(Variable partition) 방식**
  - 프로그램의 크기를 고려해서 할당
  - 분할의 크기, 개수가 동적으로 변함
  - 기술적 관리기법 필요
  - External fragmentation 발생
  - **Hole**
    - 가용메모리공간
    - 다양한 크기의 hole이 메모리 여러 곳에 흩어져 있음
    - 프로세스가 도착하면 수용가능한 hole을 할당
    - 운영체제는 다음의 정보를 유지
      - 할당공간
      - 가용공간(hole)

<img width="515" alt="스크린샷 2021-04-27 오후 7 47 14" src="https://user-images.githubusercontent.com/72622744/116235634-1212f800-a799-11eb-8446-8ffb5258be02.png">

- 외부조각:  분할이 프로그램 크기보다 작아서 생기는 조각
- 내부조각: 분할의 크기가 프로그램크기보다 커서 남는 조각

#### Dynamic Storage-Allocation Problem

가변분할방식에서 size n인 요청을 만족하는 가장 적절한 hole을 찾는 문제

- **First-fit**
  - Size가 n 이상인 것 중 최초로 찾아지는 hole에 할당
- **Best-fit**
  - Size가 n 이상인 가장 작은 hole을 찾아서 할당
  - Hole의 리스트가 크기 순으로 정렬되지 않은 경우 모든 hole의 리스트를 탐색해야 함
  - 많은 수의 아주 작은 hole들이 생성됨
- **Worst-fit**
  - 가장 큰 hole에 할당
  - 역시 모든 리스트를 탐색해야 함
  - 상대적으로 아주 큰 hole들이 생성됨

#### Compaction

- External fragmentation 문제를 해결하는 한 가지 방법
- 사용 중인 메모리 영역을 한 군데로 몰고 hole들을 다른 한 곳으로 몰아 큰 block을 만드는 것
- 매우 비용이 많이 드는 방법임
- 최소한의 메모리 이동으로 compaction하는 방법(매우 복잡한 문제)
- Compaction은 프로세스의 주소가 실행 시간에 동적으로 재배치 가능한 경우에만 수행될 수 있다.



### Noncontiguous Allocation

#### Paging

- Paging
  - Process의 virtual memory를 동일한 사이즈의 page단위로 나눔
  - virtual memory의 내용이 page단위로 noncontiguous하게 저장됨
  - 일부는 backing storage에, 일부는  physical memory에 저장
- Basic Method
  - Physical memory를 동일한 크기의 frame으로 나눔
  - Logical memory를 동일 크기의 page로 나눔(frame과 같은 크기)
  - 모든 가용 frame들을 관리
  - Page table을 사용하여 logical address를 physical address로 변환
  - External fragmentation 발생 안 함
  - Internal fragmentation 발생 가능





