## merge sort(병합정렬)

### 개념

- 분할정복을 통해 정렬
- 재귀호출을 통해 요소를 모두 쪼갠 후 차례로 병합하면서 정렬한다.
- 안정정렬

### 시간복잡도 및 공간복잡도

- 시간복잡도
  - 최선, 평균, 최악의 경우 모두 n log n
- 공간복잡도
  - 재귀를 통해 문제를 해결하므로 O(n)



### 파이썬으로 구현

```python
def merge_sort(left, right):
    global array
    if left < right:
        mid = (left+right)//2
        merge_sort(left, mid)
        merge_sort(mid+1, right)
        merge(left, mid, right)


def merge(left, mid, right):
    l_group, r_group = array[left: mid+1], array[mid+1: right+1]
    i, j, k = 0, 0, left
    ll, rl = len(l_group), len(r_group)

    while i < ll and j < rl:
        if l_group[i] <= r_group[j]:
            array[k] = l_group[i]
            i += 1
        else:
            array[k] = r_group[j]
            j += 1
        k += 1
    while i < ll:
        array[k] = l_group[i]
        k += 1
        i += 1

    while j < rl:
        array[k] = r_group[j]
        k += 1
        j += 1


array = [7,5,3,2,1,9,6,4]
merge_sort(0, len(array)-1)
print(array) # [1, 2, 3, 4, 5, 6, 7, 9]
```

