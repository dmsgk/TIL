# MVC(Model-View-Controller)

![https://cphinf.pstatic.net/mooc/20180102_176/1514820609255BQ1m8_PNG/67_0.png?type=w760](https://cphinf.pstatic.net/mooc/20180102_176/1514820609255BQ1m8_PNG/67_0.png?type=w760)

- iOS의 기본 아키텍쳐 패턴

- Model, View, Controller로 구성

  - ### Model Objects

    - 애플리케이션과 관련한 데이터를 캡슐화하고 데이터를 조작하기 위한 로직을 정의한다. 
      - 모델 객체를 생성하는 클래스는 Core Data technology를 사용하는 경우 `NSManageredObject` 클래스를 많이 사용
      - 값 타입의 모델이 필요한 경우 클래스 대신에 구조체를 활용하기도

  - ### View Objects

    - 앱 내에서 사용자가 볼 수 있는 객체
    - 뷰 객체의 주된 목적은 Model Object의 데이터를 보여주고 해당 데이터를 편집할 수 있도록 하는 것

  - ### Controller Objects

    - Controller 객체는 Model과 View를 연결하는 중개자 역할을 한다.
      - 뷰가 표시해야 하는 모델 객체에 access할 수 있는지 확인하고 뷰가 모델의 변경사항을 업데이트하도록 한다. 
    - 컨트롤러 객체는 애플리케이션의 설정 및 조정 작업을 수행할 수도 있으며, 다른 객체들의 생애주기(life cycle)를 관리하기도 한다.
    -  iOS 환경의 Cocoa Touch 프레임워크는 *coordinating controller*, *view controller*의 두 가지 기본 컨트롤러 유형을 제공

    ![img](https://cphinf.pstatic.net/mooc/20180102_77/1514820625391eR7Yt_PNG/67_2.png?type=w760)





### References

- https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/Model-View-Controller/Model-View-Controller.html
- https://www.boostcourse.org/mo326/lecture/16877?isDesc=false