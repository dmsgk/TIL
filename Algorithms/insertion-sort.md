# Insertion Sort 

## Insertion Sort(삽입정렬) 개념

- 삽입정렬의 과정

  왼쪽 끝의 숫자를 정렬이 끝났다고 간주한 후 시작.

  1. 정렬은 2번째 위치의 값을 temp에 저장
  2. temp와 이전에 있는 원소들과 비교하며 삽입해나갑니다.
  3. 1번으로 돌아가 다음 위치(index)의 값을 temp에 저장하고, 반복

  

## 시간복잡도

- **최선의 경우 O(N)**이라는 엄청나게 빠른 효율성을 가지고 있음
- 최악의 경우,  `(n-1) + (n-2) + .... + 2 + 1 => n(n-1)/2` , **O(n^2)**의 시간복잡도
- 평균의 경우도 **O(n^2)** 의 시간복잡도



## 공간복잡도

**O(N)**



## Python으로 구현하기

```python
def insertion_sort(li):
    i = 1
    while i < len(li):
        temp = li[i]
        prev = i - 1
        while prev>=0 and li[prev]>temp:
            li[prev+1] = li[prev]
            prev -= 1
        li[prev+1] = temp
        i += 1

    return li

print(insertion_sort([2,9,5,3,1,8]))  # [1,2,3,5,8,9]
```





### References

- https://github.com/GimunLee/tech-refrigerator/blob/master/Algorithm/%EC%82%BD%EC%9E%85%20%EC%A0%95%EB%A0%AC%20(Insertion%20Sort).md#%EC%82%BD%EC%9E%85-%EC%A0%95%EB%A0%AC-insertion-sort