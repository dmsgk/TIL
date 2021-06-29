# Binary Search Algorithm

## Binary Search(이분 탐색)

- 시간복잡도 O(log n)
- 정렬된 배열에서 값을 찾아내는 검색 **알고리즘**
  - cf. 이진탐색트리(Binary Search Tree)는 정렬된 구조를 저장하고 탐색하는 **자료구조**

## 접근방법

### Presudo code

- 구하고자 하는 값(예를 들어 랜선의 최대 길이)이 가질 수 있는 최소값을 left, 최댓값을 right로 설정한다. 
- while문 (left <= right 일때)
  - `mid = (left + right)//2 ` 로 두고 mid로 연산하여 문제의 조건을 만족하는지 확인한다.
    - 조건값과 구한 수를 비교해
      -  left = mid + 1로, 또는 right = mid - 1로 변경
- 결과값을 출력한다. 

