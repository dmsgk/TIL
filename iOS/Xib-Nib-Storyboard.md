# Xib, Nib, and Storyboard

> 주요내용: Xib, Nib, Storyboard 개념, Nib 로딩하기

## Xib, Nib, and Storyboard 개념

### Nib

\- Nextstep Interface Builder의 약자로, 화면을 구성하는 클래스들을 **바이너리 형태**의 압축 파일로 저장

### XIB

\- Xcode Interface Builder의 약자로, 화면을 구성하는 클래스들을 XML문법에 맞춰 저장

**XIB파일은 왜 생기게 되었나요?**

- 바이너리로 저장하지 않고 XML 형태로 저장하기 때문에 수정된 부분을 알 수 있어서 파일 관리가 아닌 소스코드로 관리가 가능해짐

- 직접 수정하려면 XML문법을 맞춰서 수정해야되기 때문에 번거로울 수 있지만, Xcode에선 Interface Builder를 제공하여 XML 형태가 아닌 그래픽 형태로 수정할 수 있게 도와줌

**프로그램이 뷰 정보를 읽어들이는 방법**

- 뷰 정보를 담고 있는 XIB파일을 빌드하게 되면, 접근하기 쉬운 바이너리 NIB파일로 컴파일 되고, 앱의 번들(앱 실행에 사용되는 파일이 저장된 폴더)로 복사된 후 실행파일에서 사용된다.



![img](https://t1.daumcdn.net/cfile/tistory/995555465B51C73B30)

###  Storyboard

- 스토리 보드는 뷰 정보와 뷰와 뷰 사이의 관계에 대한 정보를 가지고 있는 파일
- 뷰 정보인 XIB의 내용과 뷰 관계정보를 포함하고 있어서 XML로 이뤄져 있음
- 빌드를 하게 되면 컴파일된 storyboard파일로 **.storyboardc**라는 파일이 생성
  - .storyboardc 파일은 패키지 파일로 되어있고 이 내부는 nib파일과 nib파일을 관리하는 plist파일이 존재함

![img](https://t1.daumcdn.net/cfile/tistory/991E49495B51C5991B)

## Nib 로딩하기

### 1. Bundle 클래스의 `loadNibNamed` 사용

### 2. UINIb클래스 사용



### 성능적인 차이

> “A UINib object caches the contents of a nib file in memory, ready for unarchiving and instantiation. “
>
> UINib object는 메모리에 있는 nib 파일의내용을 캐시에 저장하고 있어서 보관하지 않고(unarchiving) 인스턴스 화할 준비가 되어있다

- `UINib` 클래스를 사용하는 방법은 하나의 nib 파일의 컨텐츠에 대해서 여러개의 복사본을 만들어야할때 성능적인 측면에서 더 효율적
- nib 파일을 로딩하는 프로세스는 파일 자체를 읽어오는 것 부터 시작하지만, `UINib` 인스턴스의 경우 **이미 읽어온 파일의 내용을 캐시하고 있기 때문에 디스크로 부터 파일을 읽어 들이는 오버헤드를 줄일 수 있음**





### References

- https://dalgonakit.tistory.com/82
- https://gaki2745.github.io/ios/2020/06/29/iOS-Basic-xib%EC%82%AC%EC%9A%A9%EB%B2%95/