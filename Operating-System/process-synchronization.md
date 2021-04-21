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



## Semaphores

- 앞의 방식들을 추상화시킴
- Semaphore S
  - integer variable
  - 아래의 두 가지 atomic 연산에 의해서만 접근 가능(p연산, v연산)
    - P(S) : 공유데이터를 획득하는 과정
    - V(S) : 다 사용하고 반납하는 과정
- **Two types of semaphore**
  - Counting semaphores
    - 도메인이 0이상인 임의의 정수값
    - 주로 resource counting에 사용
  - Binary semaphores
    - 0 또는 1 값만 가질 수 있는 semaphore
    - 주로 mutual exclusion(lock/unlock)사용



### Critical Section of n Processes

- 앞에서처럼 프로그래머가 일일이 코딩을 하기보다 추상화된 자료구조를 주고, 프로그래머는 semaphore를 통해 프로그래밍을 하면 훨씬 간단하게 작성할 수 있음

- ##### Busy-wait 방식의 구현 (=spin lock) 

  ```c
  // semaphore mutex; /* initially 1: 1개가 CS에 들어갈 수 있다.*/
  
  do {
    P(mutex);						/*If positive, dec & enter, otherwise wait*/
    critical section
    V(mutex);						/*Increment semaphore*/
    remainder section
    
  }while (1);
  ```
  
- ##### BlocK & Wakeup 방식의 구현(= sleep lock)

  - Semaphore를 다음과 같이 정의

    ```c
    typedef struct {
      int value;					/*semaphore*/
      struct process *L;	/*process wait queue*/
    } semaphore
    ```
    - p연산

      ```c
      S.value--;									/*prepare to enter*/
      if (S.value < 0) {					/*negative,I cannot enter*/
        add this process to S.L;
        
        block();
      }
      ```

      자원의 여분이 있다면 획득, 그렇지 않으면 sleep상태(blocked)로 바뀐다.

    - v연산

      ````c
      S.value++;
      if (S.value <= 0) {
        remove a process P from S.L;
        
        wakeup(P)
      }
      
      //자원을 다 내놓았는데도 불구하고 그 값이 0이하라는 것은 이 프로세스를 기다리면서 잠들어있는 프로세스가 있다는 의미
      ````

      자원을 다 쓰고 반납하면서 잠들어있는 프로세스가 있다면 **깨워주는(wakeup)과정도 포함**되어 있다.

- Which is Better?
  - 보통은 block & wakeup이 효율적. 구체적으로는
  - **Block/wakeup의 overhead vs Critical section 길이** 를 비교하여 결정한다.
    - Critical section의 길이가 긴 경우 block/wakeup이 적당
    - Critical section의 길이가 매우 짧은 경우 block/wakeup 오버헤드가 busy-wait 오버헤드보다 더 커질 수 있음



### Deadlock and Starvation

- **Deadlock**
  
  - 둘 이상의 프로세스가 서로 상대방에 의해 충족될 수 있는 event를 무한히 기다리는 현상
  - ex) Dining- Philosophers Problem에서 모두가 왼쪽 젓가락을 집는 경우
- **Starvation**
  
  - Indefinite blocking : 프로세스가 suspend된 이유에 해당하는 세마포어 큐에서 빠져나갈 수 없는 현상
  
    

## Classical Problems of Synchronization

### Bounded-Buffer-Problem(Producer-Consumer Problem)

- producer process, consumer process 존재
  - producer process
    1. Empty 버퍼가 있는지? (없으면 기다림)
    2. 공유데이터에 lock을 건다
    3. empty buffer에 데이터 입력 및 buffer조작
    4. lock을 푼다
    5. full buffer 하나 증가
  - consumer process
    1. Full 버퍼가 있는지? (없으면 기다림)
    2. 공유데이터에 lock을 건다
    3. Full buffer에서 데이터 꺼내고 buffer조작
    4. lock을 푼다
    5. Empty buffer 하나 증가
  
- Synchronization으로 해결해야 하는 문제
  - 버퍼의 크기가 유한한 환경에서, 버퍼가 가득 찬 경우 생산자 프로세스는 자원이 생길 때까지 기다려야 한다. 소비자 프로세스는 빈 버퍼만 있는 경우 생산자 프로세스가 내용을 채워줄 때까지 기다려야 한다. 그 때 가용자원의 개수를 센다.
  - 동시에 공유버퍼를 접근하는 것을 막기 위에 lock을  걸고 풀고 하는 역할.
  
- 해결책 

   <img width="448" alt="스크린샷 2021-04-20 오후 4 20 25" src="https://user-images.githubusercontent.com/72622744/115398826-84785b00-a222-11eb-8749-838a0c750f7d.png">

### Readers and Writers Problem

- 읽는 프로세스와 쓰는 프로세스로 구성

- 공유데이터를 DB로 명명

- 읽는 작업은 동시에 데이터에 접근해도 문제가 생기지 않지만, 쓰는 작업은 동시에 데이터에 접근하면 문제가 생긴다.

- 해결책

  - writer가 db에 접근 허가를 아직 얻지 못한 상태에서는 모든 대기중인 reader를 다 db에 접근하게 해준다.
  - writer는 대기중인 reader가 하나도 없을 때 db접근이 허용된다.
  - 일단 writer가 db에 접근 중이면 reader들은 접근이 금지된다.
  - writer가 db에서 빠져나가야만 reader의 접근이 허용된다.

  <img width="445" alt="스크린샷 2021-04-20 오후 4 27 00" src="https://user-images.githubusercontent.com/72622744/115398837-87734b80-a222-11eb-98f1-14b15172af02.png">

### Dininig- Philosophers Problem

- 철학자 다섯 명이 원탁에 앉아있음

- 두 가지 일

  - 생각하기
  - 밥 먹기

- 배고파지면 왼쪽 오른쪽 젓가락 집어서 밥을 먹고, 배불러지면 젓가락을 놓고 생각하는 일을 반복

- 세마포어로 해결하는 코드

  ```c
  do {
    P(chopstick[i]);
    P(chopstick[i+1] % 5);
    ...
    eat();
    ...
    V(chopstick[i]);
    V(chopstick[(i+1)%5]);
    ...
    think();
    ...
  } while(1);
  ```

- 위 solution의 문제점

  - **Deadlock의 가능성**이 있음
    - 모두 왼쪽 젓가락을 잡아버리면 오른쪽 젓가락을 모두가 집을 수 없음

- 해결방안

  - 4명의 철학자만이 테이블에 동시에 앉을 수 있도록 한다.
  - 젓가락을 두 개 모두 집을 수 있을 때에만 젓가락을 집을 수 있게 한다.
  - 비대칭
    - 짝수(홀수) 철학자는 왼쪽(오른쪽) 젓가락부터 집도록

## Monitor

- Semaphore의 문제점
  - 코딩하기 힘들다
  - 정확성(correctness)의 입증이 어렵다
  - 자발적 협력(voluntary coopertation)이 필요하다
  - 한 번의 실수가 모든 시스템에 치명적 영향

- 세마포어의 문제로 인해 synchronization에서는 monitor를 제공한다.

- 동시 수행중인 프로세스 사이에서 abstract data type의 안전한 공유를 보장하기 위한 high-level synchronization construct

-  모니터는 동시접근을 모니터차원에서 막는다.

- 하나의 프로세스만 모니터에 접근할 수 있도록 하고 나머지 프로세스는 줄 서서 기다리게 한다.

- 프로그래머가 동기화 제약 조건을 명시적으로 코딩할 필요 없음

- 프로세스가 모니터 안에서 기다릴 수 있도록 하기 위해 **condition variable** 사용

    	condition x, y:

  - wait연산, signal연산에 의해서만 접근가능
  - **x.waint():**
    - x.wait()을 invoke한 프로세스는 다른 프로세스가 x.signal()을 invoke하기 전까지 suspend된다.
  - **x.signal():**
    - x.signal()은 정확하게 하나의 suspend된 프로세스를 resume한다. suspend된 프로세스가 없으면 아무 일도 일어나지 않는다.

-  semaphre와 달리 lock을 걸 필요가 없다.

- Bounded-Buffer Problem을 monitor로 해결하는 코드

    <img width="448" alt="스크린샷 2021-04-20 오후 5 06 14" src="https://user-images.githubusercontent.com/72622744/115398847-893d0f00-a222-11eb-8e7e-db27d6649ad5.png">

- Dining Philosophers Problem
<img width="510" alt="스크린샷 2021-04-21 오후 9 02 01" src="https://user-images.githubusercontent.com/72622744/115559128-5eb88800-a2ee-11eb-82fb-ea5e6d470455.png">





