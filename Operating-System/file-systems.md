## Chap 10. File Systems

## File and File System

- **File**

  - "A named collection of related information"

     관련정보를 이름을 가지고 저장하는 정보

  - 일반적으로는 비휘발성의 보조기억장치에 저장

  - 운영체제는 다양한 저장장치를 file이라는 동일한 논리적 단위로 볼 수 있게 해 줌

  - Operation

    - create, read, write, reposition(lseek), delete, open, close 등

- **File attribute**(혹은 파일의 **metadata**)

  - 파일 자체의 내용이 아니라 파일을 관리하기 위한 각종 정보들
    - 파일이름, 유형, 저장된 위치, 파일 사이즈
    - 접근권한(읽기/쓰기/실행), 시간(생성/변경/사용), 소유자 등

- **File system**

  - 운영체제에서 파일을 관리하는 부분
  - 파일 및 파일의 메타데이터, 디렉토리 정보 등을 관리
  - 파일의 저장방법 결정
  - 파일 보호 등



## Directory and Logical Disk

- **Directory**
  - 파일의 메타데이터 중 일부를 보관하고 있는 일종의 특별한 파일
  - 그 디렉토리에 속한 파일 이름 및 파일 attribute들
  - operation
    - Search for a file, create a file, delete a file
    - List a directory, rename a file, traverse the file system
- **Partition(= Logical Disk)**
  - 하나의 (물리적) 디스크 안에 여러 파티션을 두는 것이 일반적
  - 여러 개의 물리적 디스크를 하나의 파티션으로 구성하기도 함
  - (물리적) 디스크를 파티션으로 구성한 뒤 각각의 파티션에 file system을 깔거나 swapping 등 다른 용도로 사용할 수 있음



## open()

- Open("/a/b/c")

  - 디스크로부터 파일c의 메타데이터를 메모리로 가지고 옴
  - 이를 위하여 directory path를 search
    - 루트 디렉토리 "/"를 open하고 그 안에서 파일 "a"의 위치 획득
    - 파일 "a"를 open 한 후 read하여 그 안에서 파일 "b"의 위치 획득
    - 파일 "b"를 open한 후 read하여 그 안에서 파일 "c"의 위치 획득
    - 파일 "c"를 open한다
  - Directory path의 search에 너무 많은 시간 소요
    - open을 read/write와 별도로 두는 이유임
    - 한번 open한 파일은 read/write 시 directory search가 불필요
  - Open file table
    - 현재 open된 파일들의 메타데이터 보관소(in memory)
    - 디스크의 메타데이터보다 몇 가지 정보가 추가
      - Open 한 프로세스의 수
      - File offset: 파일 어느위치 접근중인지 표시(별도테이블 필요)
    - File desciptor( file handle, file control block)
      - Open file table에 대한 위치정보(프로세스별)

<img width="502" alt="스크린샷 2021-05-06 오전 11 50 35" src="https://user-images.githubusercontent.com/72622744/117247289-f4205400-ae78-11eb-8ebc-71be11794ec0.png">





## File Protection

- 각 파일에 대해 누구에게 어떤 유형의 접근(read/write/execution)을 허락할 것인가?

- Access Control 방법

  - **Access control Matrix**

    <img width="402" alt="스크린샷 2021-05-06 오전 11 54 06" src="https://user-images.githubusercontent.com/72622744/117247346-0bf7d800-ae79-11eb-8c0e-6292ef03b24a.png">


    - 그러나 행렬 방식으로 하면 희소행렬이 되어 메모리가 낭비되므로 linked list로 아래와 같이 두 가지로 access control하는 방법을 생각할 수 있다.
    - Access control list: 파일별로, 누구에게 어떤 접근권한이 있는지 표시
    - Capability: 사용자별로, 자신이 접근권한을 가진 파일 및 해당 권한 표시
    - 그러나 여전히 오버헤드가 크다...

  - **Grouping**

    - 전체 user를 owner, group, public의 세 그룹으로 구분
    - 각 파일에 대해 세 그룹의 접근권한(rwx)을 3비트씩 표시
    - 예) UNIX

  - **Password**

    - 파일마다 password를 두는 방법(디렉토리 파일에 두는 방법도 가능)
    - 모든 접근 권한에 대해 하나의 password: all or nothing
    - 접근권한별  password: 암기문제, 관리 문제



## File System의 Mounting

다른 partition에 있는 root file system에 접근해야 한다면?

<img width="508" alt="스크린샷 2021-05-06 오후 12 02 38" src="https://user-images.githubusercontent.com/72622744/117247603-86c0f300-ae79-11eb-8085-abcc8219e8f8.png">
샷 2021-05-06 오후 12.02.38.png)



## Access Methods

- 시스템이 제공하는 파일정보의 접근 방식
  - **순차접근(sequential access)**
    - 카세트테이프를 사용하는 방식처럼 접근
    - 읽거나 쓰면 offset은 자동적으로 증가
  - **직접 접근(direct access, random access)**
    - LP 레코드 판과 같이 접근하도록 함
    - 파일을 구성하는 레코드를 임의의 순서로 접근할 수 있음

