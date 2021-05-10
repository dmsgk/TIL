# Chap 11. File System Implementation

## Allocation of File Data in Disk

파일을 디스크에 저장하는 방식(이론적 내용)

- Contiguous Allocation
- Linked Allocation
- Indexed Allocation



### Contiguous Allocation

- 하나의 파일이 디스크 상 연속하여 저장되는 방식

![스크린샷 2021-05-10 오후 3.16.11](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-10 오후 3.16.11.png)

- 단점

  - 외부조각이 생길 수 있다.
  - File grow가 어려움
    - 뒤에 빈 블록의 개수가 제한적인 경우 파일 크기를 키우는데 있어 한계가 있다.
    - File 생성시 얼마나 큰 hole을 할당할 것인가?
    - grow 가능 vs 낭비(내부조각 internal framgmentation 발생)

- 장점

  - Fast I/O
    - 한 번의 seek/rotation 으로 많은 바이트 transfer
    - Realtime file용으로, 또는 이미 run 중이던 process의 swapping용
  - Direct access(=random access) 가능

  

### Linked Allocation

- file data를 디스크에 연속적으로 저장하지 않고 빈 위치면 아무데나 들어갈 수 있도록 하는 방식

![스크린샷 2021-05-10 오후 3.27.55](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-10 오후 3.27.55.png)

- file의 시작위치만 directory가 가지고 있고 가면서 다음위치는 알게 되고 끝날 경우 끝났다고 표시
- 장점
  - 외부조각이 발생하지 않는다. (빈곳이면 어디든 들어가도 되므로)
- 단점
  - 직접탐색이 불가능하다(No Random Access)
  - Reliability 문제
    - 한 sector가 고장나 pointer가 유실되면 많은 부분을 잃음
  - **Pointer를 위한 공간이 block의 일부가 되어 공간효율성을 떨어뜨림**
    - 512 bytes/sector, **4 bytes/pointer**
- 변형
  - File-allocation table(FAT) 파일 시스템
    - 포인터를 별도의 위치에 보관하여 reliability와 공간효율성 문제 해결



### Indexed Allocation

- 직접접근이 가능하게 하기 위해 directory에 index block에 모든 위치를 저장해놓음

![스크린샷 2021-05-10 오후 3.36.21](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-10 오후 3.36.21.png)

- 장점
  - 외부조각이 생기지 않음
  - 직접접근 가능
- 단점
  - Small file의 경우 공간낭비 (실제로 많은 file들이 small)
  - Too Large File의 경우 하나의 block으로 index를 저장하기에 부족
    - 해결방안
      1. Linked scheme
      2. Muliti-level-index



## UNIX 파일시스템의 구조

![스크린샷 2021-05-10 오후 3.43.25](/Users/johyeonyoon/Library/Application Support/typora-user-images/스크린샷 2021-05-10 오후 3.43.25.png)

- 유닉스 파일 시스템의 중요 개념
  - Boot block
    - 부팅에 필요한 정보(bootstrap loader)
  - Super block
    - 파일시스템에 관한 총체적인 정보를 담고 있다(어디가 빈 블록이고 어디가 실제로 사용중인 블록인지, 어디까지가 inode list이고  등)
  - Inode list
    - 파일 이름을 제외한 파일의 모든 메타데이터를 저장
  - Data block
    - 파일의 실제 내용을 보관

