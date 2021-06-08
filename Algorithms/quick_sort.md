# Quick Sort

## Quick Sort 개념

- 분할정복 알고리즘을 활용하여 리스트를 정렬한다. 
- **Quick Sort의 과정**
  1. 정렬 기준이 되는 pivot을 선택한다. (보통 랜덤으로 선택)
  2. 오른쪽(j)에서 왼쪽으로 가면서 피벗보다 작은 수 찾으면 멈춤
  3. 왼쪽(i)에서 오른쪽으로 가면서 피벗 이상인 수 찾으면 멈춤
  4. 각 인덱스 i, j에 대한 요소를 교환
  5. 2,3,4번 과정 반복 
  6. 이제 교환된 피벗 기준으로 왼쪽엔 피벗보다 작은 값, 오른쪽엔 큰 값들만 존재함
  7. 이와 같은 과정을 재귀로 반복하여 시행한다.

- 선택정렬과 마찬가지로 퀵소트도 동일한 값을 가질 경우 정렬 후 기존 순서가 유지되지 않는 **불안정정렬**이다. 

## 시간복잡도

- **O(n^2)** : **피벗 값이 최소나 최대값으로 지정되어 파티션이 나누어지지 않았을 때** 최악의 경우가 되어 O(n^2)에 대한 시간복잡도를 가짐
- **Θ(nlogn)**: 그러나 다수의 경우 평균복잡도는 nlogn 이기 때문에 효율적인 정렬 알고리즘이다. 
- cf ) 퀵소트의 경우 시간복잡도를 O(nlogn)라고 하기도 한다. 

### ⭐️Improved Quick Sort - O(n^2)의 시간복잡도를 개선하는 방법 

- **Median of Three QuickSort** : 맨 왼쪽, 중간, 맨 오른쪽 인덱스에 위치한 숫자들을 정렬하여 그중 중간값(Median)을 피벗으로 삼아 퀵소트
- **삽입정렬과 함께 사용** : 만약 arr의 size가 특정 수 (e.g. 200) 이하라면 삽입정렬, 그 것보다 크면 퀵정렬을 사용하여 정렬하는 것이 성능이 더욱 좋음. 가장 빠른 조합은 Median of Three와 삽입 정렬을 함께 사용하는 것
- **난수 분할** : Pivot이 항상 편향되는 최악의 경우를 막기 위해 Pivot값을 매번 Random한 위치에서 잡는 방법

## 공간복잡도

**O(n)**

## Python으로 구현하기

```python
import random

def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[random.randrange(0, len(arr))]
    lesser_arr, equal_arr, greater_arr = [], [], []
    for num in arr:
        if num < pivot:
            lesser_arr.append(num)
        elif num > pivot:
            greater_arr.append(num)
        else:
            equal_arr.append(num)
    return quick_sort(lesser_arr) + equal_arr + quick_sort(greater_arr)

print(quick_sort([3,5,8,1,2,9,4,7,6]))   # [1, 2, 3, 4, 5, 6, 7, 8, 9]

```







### References

- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/QuickSort.md
- https://gusdnd852.tistory.com/124