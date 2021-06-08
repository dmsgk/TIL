# Longest Increasing Sequence(LIS)

가장 긴 증가하는 부분 수열의 길이를 구하는 알고리즘

[ 7, **2**, **3**, 8, **4**, **5** ] → 해당 배열에서는 [2,3,4,5]가 LIS로 답은 4



### 구현방법

- DP : O(n^2)

- Lower Bound: O(nlogn)

  N^2으로 해결할 수 없는 문제일 경우 (ex. 배열의 길이가 최대 10만일 때..) Lower Bound를 활용한 LIS 구현을 진행해야

  

### References

- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/LIS%20(Longest%20Increasing%20Sequence).md