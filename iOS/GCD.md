# Grand Central Dispatch(GCD)

> 키워드: GCD, Dispatch Queue, Dispatch Source, Operation Queue, Dispatch Queue의 종류, Dispatch Source

## GCD

- Grand Central Dispatch(GCD)는 멀티코어와 멀티 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술
- 기본적으로 스레드 풀의 관리를 프로그래머가 아닌 운영체제에서 관리하기 때문에 프로그래머가 태스크(작업)을 비동기적으로 쉽게 사용가능
-  프로그래머가 실행할 태스크(작업)을 생성하고 `Dispatch Queue`에 추가하면 `GCD`는 태스크(작업)에 맞는 스레드를 자동으로 생성해서 실행하고 작업이 종료되면 해당 스레드를 제거한다.

## Dispatch Queue

- 디스패치 대기열(Dispatch Queue)은 작업을 연속적 혹은 동시에 진행하기는 하지만, 언제나 먼저 들어오면 먼저 나가는 순서로 실행.
  -  `Serial Dispatch Queue`는 한 번에 하나의 작업만을 실행하며, 해당 작업이 대기열에서 제외되고 새로운 작업이 시작되기 전까지 기다림
  - `Concurrent Dispatch Queue`는 이미 시작된 작업이 완료될 때까지 기다리지 않고 가능한 많은 작업을 진행. 
- 디스패치 대기열(Dispatch Queue)은 `GCD` 기술 일부



### Dispatch Queue의 종류

| Main Queue                                                   | Global Queue                                                 | Private Queue                                                |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1. 오직 한 개 <br />2. **Serial** <br />3. 메인 스레드에서 처리<br /> 4.`DispatchQueue.main.async{}` | 1. 종류 여러 개 <br />2. 기본 설정: **Concurrent**<br />3.중요도에 따라 서비스 품질(QoS)을 설정한 큐 생성 가능.<br /> 4. `DispatchQueue.global()` 또는`DispatchQueue.global(qos:)` | 1. 커스텀으로 만듦. <br />2. 기본 설정: **Serial** (Concurrent 설정 가능) <br />3. QoS 설정도 가능 <br />4. `DispatchQueue(label:)` |

### Dispatch Queue를 사용하는 기술

#### Dispatch Source

- 디스패치 소스(Dispatch Source)는 특정 유형의 시스템 이벤트를 비동기적으로 처리하기 위한 C 기반 메커니즘
-  특정 유형의 시스템 이벤트에 대해 정보를 캡슐화하고, 해당 이벤트가 발생할 때마다 특정 클로저(블록) 객체 혹은 기능을 디스패치 대기열(Dispatch Queue)에 전달함
-  Grand Central Dispatch supports the following types of dispatch sources
  - *Timer dispatch sources* generate periodic notifications.
  - *Signal dispatch sources* notify you when a UNIX signal arrives.
  - *Descriptor sources* notify you of various file- and socket-based operations, such as:
    - When data is available for reading
    - When it is possible to write data
    - When files are deleted, moved, or renamed in the file system
    - When file meta information changes
  - *Process dispatch sources* notify you of process-related events, such as:
    - When a process exits
    - When a process issues a `fork` or `exec` type of call
    - When a signal is delivered to the process
  - *Mach port dispatch sources* notify you of Mach-related events.
  - *Custom dispatch sources* are ones you define and trigger yourself.

#### Dispatch Groups

- 관련 문서 : [Waiting on Groups of Queued Tasks]( https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/OperationQueues/OperationQueues.html#//apple_ref/doc/uid/TP40008091-CH102-SW25)

#### Dispatch Semaphores

- 관련 문서: [Using Dispatch Semaphores to Regulate the Use of Finite Resources](https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/OperationQueues/OperationQueues.html#//apple_ref/doc/uid/TP40008091-CH102-SW24)



## Operation Queue

- 연산 대기열(Operation Queue)은 `Concurrent Dispatch Queue`와 동일하게 동작하며, `Operation Queue` 클래스에 의해 구현.
- 디스패치 대기열은 항상 먼저 들어오면 먼저 나가는 순서(FIFO - First in First out)로 작업을 실행하지만, 연산 대기열(Operation Queue)은 작업의 실행 순서를 결정할 때에 다른 요인들을 고려
- 연산 대기열(Operation Queue)은 디스패치 대기열(Dispatch Queue)과 매우 유사한 클래스

### GCD와 연산 대기열 (Operation Queue)

#### 차이점

- Operation Queue에서는 동시에 실행할 수 있는 연산(Operation)의 최대 수를 지정할 수 있음
- Operation Queue에서는 KVO(Key Value Observing)을 사용할 수 있는 많은 프로퍼티들이 존재
- Operation Queue에서는 연산(Operation)을 일시 중지, 다시 시작 및 취소를 할 수 있음

#### 언제 사용해야 할까?

- **Operation Queue** : 
  - 비동기적으로 실행되어야 하는 작업을 객체 지향적인 방법으로 사용하는 데 적합 
  - KVO(key Value Observing)를 사용해 작업 진행 상황을 감시하는 방법이 필요할 때도 적합
- **GCD :** 
  - 작업이 복잡하지 않고 간단하게 처리하거나 특정 유형의 시스템 이벤트를 비동기적으로 처리할 때 적합.  예- 타이머, 프로세스



### References

- https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/GCDWorkQueues/GCDWorkQueues.html#//apple_ref/doc/uid/TP40008091-CH103-SW1
- https://www.boostcourse.org/mo326/lecture/16916?isDesc=false
- https://lena-chamna.netlify.app/post/concurrency_programming_thread_and_queue/