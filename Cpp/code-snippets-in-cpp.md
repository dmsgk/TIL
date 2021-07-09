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

