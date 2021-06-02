# Optional Binding

> 주요 내용: Optional Unwrapping, Forced Unwrapping, Optional Binding



## Optional Binding

- Optional Unwrapping (옵셔널 추출)의 방식 중 하나

  > Optional Unwrapping : 옵셔널의 값을 옵셔널이 아닌 값으로 추출하는 방법
  >
  > Swift에서는 아래 두 가지 방식을 사용함
  >
  > \- 강제추출방식 (런타임 에러 가능성이 있기 때문에 지양하는 것이 좋음)
  >
  > \- 옵셔널 바인딩

- 옵셔널에 값이 있는지 확인할 때 사용

  - 옵셔널에 값이 있다면 옵셔널에서 추출한 값을 일정 블록 안에서 사용할 수 있는 상수나 변수로 할당해서 옵셔널이 아닌 형태로 사용할 수 있도록 해준다. 

- 예제코드

  ```Swift
  var myName : String? = "dsadjfkjls"
  
  // 옵셔널 바인딩을 통한 임시 상수 할당
  if let name = myName {
    print("My name is \(name)")
  } else {
    print("myName == nil")
  }
  // My name is dsadjfkjls
  
  
  // 옵셔널 바인딩을 통한 임시 변수 할당
  if var name = myName {
    name = "kldsajf"  // 변수이므로 내부에서 변경 가능
    print("My name is \(name)")
  } else {
    print("myName == nil")
  }
  // My name is kldsajf
  
  ```

  if 구문을 실행하는 블록 안쪽에서만 name이라는 임시 상수, 변수로 사용할 수 있음



## `if let` 구문과 `guard let` 구문

- 조건을 가지고 분기해서 처리하려면 if let을 사용
- 요구사항만을 반영해 예외상황을 처리하려면 gaurd let을 사용하면 좀 더 간결한 코드가 될 수 있음



