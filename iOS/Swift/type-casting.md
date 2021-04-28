# Type Casting

- 스위프트의 경우 다른 언어의 타입변환 또는 타입캐스팅이 이니셜라이져로 가능하다. 

- 그 대신 스위프트의 타입캐스팅은 인스턴스의 타입을 확인하거나 자신을 다른 타입의 인스턴스인양 행세할 수 있게 한다.

- 타입캐스팅은 실제로 인스턴스를 수정하거나 값을 변경하는 작업은 아님

### 1. 데이터타입 확인

- 타입연산자 `is`를 사용하여 인스턴스가 어떤 클래스의 인스턴스인지 타입확인 가능
  - 인스턴스가 해당 클래스의 인스턴스거나 그 자식클래스의 인스턴스라면 true 반환
  - 그렇지 않다면 false 반환

- Meta Type 타입을 이용

### 2. 다운캐스팅

- 자식클래스보다 더 상위에 있는 부모클래스의 타입을 자식클래스의 타입으로 캐스팅하는 것

- 타입캐스트 연산자: `as?`,  `as!`

  - `as?` 연산자는 다운캐스팅이 실패시 nil 반환
  - `as!` 연산자는 다운캐스팅이 실패시 런타임 에러

  ```swift
  var mike: Person = UniversityStudent() as Person
  var yagom: Person = Person()
  var hana: Student = Student()
  var jason: UniversityStudent = UniversityStudent()
  
  var optionalCasted: Student?
  
  optionalCasted = mike as? UniversityStudent
  optionalCasted = jenny as? UniversityStudent // nil
  optionalCasted = jina as? UniversityStudent // nil
  optionalCasted = jina as? Student // nil
  ```

  

### 3. Any, AnyObject의 타입캐스팅

-  `Any`,  `Anyobject` - 특정 타입을 지정하지 않고 여러 타입의 값을 할당할 수 있는 타입
  - `Anyobject`는 클래스의 인스턴스만 취할 수 있음
  - `Any`는 함수, 구조체, 클래스, 열거형 등 모든 타입의 인스턴스를 취할 수 있음





### References

- 야곰, 2019, 스위프트 프로그래밍, 3판, 한빛미디어.