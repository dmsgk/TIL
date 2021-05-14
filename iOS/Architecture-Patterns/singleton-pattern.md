# Singleton Pattern

### 주요 키워드

> `Singleton Pattern`, `Singleton의 활용`,  `[iOS] Cocoa Framework에서 사용되는 Singleton Pattern`, `[iOS] 예제`



## Singleton이란?

- Singleton은 **특정 클래스의 인스턴스가 하나임을 보장하는 객체**를 의미합니다. 

- 일반적으로 클래스에서 여러 개의 인스턴스를 생성할 수 있는데, Singleton에서는 어떤 클래스의 인스턴스가 **오로지 하나**임을 보장한다는 것이죠.

- Singleton Pattern에서는 생성자가 여러 차례 호출되더라도 실제로 생성되는 객체는 하나고 최초 생성 이후에 호출된 생성자는 최초에 생성한 객체를 반환합니다. 

  

## Singleton Pattern의 활용

- Singleton Pattern은 객체가 불필요하게 여러 개 만들어질 필요가 없는 경우에 사용할 수 있습니다. 
  
- Ex ) 데이터 관리, 네트워크 연결처리
  
- #### Singleton Pattern을 사용할 경우의 이점은 다음과 같습니다. 

  - Singleton pattern을 사용하면 한 클래스의 인스턴스가 한 개만 생성되므로, 메모리 공간을 효율적으로 사용할 수 있습니다.
  - 생성된 인스턴스가 전역 인스턴스이므로, 다른 인스턴스들과 데이터 공유가 쉽습니다.

- #### Singleton Pattern을 사용시 주의해야 할 점은 다음과 같습니다. 

  - 멀티 스레드 환경에서 <u>동시에</u> 싱글턴 객체를 참조할 경우 인스턴스가 여러 개 생성되는 문제가 발생할 수 있습니다. 



## [iOS] Cocoa Framework에서 사용되는 Singleton Pattern

싱글턴 인스턴스를 반환하는 팩토리 메서드나 프로퍼티는 일반적으로 `shared`라는 이름을 사용합니다.

- [FileManager](<https://developer.apple.com/documentation/foundation/filemanager>)
  - 애플리케이션 파일 시스템을 관리하는 클래스입니다.
  - `FileManager.default`
- [URLSession](<https://developer.apple.com/documentation/foundation/urlsession>)
  - URL 세션을 관리하는 클래스입니다.
  - `URLSession.shared`
- [NotificationCenter](<https://developer.apple.com/documentation/foundation/notificationcenter>)
  - 등록된 알림의 정보를 사용할 수 있게 해주는 클래스입니다.
  - `NotificationCenter.default`
- [UserDefaults](<https://developer.apple.com/documentation/foundation/userdefaults>)
  - Key-Value 형태로 간단한 데이터를 저장하고 관리할 수 있는 인터페이스를 제공하는 데이터베이스 클래스입니다.
  - `UserDefaults.standard`
- [UIApplication](<https://developer.apple.com/documentation/uikit/uiapplication>)
  - iOS에서 실행되는 중앙제어 애플리케이션 객체입니다.
  - `UIApplication.shared`



## [iOS] Singleton 예제 

 Singleton을 사용하는 간단한 예제를 들어보겠습니다. 

```swift
class MyClass {
  static let shared = MyClass()
  private init (){}
  
  var name: String?
  var id: String?
}
```



