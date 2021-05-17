# MVVM (Model-View-View Model)

![05](http://labs.brandi.co.kr///assets/2018/20180227/03.png)



## MVVM이란?

**❶ UI 로직과 비즈니스 로직을 분리하고, ❷ 리액티브한 UI 컨셉과 함께 협력하여 작동하는 디자인 패턴(아키텍쳐 패턴)** 

- ### Model - 앱 데이터

  - UI에 독립적이다. 
    - SwiftUI나 UIKit을 import하지 않는다. 
  - App이 하는 일에 대한 데이터와 로직을 캡슐화한다
  - Model이 변경되었을 때 ViewModel에 알린다. 

- ### View - 사용자에게 보이는 부분. 

  - MVC와 달리 MVVM에서는 ViewController를 View로 취급한다.
  - View는 ViewModel을 참조한다.(반대는 성립하지 않음)
  - View는 Model을 참조하지 않는다. (반대도 마찬가지)
  -  MVVM에서 뷰를 변경하고 뷰 입력을 뷰 모델에 전달하는 작업을 담당

- ### ViewModel - Model과 View를 잇는 중재자 역할

  - ViewModel은 View input으로부터 Model을 업데이트한다. 
  - ViewModel은 Model이 변경되면 View에 반영한다. (Model output으로부터 View를 업데이트한다.)
  - ViewModel은 **View에 직접적으로 이야기하지 않는다. 무언가 바뀌었다고 발표(publish)** 한다.
  - 모든 UI 컨트롤의 상태를 알려주는 프로퍼티들을 포함한다.



## MVC에 비한 MVVM의 장점

- View와 ViewModel 사이에 Binding(바인딩-연결고리)이 존재함
  - ViewModel은 Model에 변화를 주고, ViewModel을 업데이트하는데 이 바인딩으로 인해 View도 업데이트된다.
- ViewModel은 View에 대해 아무 것도 모르므로 테스트가 용이하다. 
  - Cf ) MVC에서 View Controller에서는 Controller가 View의 life cycle(라이프 사이클)에 관여하기 때문에 View와 Controller를 분리하기 어렵다. (**Massive View Controllers**) 앱을 테스트할 때, Model은 따로 분리되어 테스트를 할 수 있어도 View와 Controller는 강하게 연결되어 있기 때문에 각각 테스트하기 어려움
- ViewController가 간결해진다. 
  - 모든 UI로직이 ViewModel에 있으므로 MVC에 비해 ViewController가 가벼워진다. 
- ViewModel이 로직을 더 잘 나타낼 수 있다. 



## MVVM 사용하기

### Data Binding

MVVM에서는 View의 output과 ViewModel 간의 바인딩이 필요하다. 바인딩은 아래와 같은 방법으로 할 수 있다.

- **Key-Value Observing (KVO)**
- **Functional Reactive Programming (FRP)**: 이벤트와 데이터를 스트리밍하여 처리하는 패러다임.  `RxSwivt`와 `ReactiveSwift` 프레임워크를 활용하여 적용가능
- **Delegate**: 값이 바뀔 때 notification을 pass하도록.
- **Boxing**: 프로퍼티 옵저버를 사용하여 값이 변경되는지 확인



>  A general rule of thumb is to never import `UIKit` in your **view models**.



### References

- https://www.raywenderlich.com/6733535-ios-mvvm-tutorial-refactoring-from-mvc
- http://labs.brandi.co.kr/2018/02/21/kimjh.html
- https://lena-chamna.netlify.app/post/ios_design_pattern_mvvm/



