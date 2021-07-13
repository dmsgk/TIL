# C++ 문법

## 입력

### 표준입력(cin)

c++에서 지원하는 기본자료형은 추출연산자(`>>`)사용해 `cin`에서 키보드 입력을 얻을 수 있음

```c++
#include <iostream> // C언어의 <stdio.h>격

using namespace std; // 표준 네임스페이스를 사용하겠다는 의미

int main(void){
    
    int num;
    cout << "숫자 입력 :"; // cout는 C의 printf와 동일하다.
    cin >> num; // cin은 C의 scanf와 동일하다.
    cout << num << endl; // endl은 C의 개행문자 출력과 동일하다.
    
    return 0;
}
```

`cin`에서는 공백을 추출할 값이 종료되는 것으로 인식. 



공백이 포함된 한 줄의 모든 값을 받으려면 `getline` 사용해야 함

```cpp
// cin with strings
#include <iostream>
#include <string>
using namespace std;

int main ()
{
  string mystr;
  cout << "What's your name?" << endl;
  getline (cin, mystr);
  cout << "Hello " << mystr << endl;

  return 0;
}
```





### cin, cout 최적화

아래와 같은 구문을 활용하면 cin와 cout의 속도를 향상시킬 수 있음

```cpp
ios::sync_with_stdio(0);  // c와 c++ 입출력의 synchronization을 false로 변경
cin.tie(0); 
cout.tie(0);  // cin과 cout의 tie 해제
```





### 1. 배열 입력받기

```cpp
#include <iostream>
using namespace std;

int main(void){
    
    char arr[10];
    cout << "문자 입력";
    cin >> arr; 
    cout << "내용 : " << arr;
    
    cout << strlen(arr) << endl; 
    cout << arr[0] << endl;
    
    return 0;
}
```

### 동적할당

`new` 와 `delete` 키워드를 사용해 동적할당과 해제가 가능함

```cpp
#include <iostream>
using namespace std;

int main() {
    int *p = new int[0];    // int형 변수 [0]
    
    for (int i = 0; i < 9; i++) {  // 9개 동적할당
        p[i] = i+1;
    }
    
    for (int i = 0; i < 9; i++) {
        cout << p[i] << endl;
    }
    
    delete[] p;  // 동적할당 해제
    return 0;
    
}
```





## 벡터

- 배열과 벡터는 원소에 직접 접근하여 탐색시간이 O(1) 이다. 

- 배열은 임의의 위치에 원소를 삽입하거나 할당된 메모리가 꽉 찼을 때 문제가 발생. -> 동적 배열을 사용해 문제 해결(리스트, 벡터)
- 벡터는 임의의 위치에 자료를 추가/삭제하는 경우 시간은 O(N)이지만 마지막 위치에 추가/삭제 및 탐색하는 시간은 O(1)로 빠르다.
- 그러므로 동적배열이 필요하고 자료의 삽입/삭제보다 탐색을 많이 할 경우 벡터를 사용할 것

### 벡터 선언

```cpp
#include <vector>
using namespace std;

// 벡터선언
vector<int>v;  // int형 자료를 저장하는 벡터v 생성
vector<int>v(3); // 0이 3개 저장된 벡터 v 생성.
vector<int>v(3, 8); // 8이 3개 저장된 벡터 v를 생성.
```



## for문

`for (초기식; 조건식; 변화식) {명령문}`



