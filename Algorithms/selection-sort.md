# Selection Sort

## Selection Sort 개념

- **해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘**

- 최솟값을 선형탐색하여 0번째 수와 교환. 1번째부터 끝까지 중에서 최솟값 탐색 후 1번째 수와 교환....끝까지 반복

  

## 시간복잡도

#### O(n^2) 

데이터의 개수가 n개라고 했을 때,

- 첫 번째 회전에서의 비교횟수 : 1 ~ (n-1) => n-1

- 두 번째 회전에서의 비교횟수 : 2 ~ (n-1) => n-2

  ...

- `(n-1) + (n-2) + .... + 2 + 1 => n(n-1)/2`

최선, 평균, 최악의 경우 시간복잡도는 **O(n^2)** 으로 동일



## 공간복잡도

주어진 배열 안에서 교환(swap)을 통해, 정렬이 수행되므로 **O(n)** 



## 장단점

### 장점

- Bubble sort와 마찬가지로 알고리즘이 단순함.
- 정렬을 위한 비교 횟수는 많지만, Bubble Sort에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적
- Bubble Sort와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않음
  -  **제자리 정렬(in-place sorting)**

### 단점

- 시간복잡도가 O(n^2)으로, 비효율적
- **불안정 정렬(Unstable Sort)**
  - **정렬되지 않은 상태에서 같은 키값을 가진 원소의 순서가 정렬 후에도 유지되는지 여부**에 따라 안정정렬과 불안정정렬로 구분됨



## Python으로 구현하기

```python
def selection_sort(li):
    i = 0
    while i < len(li)-1:
        switch_num, switch_idx = li[i], i
        j = i+1
        while j < len(li):
            if switch_num > li[j]:
                switch_idx = j
                switch_num = li[j]
            j += 1
        start_num = li[i]
        li[i], li[switch_idx] = switch_num, start_num
        i += 1
    return li

print(selection_sort([2,9,5,3,1,8]))  # [1, 2, 3, 5, 8, 9]
```



### References

- https://github.com/GimunLee/tech-refrigerator/blob/master/Algorithm/%EC%84%A0%ED%83%9D%20%EC%A0%95%EB%A0%AC%20(Selection%20Sort).md#%EC%84%A0%ED%83%9D-%EC%A0%95%EB%A0%AC-selection-sort