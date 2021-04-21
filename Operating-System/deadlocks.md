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

deadlock이 빈번히 발생하는 이벤트가 아니기 때문에 미연에 방지하는 오버헤드가 더 들기 때문에 현대적 시스템에서는 deadlock이 생기든 말든 둔다.

- **Deadlock Preventation**
- **Deadlock Avoidance**
  - 자원요청에 대한 부가적인 정보를 이용해서 deadlock의 가능성이 없는 경우에만 자원을 할당
  - 시스템 state가 원래 state로 돌아올 수 있는 경우에만 자원할당
- **Deadlock Detection and recovery**
  - deadlock발생은 허용하되 그에 대한 detection 루틴을 두어 deadlock 발견시 recover
- **Deadlock Ignorance**
  - deadlock을 시스템이 책임지지 않음
  - unix를 포함한 대부분의 os가 채택하고 있음

### Deadlock Prevention

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

### Deadlock Avoidance

- 자원요청에 대한 부가정보를 이용해서 자원할당이 deadlock으로부터 안전한지를 동적으로 조사해서 안전한 경우에만 할당
- 가장 단순하고 일반적인 모델은 프로세스들이 필요로 하는 각 자원별 최대 사용량을 미리 선언하도록 하는 방법임
- Safe state
  - 시스템 내의 프로세스들에 대한 safe sequence가 존재하는 상태
- Safe sequence
  - 프로세스의 sequence가 safe하려면 pi의 자원요청이 **가용자원 + 모든 pi의 보유자원**에 의해 충족되어야 함
  - 조건을 만족하면 다른방법으로 모든 프로세스의 수행을 보장
    - Pi의 자원요청이 즉시 충족될 수 없으면 모든 pi가 종료될 때까지 기다린다.
    - p(i-1)이 종료되면 pi의 자원요청을 만족시켜 수행한다.

- 두 가지 Avoidance 알고리즘이 존재

#### Resource Allocation Graph Algorithm

자원에 대한 인스턴스가 하나밖에 없는 경우

available한 자원을 모두 주는 것이 아니라 deadlock의 위험성이 있는 경우에는 애초에 자원을 주지 않음으로써 deadlock을 avoid하는 방식

#### Banker's Algorithm

자원에 대한 인스턴스가 여러 개인 경우

가용자원만 가지고 최대요청을 충족시킬 수 없는 경우, 요청을 받아들이지 않고 기다리게 한다.

![스크린샷 2021-04-21 오후 10.05.30](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-04-21 오후 10.05.30.png)