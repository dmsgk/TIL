# Chap 7. Deadlocks

## The Deadlock Problem

- **Deadlock**
  - 일련의 프로세스들이 서로가 가진 **자원**을 기다리며 block된 상태
- **Resource(자원)**
  - 하드웨어, 소프트웨어 등을 포함하는 개념
  - (예) I/O device, CPU cycle, memory space, semaphore 등
  - 프로세스가 자원을 사용하는 절차
    - **Request, Allocate, Use, Release**
- Deadlock Example 
  - 시스템에 2개의 tape drive가 있다.
  - 프로세스 p1과 p2 각각이 하나의 tape drive를 보유한 채 다른 하나를 기다리고 있다

## Deadlock 발생의 4가지 조건

4가지 조건을 모두 충족해야 deadlock이 발생함

- **Mutual exclusion(상호 배제)**

  - 매 순간 하나의 프로세스만이 자원을 사용할 수 있음

- **No preemption(비선점)**

  - 프로세스는 자원을 스스로 내어놓을 뿐 강제로 빼앗기지 않음

- **Hold and wait(보유대기)**

  - 자원을 가진 프로세스가 다른 자원을 기다릴 때 보유자원을 놓지 않고 계속 가지고 있음

- **Circular wait(순환대기)**

  - 자원을 기다리는 프로세스 간에 사이클이 형성되어야 함

  - 프로세스 p0,...,pn이 있을 때

    P0는 p1이 가진 자원을 기다림

    p1은 p2가 가진 자원을 기다림

    Pn-1은 pn이 가진 자원을 기다림

    pn은 p0이 가진 자원을 기다림

## Resource-Allocation Graph

자원할당 그래프에서 dealock이 있는지는

- 그래프에 <u>cycle이 없으면</u> <u>deadlock이 아니다.</u>
- 그래프에 <u>cycle이 있으면</u>
  - If only one instance per resource type, then **deadlock**
  - if several instances per resource type, possibility of deadlock



## Deadlock의 처리 방법

- **Deadlock Preventation**
- **Deadlock Avoidance**
  - 자원요청에 대한 부가적인 정보를 이용해서 deadlock의 가능성이 없는 경우에만 자원을 할당
  - 시스템 state가 원래 state로 돌아올 수 있는 경우에만 자원할당
- **Deadlock Detection and Recovery**
  - deadlock발생은 허용하되 그에 대한 detection 루틴을 두어 deadlock 발견시 recover
- **Deadlock Ignorance**
  - deadlock을 시스템이 책임지지 않음
  - unix를 포함한 대부분의 os가 채택하고 있음
    - deadlock이 빈번히 발생하는 이벤트가 아니기 때문에 미연에 방지하는 오버헤드가 더 들기 때문에 현대적 시스템에서는 deadlock이 생기든 말든 둔다.
- 위의 2가지 방법은 deadlock을 예방하는 것이고, 아래 2가지 방법은 deadlock발생은 허용하는 방법

### - Deadlock Prevention

자원할당 시 deadlock의 4가지 필요 조건 중 어느 하나가 만족되지 않도록 하는 것

- Mutual Exclusion
  - 공유해서는 안 되는 자원의 경우 반드시 성립해야 함
- Hold and Wait
  - 프로세스가 자원을 요청할 때 다른 어떤 자원도 가지고 있지 않아야 한다.
  - 방법1. 프로세스 시작 시 모든 필요한 자원을 할당받게 하는 방법
  - 방법2. 자원이 필요할 경우 보유 자원을 모두 놓고 다시 요청
- No Preemption
  - process가 어떤 자원을 기다려야 하는 경우 이미 보유한 자원이 선점됨
  - 모든 필요한 자원을 얻을 수 있을 때 그 프로세스는 다시 시작된다
  - State를 쉽게 save하고 restore할 수 있는 자원에서 주로 사용(cpu, memory)
- Circualr Wait
  - 모든 자원 유형에 할당 순서를 정하여 정해진 순서대로만 자원할당
  - 예를 들어 순서가 3인 자원 Ri를  보유 중인 프로세스가 순서가 1인 자원 Ri을 할당받기 위해서는 우선 Ri를 release해야 한다. 
  - => Utilzation 저하, throughput 감소, starvation 문제

### - Deadlock Avoidance

- 자원요청에 대한 부가정보를 이용해서 자원할당이 deadlock으로부터 안전한지를 동적으로 조사해서 안전한 경우에만 할당
  - i.e. 시스템이 **unsafe state**에 들어가지 않는 것을 보장
- 가장 단순하고 일반적인 모델은 프로세스들이 필요로 하는 각 자원별 최대 사용량을 미리 선언하도록 하는 방법임
- **Safe state**
  - 시스템 내의 프로세스들에 대한 **safe sequence**가 존재하는 상태
  - **Safe sequence**
    - 프로세스의 sequence가 safe하려면 pi의 자원요청이 "**가용자원 + 모든 pi의 보유자원**" 에 의해 충족되어야 함
    - 조건을 만족하면 다른방법으로 모든 프로세스의 수행을 보장
      - Pi의 자원요청이 즉시 충족될 수 없으면 모든 pi가 종료될 때까지 기다린다.
      - p(i-1)이 종료되면 pi의 자원요청을 만족시켜 수행한다.
- 시스템이 **safe state**에 있으면 **no deadlock**
- 시스템이 **unsafe state**에 있으면 **possibility of deadlock**
- 두 가지 Avoidance 알고리즘이 존재(후술)

#### Resource Allocation Graph Algorithm

- 자원에 대한 인스턴스가 하나밖에 없는 경우
- 자원할당그래프를 통해
- available한 자원을 모두 주는 것이 아니라 deadlock의 위험성이 있는 경우에는 애초에 자원을 주지 않음으로써 deadlock을 avoid하는 방식

#### Banker's Algorithm

- 자원에 대한 인스턴스가 여러 개인 경우
- 프로세스는 처음에 자원을 최대 얼마나 쓸지 미리 declare
- 가용자원만 가지고 최대요청을 충족시킬 수 없는 경우, 가용자원이 남아있다고 하더라도 요청을 받아들이지 않고 기다리게 한다.

<img width="503" alt="스크린샷 2021-04-21 오후 10 05 30" src="https://user-images.githubusercontent.com/72622744/115559285-8b6c9f80-a2ee-11eb-8a9f-f87f7f5f2f58.png">

### - Deadlock Detection  and Recovery

- Deadlock Detection

  - 자원 당 인스턴스가 하나인 경우에는 자원할당그래프로 

    - 자원할당 그래프에서의 cycle이 곧 deadlock을 의미

  - 자원 당 인스턴스가 여러 개인 경우에는 표를 그려서  

    - Banker's Algorithm과 유사한 방법 활용

    ![스크린샷 2021-04-22 오전 10.37.49](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-04-22 오전 10.37.49.png)

    - 가용자원으로 처리할 수 있는 요청이 있는지 살펴보 요청하지 않은 프로세스의 자원을 가용자원으로 합쳐놓고 가용자원으로 처리가능한지 확인하면서 문제가 발생하지 않고 끝까지 갈 수 있는지 확인
    - 현재 요청된 것이 없는 프로세스로에 할당된 자원이 반납된다고 가정
      - 0번 프로세스는 B를 하나 가지고 있고 추가로 요청한 것이 없기 때문에 낙관적으로 생각해서(진짜 deadlock만 찾겠다는 생각) B를 반납할 것으로 가정. 2번 프로세스도 마찬가지로 A 3개, C 3개 반납할 것으로 가정
    - 이와 같이 반납된 자원을 가지고 요청을 충족시킬 수 있는 경우 자원을 할당해주고, 요청한 프로세스는 다시 사용하고 자원을 반납한다고 가정
    - 요청을 다 받아들이는 시퀀스가 존재한다면 deadlock이 없다고 한다. 위의 예시는 deadlock이 아닌 상태.
    - 아래예시는 deadlock이 존재하는 경우

    ![스크린샷 2021-04-22 오전 10.52.40](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-04-22 오전 10.52.40.png)

- Wait-for graph 알고리즘

  - Resource type 당 single instance인 경우
  - Wait-for graph
    - 자원할당 그래프의 변형
    - 프로세스만으로 node 구성
    - pi가 가지고 있는 자원을 pk가 기다리는 경우 pk-> pi
  - Algorithm
    - Wait-for graph에 사이클이 존재하는지를 주기적으로 조사
    - O(n^2)

  ![스크린샷 2021-04-22 오전 10.35.25](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-04-22 오전 10.35.25.png)

- Recovery
  - **Process Termination**
    - Abort all deadlocked processes
    - Abort one process at a time until the deadlock cycle is eliminated
  - **Resource Preemption**
    - 비용을 최소화할 victim의 선정
    - safe state로 rollback 하여 process를 restart
    - Starvation문제
      - 동일한 프로세스가 계속해서 victim으로 선정되는 경우
      - Cost factor에 rollback 횟수도 같이 고려하는 방안을 생각해볼 수 있음

### - Deadlock Ignorance

- Deadlock이 일어나지 않는다고 생각하고 아무런 조치도 취하지 않음
  - Deadlock이 매우 드물게 발생하므로 deadlock에 대한 조치 자체가 더 큰 overhead일 수 있음
  - 만약, 시스템에 deadlock이 발생한 경우 시스템이 비정상적으로 작동하는 것을 사람이 느낀 후 직접 process를 죽이는 방법으로 대체
  - Unix, windows 등 대부분의 범용 os가 채택

