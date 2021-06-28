# Sieve of Eratosthenes (에라토스테네스의 체)

## 개념

- ~~수학귀신에 나왔던 알고리즘~~

- 소수 찾는 알고리즘

![에라토스테네스의 체](https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif)

- 구체적 프로세스
  1. 2부터 소수를 구하고자 하는 구간의 모든 수를 나열한다. 그림에서 회색 사각형으로 두른 수들이 여기에 해당한다.
  2. 2는 소수이므로 오른쪽에 2를 쓴다. (빨간색)
  3. 자기 자신을 제외한 2의 배수를 모두 지운다.
  4. 남아있는 수 가운데 3은 소수이므로 오른쪽에 3을 쓴다. (초록색)
  5. 자기 자신을 제외한 3의 배수를 모두 지운다.
  6. 남아있는 수 가운데 5는 소수이므로 오른쪽에 5를 쓴다. (파란색)
  7. 자기 자신을 제외한 5의 배수를 모두 지운다.
  8. 남아있는 수 가운데 7은 소수이므로 오른쪽에 7을 쓴다. (노란색)
  9. 자기 자신을 제외한 7의 배수를 모두 지운다.
  10. 위의 과정을 반복하면 구하는 구간의 모든 소수가 남는다.
- 그림의 경우, ![{\displaystyle 11^{2}>120}](https://wikimedia.org/api/rest_v1/media/math/render/svg/542ed9781025d9b298c52a42b63958fdf35dc985)이므로 **11보다 작은 수의 배수들만 지워도 충분하다.** 즉, 120보다 작거나 같은 수 가운데 2, 3, 5, 7의 배수를 지우고 남는 수는 모두 소수이다.



## 시간복잡도

- O(Nlog(logN)) 

- 가장 빠르고 정확하게 소수를 구할 수 있는 방법



## Python3으로 구현하기

```python
# 에라토스테네스의 체 구현하기 - n까지 숫자 중 소수 찾기
import math

def prime_num(n):
    num_set = {i for i in range(2,n+1)}
    num = math.ceil(math.sqrt(n))   # n의 제곱근보다 크거나 같은 정수까지 탐색할 것

    for i in range(2,num+1):
        j = 2
        while i*j <= n:
            num_set -= {i*j}
            j += 1
    return num_set

n = int(input())
print(prime_num(n))  # n= 120일때, [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103, 107, 109, 113] 출력
```



### References

- https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4

