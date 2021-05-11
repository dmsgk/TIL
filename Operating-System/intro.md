# Chap 1. Intro

## 운영체제란?

컴퓨터 하드웨어 바로 위에 설치되어 사용자 및 다른 소프트웨어와 하드웨어를 연결하는 소프트웨어 계층

![os_info_1](/Users/johyeonyoon/Library/Application Support/typora-user-images/os_info_1.png)

- 협의의 운영체제(커널) : 운영체제의 핵심 부분으로 메모리에 상주하는 부분

- 광의의 운영체제: 커널 뿐 아니라 각종 주변 시스템 유틸리티를 포함한 개념

  

### 운영체제의 목표

- 컴퓨터시스템을 편리하게 사용할 수 있는 기능을 제공
- 컴퓨터의 **자원을 효율적으로 관리**(프로세서, 기억장치, 입출력 장치 등의 효율적 관리)



### 운영체제의 분류

#### 동시 작업 가능 여부

- 단일 작업(single tasking)
- 다중작업(multi tasking)

#### 사용자의 수

컴퓨터 한 대를 여러 사용자가 동시에 접속하여 사용할 수 있는지 여부

- 단일 사용자

  ex) Ms-dos, ms windows

- 다중 사용자

  ex) Unix, nt server

#### 처리 방식

- 일괄 처리(batch processing)
  - 작업 요청의 일정량 모아서 한꺼번에 처리
- 시분할(time sharing) 
  -  우리가 사용하는 컴퓨터 그 자체를 생각하면 된다
  -  여러 작업을 수행할 때 컴퓨터 처리능력을 일정 시간단위로 분할하여 사용하기 때문에 일괄처리시스템에 비해 짧은 응답시간을 가짐
- 실시간(Realtime OS)
  - 정해진 시간 안에 어떠한 일이 반드시 종료됨이 보장되어야 하는 실시간 시스템을 위한 OS
  - Ex) 원자로/공장 제어, 미사일 제어, 반도체 장비
  - 최근 실시간 시스템의 개념이 **확장**
    - Hard realtime system
    - **Soft realtime system**(영화를 보거나 하는 등의 데드라인이 있는 경우 사용할 수 있음)

### 몇 가지 용어

아래의 용어는 컴퓨터에서 여러 작업을 동시에 수행하는 것을 의미한다. 

- Multitasking
- Multiprogramming 
- Time sharing
- Multiprocess

Multiprogramming은 여러 프로그램이 메모리에 올라가 있음을 강조, Time sharing은 CPU의 시간을 분할하여 나누어 쓴다는 의미를 강조

- Multiprocessor: 하나의 컴퓨터에 cpu가 여러 개 붙어 있음을 의미

