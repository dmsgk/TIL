# LaunchScreen

## LaunchScreen AppDelegate에서 시간 지연시키기

초기 런치 스크린을 띄울 때 시간을 지연시켜야하는 경우가 있다. 그 경우 앱이 시작되는 부분에서 딜레이를 걸어주면 된다. AppDelegate에서 아래와 같은 함수에

```swift
// AppDelegate
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        return true
    }
```

 다음과 같은 내용을 추가해주면 된다. 이 경우 2.0은 2초를 의미한다. 

```
Thread.sleep(forTimeInterval: 2.0)
```



