# Chap 6. Process Synchronization

### OS 에서 race condition은 언제 발생하는가?

1. Kernel 수행 중 인터럽트 발생 시
2. Pocess가 system call을 하여 kernel mode로 수행 중인데 context switch가 일어나는 경우
   - 해결책: 커널모드에서 수행 중일 때는 cpu를 preempt하지 않음. 커널모드에서 사용자모드로 돌아갈 때 preempt
3. Multiprocessor에서 shared memory 내의 kernel data
   - **해결책1.** 한 번에 하나의 cpu만이 커널에 들어갈 수 있게 하는 방법
   - **해결책2.** 커널 내부에 있는 각 공유 데이터에 접근할 때마다 그 데이터에 대한 lock/unlock 방법



## Process Synchronization 문제

- 공유데이터의 동시 접근은 데이터의 불일치문제를 발생시킬 수 있다.
- 일관성 유지를 위해서는 협력 프로세스 간의 실행순서를 정해주는 매커니즘 필요
- **Race Condition**
  - 여러 프로세스들이 동시에 공유데이터를 접근하는 상황
  - 데이터의 최종 연산 결과는 마지막에 그 데이터를 다룬 프로세스에 따라 달라짐
- Race condition을 막기 위해서는 concurrent process는 **동기화(synchronize)**되어야 한다. 



## The Critical-Section Problem

- n 개의 프로세스가 공유데이터를 동시에 사용하기를 원하는 경우
- 각 프로세스의 code segment에는 **공유데이터를 접근하는 코드인** **critical section**이 존재



### 프로그램적 해결법의 충족 조건

- #### **Mutual Exclusion**(상호 배제)

  - 하나의 프로세스가 critical section부분을 수행 중이면 다른 모든 프로세스들은 그들의 critical section에 들어가면 안 된다.

- #### **Progress** 

  - 아무도 critical section에 있지 않은 상태에서 critical section에 들어가고자 하는 프로세스가 있으면 critical section에 들어가게 해 주어야 한다.

- #### **Bounded Waiting**

  - 프로세스가 critical section에 들어가려고 요쳥한 후부터 그 요청이 허용될 때까지 다른 프로세스들이 critical section에 들어가는 횟수에 한계가 있어야 한다.  -> starvation 방지



### Algorithm 1

```c
// int turn;   /*initially turn = 0; */

do {
  while (turn != 0);			/*My turn?*/
  
  **critical section**
    
  turn = 1;								/**/
  remainder section
} while (1);
```

- 다른 프로세스가 critical section에 있는 경우 자신의 차례가 아니기 때문에 while문에서 기다리다가, 상대방의 critical section에서 빠져나올 때 turn 해주기 때문에 자신이 critical section으로 들어갈 수 있음.
- **문제점**: Mutual Section은 만족하나 Progress를 충족하지 않아 critical section을 해결하는 제대로 된 알고리즘이라고 할 수 없다.

### Algorithm 2

```c
//initially flag[모두] = false. /*no one is in CS*/

//하나의 프로세스 (Pi) cs 알고리즘
do {
  flag[i] = true; 			/* Pretend I am in */
  while (flag[j]);			/*Is he also in? then wait*/
  
  **critical section**
  
 flag[i] = false; 			/*I am out now*/
} while (1);
```

- 처음에는 모든 flag가 false로, 모두 critical section에 들어가고 싶어하지 않는 상태
- 본인이 critical section에 들어가고 싶으면 flag를 true로 만들고, 상대방의 flag를 확인한다. 상대방의 flag가 true이면 기다리고 false이면 본인이 critical section에 들어간다. 
- Critical section에서 나올 때에는 flag를 false로 바꾸어 상대방이 들어갈 수 있도록 한다. 
- **문제점:** 둘 다 2행까지 수행 후 서로 기다리는 상황이 발생할 수 있다. Progress 조건을 충족하지 못한다. 



### Algorithm 3 (Peterson's Algorithm)

```c
do {
  flag[i] = true;          				/*My intention is to enter....*/
  turn = j;												/*Set to his turn*/
  while (flag[j] && turn == j); 	/*wait only if ...*/
  
  **critical section**
    
  flag[i] = false;
  remainder section
} while(1);
```

- turn과 flag 변수를 모두 사용한다. 
- cs에 들어가고자 할 때 flag를 true로 바꾸고 turn을 상대방으로 바꾼다. 
- 상대바이 깃발을 들고 있으며, 상대방 차례일 때는 상대방이 들어가고 아닌 경우 본인이 들어간다. 
- flag를 false로 바꾼다. 
- **Mutual Exclusion, Progress, Bounded Waiting** 세 조건을 모두 만족하는 알고리즘
- **문제점**
  - **Busy Waiting(=spin lock)** :계속 cpu와 memory를 쓰면서 wait. 비효율성



### Synchronization Hardware

- 문장 하나하나가 실행되는 도중에도 cpu를 빼앗길 수 있기 때문에, 중간중간 cpu가 뺏긴다는 가정 하에 알고리즘을 짜다 보니 앞에서와 같이 소프트웨어적으로 복잡한 코드가 만들어졌다. 
  - 데이터를 읽고 쓰는 것을 하나의 instruction으로 수행할 수 없기 때문에. 
- 인스트럭션 하나를 가지고 데이터를 읽는 작업과 데이터를 쓰는 작업을 동시에 수행할 수 있는 (task & modify) 하드웨어적인 인스트럭션이 지원된다면 **간단하게** lock을 걸고 푸는 일을 해결할 수 있다.

```c
do {
  while (Test_and_Set(lock));
  
  critical section
    
  lock = false;
  remainder section
}
```

- critical section에 들어가기 전 다른 lock이 있는지 확인하고 lock이 없으면 lock을 걸고 들어가고, 빠져나올 때 lock을 풀어준다. 



### Semaphores

- 앞의 방식들을 추상화시킴
- Semaphore S
  - integer variable
  - 아래의 두 가지 atomic 연산에 의해서만 접근 가능(p연산, v연산)
    - P(S) : 공유데이터를 획득하는 과정
    - V(S) : 다 사용하고 반납하는 과정



### Critical Section of n Processes

- 앞에서처럼 프로그래머가 일일이 코딩을 하기보다 추상화된 자료구조를 주고, 프로그래머는 semaphore를 통해 프로그래밍을 하면 훨씬 간단하게 작성할 수 있음

  

