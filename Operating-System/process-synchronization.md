# Chap 6. Process Synchronization

### OS 에서 race condition은 언제 발생하는가?

1. Kernel 수행 중 인터럽트 발생 시
2. Pocess가 system call을 하여 kernel mode로 수행 중인데 context switch가 일어나는 경우
   - 해결책: 커널모드에서 수행 중일 때는 cpu를 preempt하지 않음. 커널모드에서 사용자모드로 돌아갈 때 preempt
3. Multiprocessor에서 shared memory 내의 kernel data
   - 해결책1. 한 번에 하나의 cpu만이 커널에 들어갈 수 있게 하는 방법
   - 해결책2. 커널 내부에 있는 각 공유 데이터에 접근할 때마다 그 데이터에 대한 lock/unlock 방법



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

