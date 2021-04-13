# Chap 5. CPU Scheduling

## CPU Scheduling의 필요성 - cpu burst time의 분포

- Cpu-burst-time을 볼 때 cpu burst가 짧은, 즉 중간에 I/O가 많이 끼어드는**(I/O bound job**) 빈도가 매우 높았으며 cpu burst가 아주 긴(**cpu bound job**) 프로세스의 빈도가 낮았다.
  - 참고 - 프로세스의 특성 분류	
    - I/O bound process
      - cpu를 잡고 계산하는 시간보다 I/O에 많은 시간이 필요한 job (many short CPU bursts)
    - Cpu bound process
      - 계산 위주의 job (few very long CPU bursts)



- 여러 종류의 job(=process) 가 섞여 있기 때문에 cpu 스케줄링이 필요함
  - Interactive job에게 적절한 response 제공 요망(cpu를 공평하게 주기보다 사람과 interaction을 하는 job에게 스케줄링을 하도록, 사람을 오래 기다리지 않도록 하는 효율적인 방식)
  - cpu와 I/O 장치 등 시스템 자원을 골고루 효율적으로 사용



## Cpu Scheduler & Dispatcher

-  **Cpu Scheduler**
  - Ready 상태의 프로세스 중에서 이번에 cpu를 줄 프로세스를 고른다.

- **Dispatcher**
  - cpu의 제어권을 cpu scheduler에 의해 선택된 프로세스에 넘긴다.
  - 이 과정을 context switch(문맥교환) 라고 한다.



- Cpu scheduling이 필요한 경우는 다음 경우와 같이 프로세스에게 상태변화가 있는 경우이다.

  1. Running -> Blocked  (ex.  i/o 요청하는 시스템 콜)
  2. Running -> Ready  (ex. 할당시간 만료로 timer interrupt)
  3. Blocked -> Ready  (ex. I/O 완료 후 인터럽트)
  4. Terminate

  위의 1, 4의 스케줄링은 **nonpreemptive(= 강제로 빼앗지 않고 자진 반납)** - 비선점형.

  나머지는 **preemptive(= 강제로 빼앗음)** - 선점형. 대부분의 경우 여기에 해당함




## Scheduling Criteria 

Performance Index(= Performance Measure, 성능 척도)

스케줄링의 성능을 측정할 수 있는 기준

- <u>시스템 입장</u>에서의 성능척도

  cpu 하나로 최대한 일을 많이 시킬수록 성능이 좋음

  - **CPU utilization(이용률)**
    - 전체 시간 중 cpu가 일한 시간의 비율
  - **Throughput(처리량)**
    - 주어진 시간 동안 몇 개의 작업을 했는지.

- <u>프로세스 입장</u>에서의 성능척도

  cpu를 빨리 얻어서 일을 빠르게 끝낼수록 성능이 좋음

  - **Turnaround time(소요시간, 반환시간)**
    - cpu를 쓰러 들어와서 다 쓰고 나갈 때까지 걸리는 시간. 
  - **Waiting time(대기시간)**
    - ready queue에서 기다린 시간.
  - **Response time(응답시간)**
    - ready queue에 들어와서 처음으로 cpu를 얻기까지 걸린 시간. 
    - waiting time과 구별: 선점형 프로그래밍의 경우 줄 서서 기다리는 시간이 여러 번 존재하므로 wating time과 차이가 존재하는 개념



## 스케줄링 방법

### FCFS(First-Come First-Served)

- 먼저 온 작업을 먼저 처리하는 스케줄링 방법
- **문제점**
  - **Convoy effec**t가 발생할 수 있음
    - **Convoy effect** : 긴 시간을 요하는 프로세스 뒤에 짧은 시간이 걸리는 프로세스가 있는 경우, 짧은 프로세스가 지나치게 오래 기다리는 현상을 의미함.

### SJF(Shortest-Job-First)

- 시간이 짧게 걸리는 작업 순으로 처리하는 스케줄링 방법
- 주어진 프로세스에 대해 **minimum average wating time**을 보장한다.
- Two schemes
  - <u>Nonpreemptive</u> 
    - 일단 cpu를 잡으면 그보다 짦은 프로세스가 나타나더라도 이번 cpu burst가 완료될 때까지 cpu를 선점(preemptive )하지 않음
  - <u>Preemptive</u> 
    - cpu를 잡았더라도 더 짦은 cpu burst time을 가지는 새로운 프로세스가 도착하면 cpu를 빼앗김
    - 이 방법을 **Shortest-Remaining-Time-First(SRTF)**라고도 부른다. 
- **문제점**
  - Starvation
    - cpu burst time이 짧은 프로세스가 계속 등장한다면 long process가 실행되지 못한다. 
  - cpu 사용시간을 미리 알 수 없으므로 실제 시스템에서 SJF를 사용하기 어려움. cpu 사용시간을 추정하여 사용
    - 과거의 cpu burst time을 이용해서 추정(**exponential averaging**)

### Priority Scheduling

- 우선순위가 높은 순으로 작업을 처리하는 스케줄링 방법
  - 숫자(정수)로 우선순위를 나타내며, 주로 정수값이 작은 순으로 우선순위가 높게 설정한다.
- Two schemes
  - <u>Nonpreemptive</u>
  - <u>Preemptive</u>
- SJF도 일종의 priority scheduling이다. (우선순위 = cpu burst time)
- **문제점**
  - Starvation
    - 해결방법 : Aging : 시간이 지날수록 우선순위가 높도록 설정하는 방법

### Round Robin(RR)

- cpu를 줄 때 동일한 할당시간을 주고, 그 시간이 끝나면 timer interrupt에 의해 cpu를 빼앗기게 되고, ready queue의 맨 뒤에 가서 줄을 서게 된다. 그 다음 프로세스가 할당 시간만큼 cpu를 쓰고...
- n개의 프로세스가 ready queue에 있고 할당 시간이 q time unit일 경우 각 프로세는 최대 q time unit 단위로 cpu 시간의 1/n을 얻는다. 
  - 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않는다. (응답시간이 빠르다.) response time이 빨라진다.
  - cpu를 누가 빨리 쓸지 예측할 필요 없이 모든 프로세스가 cpu를 한번씩 사용할 수 있다.
- cpu를 길게 쓰는 프로세스는 기다리는 시간도 길어지고, cpu를 짧게 쓰는 프로세스는 기다리는 시간도 짧아지는 특징
- Perfomance(양 극단의 케이스)
  - q large => FCFS와 같아진다.
  - q small => context switch 오버헤드가 커진다. 

### Mulitlevel Queue

![best finisher: Operating System | Multilevel Queue Scheduling | Multilevel  Feedback Queue Scheduling](https://lh4.googleusercontent.com/proxy/lYxelQRhUPRflIM9oycgdw517LlY4B5v8lMNCQLEPiyKwi45u8i-v9o8WKTFEyChyUjSafPQHWwMm3chpsD6sUvuOCH2EZTo0pNDQiwbm25Kkqe98_wrdya-5jgkIqWv6O_6UQ=s0-d)



- Ready queue를 여러 개로 분할
  - foreground queue(interactive)
  - background queue(batch - no human interaction)
- 각 큐는 독립적인 스케줄링 알고리즘을 가진다.
  - Foreground - RR
  - Background - FCFS
- 큐에 대한 스케줄링이 필요
  - Fixed priority scheduling
  - Time slice

### Multilevel Feedback Queue

- 프로세스가 다른 큐로 이동

- Cpu burst가 짧은 프로세스를 우선순위를 더 많이 주고 긴 프로세스는 점점 다른 큐로 이동하면서 우선순위에서 밀려남. 

  ![Multilevel Feedback Queues | Download Scientific Diagram](https://www.researchgate.net/profile/Jyotirmay-Patel/publication/265184702/figure/fig1/AS:295890351869964@1447557165376/Multilevel-Feedback-Queues.png)

---

cpu가 여러 개 있는 경우의 스케줄링

### Multiple-Processor-Scheduling

- cpu가 여러 개인 경우 스케줄링은 더욱 복잡해짐
- Homogeneous processor 인 경우
- Load sharing
  - 일부 프로세서에 job이 몰리지 않도록 부하를 적절히 공유하는 메커니즘 필요
  - 별개의 큐를 두는 방법 vs 공동 큐를 사용하는 방법
- Symmetric Multiprocessing(SMP)
  - 모든 cpu가 대등하여 각 프로세서가 알아서 스케줄링 결정
- Asymmetric multiprocessing
  - 하나의 프로세서가 전체적인 시스템 데이터의 접근과 공유를 책임지고 나머지 프로세서는 거기에 따름

---

### Real-Time Scheduling

데드라인 안에 무조건 프로세스가 종료되어야 하는 스케줄링

- Hard real time systems
- Soft real time computing
  - 데드라인을 반드시 보장하기보다 다른 프로세스에 비해 우선순위를 주는.

### Thread Scheduling

- Local Scheduling
  - User level thread의 경우 사용자 수준의 thread library에 의해 어떤 thread를 스케줄할지 결정
- Global Scheduling
  - Kernel level thread의 경우 일반 프로세스와 마찬가지로 커널의 단기 스케줄러가 어떤 thread를 스케줄할지 결정



## Algorithm Evaluation

- Queing models
  -  확률분포로 주어지는 arrival rate와 service rate 등을 통해 각종 performance index값을 계산
- Implementation(구현) & Measurements(성능 측정)
  - 실제 시스템에 알고리즘을 구현하여 실제작업(workload)에 대해서 성능을 측정 비교
- Simulation(모의 실현)
  - 알고리즘을 모의프로그램으로 작성 후 trace를 입력으로 하여 결과 비교