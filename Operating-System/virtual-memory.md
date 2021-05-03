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

![스크린샷 2021-05-03 오후 8.50.14](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-03 오후 8.50.14.png)

메모리 레퍼런스가 있었는데 invalid로 표시가 된 경우. trap이 걸려서 cpu가 운영체제로 넘어간다. 운영체제는 backing store에 있는 페이지를 물리적 메모리로 올려둔다. 올려둔 작업이 끝나면 해당하는 frame #를 entry에 적어두고 valid로 바꾼다. 이후 cpu를 얻어서 주소변환을 하면 valid로 되어 있으니 주소변환이 정상적으로 되어 해당하는 물리적 메모리의 page frame을 접근할 수 있게 된다.



![스크린샷 2021-05-03 오후 8.54.56](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-03 오후 8.54.56.png)



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

![스크린샷 2021-05-03 오후 9.07.37](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-03 오후 9.08.38.png)



### FIFO(First In First Out) Algorithm

- FIFO: 먼저 들어온 것을 먼저 내쫓음

![스크린샷 2021-05-03 오후 9.13.30](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-03 오후 9.13.30.png)

FIFO Anomaly : 메모리 프레임을 늘려주어도 page fault가 더 많이 발생하는 상황이 있을 수 있다.



### LRU (Least Recently Used) Algorithm

- 가장 오래 전에 참조된 것을 지움

![스크린샷 2021-05-03 오후 9.16.49](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-03 오후 9.16.49.png)



### LFU(Least Freqeuntly Used) Algorithm

- LFU: 참조횟수(reference count)가 가장 적은 페이지를 지움
  - 최저 참조 횟수인 page가 여럿 있는 경우
    - LFU 알고리즘 자체에서는 여러 page 중 임의로 선정한다
    - 성능 향상을 위해 가장 오래 전에 참조된 page를 지우게 구현할 수도 있다
  - 장단점
    - LRU처럼 직전 참조 시점만 보는 것이 아니라 장기적인 시간 규모를 보기 때문에 page의 인기도를 좀 더 정학히 반영할 수 있음
    - 참조 시점의 최근성을 반영하지 못함
    - LRU보다 구현이 복잡함



![스크린샷 2021-05-03 오후 9.29.15](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-03 오후 9.29.15.png)



