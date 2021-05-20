# Bubble Sort

## Bubble Sort 개념

- `서로 인접한 두 원소의 대소를 비교하고, 조건에 맞지 않다면 자리를 교환하며 정렬하는 알고리즘`
- **Ascending Order**
  - 첫 번째 수와 두 번째 수를 비교하여 정렬하고, 2번째와 3번째 비교정렬...계속하여 제일 큰 숫자를 확정짓고, 이를 반복하여 첫 번째 수까지 정렬되도록 한다.
- **Descending Order**
  - n-1과 n번째를 수를 비교하여 정렬하고 n-2번째 수와 n-1번째 수를 비교 정렬....계속하여 제일 작은 숫자를 확정짓고, 이를 반복하여 마지막 수까지 정렬되도록 한다. 



## 시간복잡도 

- **O(n^2)** 
  - 시간복잡도를 계산하면, `(n-1) + (n-2) + (n-3) + .... + 2 + 1 => n(n-1)/2`이므로
  -  Bubble Sort는 정렬이 돼있던 안돼있던, 2개의 원소를 비교하기 때문에 최선, 평균, 최악의 경우 모두 시간복잡도가 **O(n^2)** 으로 동일
    - => (개선된 Bubble Sort)



## 공간복잡도 : O(n)

주어진 배열 안에서 교환(swap)을 통해, 정렬이 수행되므로 **O(n)** 입니다.



## Python으로 구현하기

### Ascending Order

```python
# ascending order
def bubble_sort(li):
    i = len(li)-1
    while i > 0:
        idx = 0
        while idx < i:
            if li[idx] > li[idx+1]:
                f, b = li[idx], li[idx+1]
                li[idx], li[idx+1] = b,f
            idx += 1
        i -= 1
    return li

print(bubble_sort([2,9,5,3,1,8]))  # [1,2,3,5,8,9]
```

### Desceding Order

```python
# descending order
def bubble_sort(li):
    idx = 0
    while len(li)-1 > idx:
        i = len(li) - 1
        while i > 0:
            if li[i-1] > li[i]:
                f, b = li[i-1], li[i]
                li[i-1], li[i] = b, f
            i -= 1
        idx += 1
    return li

print(bubble_sort([2,9,5,3,1,8]))  # [1,2,3,5,8,9]
```

