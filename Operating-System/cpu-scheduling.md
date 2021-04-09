# Chap 5. CPU Scheduling

## CPU Scheduling의 필요성 - cpu burst time의 분포

- Cpu-burst-time을 볼 때 cpu burst가 짧은, 즉 중간에 I/O가 많이 끼어드는**(I/O bound job**) 빈도가 매우 높았으며 cpu burst가 아주 긴(**cpu bound job**) 프로세스의 빈도가 낮았다.
  - 참고 - 프로세스의 특성 분류	
    - I/O bound process
      - cpu를 잡고 계산하는 시간보다 I/O에 많은 시간이 필요한 job (many short CPU bursts)
    - Cpu bound process
      - 계산 위주의 job (few very long CPU bursts)



- 여러 종류의 job(=process) 가 섞여 있기 때문에 cpu 스케줄링이 필요함
  - Interactive job에게 적절한 response 제공 요망(cpu를 공평하게 주기보다 사람과 interaction을 하는 job에게 스케줄링을 하도록)
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

  위의 1, 4의 스케줄링은 **nonpreemptive(= 강제로 빼앗지 않고 자진 반납)**

  나머지는 **preemptive(= 강제로 빼앗음)**

  

