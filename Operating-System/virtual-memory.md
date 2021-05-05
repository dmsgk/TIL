# Chap 9. Virtual Memory

*virtual memory 기법은 전적으로 운영체제가 관여*

## Demand Paging

- 실제로 필요할 때 page를 메모리에 올리는 것

  - 얻는 효과
    - I/O의 감소
    - Memory 사용량 감소
    - 빠른 응답시간
    - 더 많은 사용자 수용

- Valid/ Invalid bit의 사용

  - Invalid의 의미

    - 사용되지 않는 주소영역인 경우
    - 페이지가 물리적 메모리에 없는 경우

  - 처음에는 모든 page entry가 invalid로 초기화

  - address translation 시에 invalid bit이 set되어 있으면

     => **Page fault** 발생

## Page Fault

- Invalid page를 접근하면 MMU가 trap을 발생시킴(page fault trap)
- Kernel mode로 들어가서 page fault handler가 invoke됨
- 다음과 같은 순서로 page fault를 처리한다
  1. Invalid reference?  => abort process
  2. Get a empty page frame( 없으면 뺏어온다: replace -> Free frame이 없는 경우 파트 참조)
  3. 해당 페이지를 disk에서 메모리로 읽어온다
     1. Disk I/O가 끝나기까지 이 프로세스는 CPU를 preempt당함 (block)
     2. Disk read가 끝나면 page tables entry 기록, valid/invalid bit = "valid"
     3. ready queue에 process를 insert -> dispatch later
  4. 이 프로세스가 cpu를 잡고 다시 running
  5. 아까 중단되었던 instruction을 재개

<img width="515" alt="스크린샷 2021-05-03 오후 8 50 14" src="https://user-images.githubusercontent.com/72622744/116877195-957c8f80-ac58-11eb-820d-e0ad34b9b11f.png">

메모리 레퍼런스가 있었는데 invalid로 표시가 된 경우. trap이 걸려서 cpu가 운영체제로 넘어간다. 운영체제는 backing store에 있는 페이지를 물리적 메모리로 올려둔다. 올려둔 작업이 끝나면 해당하는 frame #를 entry에 적어두고 valid로 바꾼다. 이후 cpu를 얻어서 주소변환을 하면 valid로 되어 있으니 주소변환이 정상적으로 되어 해당하는 물리적 메모리의 page frame을 접근할 수 있게 된다.



<img width="512" alt="스크린샷 2021-05-03 오후 8 54 56" src="https://user-images.githubusercontent.com/72622744/116877275-b04f0400-ac58-11eb-8883-bc0542f4f67b.png">



### Free frame이 없는 경우

- **Page replacement**

  - 어떤 frame을 빼앗아올지 결정해야 함
  - 곧바로 사용되지 않을 page를 쫓아내는 것이 좋음
  - 동일한 페이지가 여러 번 메모리에서 쫓겨났다가 다시 들어올 수 있음

- **Replacement Algorithm**

  - **Page-fault rate를 최소화**하는 것이 목표

  - 알고리즘의 평가

    - 주어진 page reference string에 대해 page fault를 어라나 내는지 조사

  - Reference string의 예

    1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5.



## Replacement Alogrithm	

### Optimal Algorithm

- MIN(OPT): 가장 먼 미래에 참조되는 page를 replace
- 미래의 참조를 어떻게 아는가?
  - Offline algorithm	( 미리 알고있다는 가정하에 운영하는 알고리즘. 온라인이 아니라)
- 실제로 사용할 수는 없지만 다른 알고리즘의 성능에 대한 upper bound 제공(가장 적거나 같은 page fault를 발생시킨다.)
  - Belady's optimal algorithm, MIN, OPT 등으로 불림

<img width="499" alt="스크린샷 2021-05-03 오후 9 08 38" src="https://user-images.githubusercontent.com/72622744/116877341-c78df180-ac58-11eb-9022-1f7b92b29807.png">


### FIFO(First In First Out) Algorithm

- FIFO: 먼저 들어온 것을 먼저 내쫓음

<img width="514" alt="스크린샷 2021-05-03 오후 9 13 30" src="https://user-images.githubusercontent.com/72622744/116877445-eb513780-ac58-11eb-94e5-0e1a65f8222e.png">

FIFO Anomaly : 메모리 프레임을 늘려주어도 page fault가 더 많이 발생하는 상황이 있을 수 있다.



### LRU (Least Recently Used) Algorithm

- 가장 오래 전에 참조된 것을 지움

<img width="493" alt="스크린샷 2021-05-03 오후 9 16 49" src="https://user-images.githubusercontent.com/72622744/116877542-0a4fc980-ac59-11eb-966e-21c6755a5940.png">


### LFU(Least Freqeuntly Used) Algorithm

- LFU: 참조횟수(reference count)가 가장 적은 페이지를 지움
  - 최저 참조 횟수인 page가 여럿 있는 경우
    - LFU 알고리즘 자체에서는 여러 page 중 임의로 선정한다
    - 성능 향상을 위해 가장 오래 전에 참조된 page를 지우게 구현할 수도 있다
  - 장단점
    - LRU처럼 직전 참조 시점만 보는 것이 아니라 장기적인 시간 규모를 보기 때문에 page의 인기도를 좀 더 정학히 반영할 수 있음
    - 참조 시점의 최근성을 반영하지 못함
    - LRU보다 구현이 복잡함



<img width="514" alt="스크린샷 2021-05-03 오후 9 29 15" src="https://user-images.githubusercontent.com/72622744/116877608-218eb700-ac59-11eb-9725-fd84760b056e.png">





## 다양한 Caching 환경

- Caching 기법

  - 한정된 빠른공간(=캐쉬)에 요청된 데이터를 저장해두었다가 후속요청시 캐쉬로부터 직접 서비스하는 방식
  - paging system 외에서도 cache memory, buffer caching, Web caching 등 다양한 분야에서 사용

- 캐쉬 운영의 시간제약

  - 교체알고리즘에서 삭제할 항목을 결정하는 일에 지나치게 많은 시간이 걸리는 경우 실제시스템에서 사용할 수 없음

  - Buffer caching이나 Web caching의 경우

    - O(1)에서 O(log n) 정도까지 허용

  - **Paging system인 경우**

    - page fault인 경우에만 OS가 관여함
    - 페이지가 이미 메모리에 존재하는 경우 참조시각 등의 정보를 OS가 알 수 없음
    - O(1)인 LRU의 list 조작조차 불가능

    -> LRU, LFU 가능하지 않음





## Clock Algorithm

- Clock Algorithm
  - LRU의 근사 알고리즘
  - 여러 명칭으로 불림
    - Second chance algorithm
    - NUR(Not Used Recently) 또는 NRU(Not Recently Used)
  - Reference bit을 사용해서 교체대상페이지 선정(circular list)
  - Reference bit가 0인 것을 찾으면 그 페이지를 교체
  - 한 바퀴 되돌아와서도(=second chance) 0이면 그때에는 replace 당함
  - 자주 사용되는 페이지라면 second chance가 올 때 1
- Clock Algorithm의 개선
  - Reference bit과 modified bit을 함께 사용
  - Reference bit = 1: 최근에 참조된 페이지
  - Modified bit = 1 : 최근에 변경된 페이지(I/O를 동반하는 페이지)

![스크린샷 2021-05-05 오후 3.58.36](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-05 오후 3.58.36.png)



## Page frame의 Allocation

- Allocation problem: 각 프로세스에 얼마만큼의 page frame을 할당할 것인가
- Allocation의 필요성
  - 메모리 참조 명령어 수행 시 명령어, 데이터 등 여러 페이지 동시 참조
    - 명령어 수행을 위해 최소한 할당되어야 하는 frame의 수가 있음
  - Loop를 구성하는 page들은 한꺼번에 allocate되는 것이 유리함
    - 최소한의 allocation이 없으면 매 loop마다 page fault
- Allocation Scheme
  - **Equal allocation**: 모든 프로세스에 똑같은 개수 할당
  - **Proportional allocation** : 프로세스 크기에 비례하여 할당
  - **Priority allocation**: 프로세스의 priority에 따라 다르게 할당



### Global vs Local Replacement

- Global replacement
  - Replace시 다른 process에 할당된 frame을 빼앗아 올 수 있다
  - Process 별 할당량을 조절하는 또다른 방법임
  - FIFO, LRU, LFU등의 알고리즘읠 global replacement로 사용시에 할당
  - Working set, PFF 알고리즘 사용
- Local replacement
  - 자신에게 할당된 frame 내에서만 replacement
  - FIFO, LRU, LFU 등의 알고리즘을 process 별로 운영시



### Thrashing

- 프로세스의 원활한 수행에 필요한 최소한의 page frame 수를 할당받지 못한 경우 발생
- page fault rate이 매우 높아짐
- cpu utilization이 낮아짐(한번 실행하려면 그 프로그램이 메모리에 없음, I/O를 해야 한다..)
- OS는 MPD를 높여야 한다고 판단
- 또다른 프로세스가 시스템에 추가됨
- 프로세스당 할당된 frame수가 더욱 감소
- 프로세스는 page의 swap in/ swap out으로 매우 바쁨
- 대부분의 시간에 cpu는 한가함
- Low throughput



## Working-Set Model

- Locality of reference
  - 프로세스는 특정시간 동안 일정 장소만을 집중적으로 참조한다
  - 집중적으로 참조되는 해당 page들의 집합을 locality set이라 함
- Working-set Model
  - Locality에 기반하여 프로세스가 일정 시간동안 원활하게 수행되기 위해 한꺼번에 메모리에 올라와있어야 하는 page들의 집합을 Working Set이라 정의함
  - Working Set 모델에서는 process의 working set 전체가 메모리에 올라와 있어야 수행되고 그렇지 않을 경우 모든 frame을 반납한 후 swap out(suspend)
  - Thrashing을 방지함
  - Multiprogramming degree를 결정함

