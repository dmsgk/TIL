# Code Snippets in Swift

## String

### 문자열 쪼개기 

#### `components(separatedBy: "원하는문자")`

- 예제

```swift
let str = "[00:16:200]we wish you a merry christmas\n[00:18:300]we wish you a merry christmas\n[00:21:100]we wish you a merry christmas\n[00:23:600]and a happy new year"
let arr = str.components(separatedBy: "\n") // ["[00:16:200]we wish you a merry christmas", "[00:18:300]we wish you a merry christmas", "[00:21:100]we wish you a merry christmas", "[00:23:600]and a happy new year"]

// seperatedBy: 에 대괄호`[ ]`를 넣어 그 안에 넣은 하여 여러 문자를 기준으로 쪼갤 수 있음
let arr2 = str.components(seperatedBy:["\n", "]"] )
// ["[00:16:200", "we wish you a merry christmas", "[00:18:300", "we wish you a merry christmas", "[00:21:100", "we wish you a merry christmas", "[00:23:600", "and a happy new year"]

```



## [Resize UIImage]

\-  작성일 210601

```swift
extension UIImage {
   func resizedImage(newWidth: CGFloat) -> UIImage {
       guard size.width > newWidth else { return self }
       let scale = newWidth / self.size.width
       let newHeight = self.size.height * scale
       let newSize = CGSize(width: newWidth, height: newHeight)
       let renderer = UIGraphicsImageRenderer(size: newSize)
       let image = renderer.image { (context) in
           self.draw(in: CGRect(origin: CGPoint(x: 0, y: 0), size: newSize))
       }
       return image
   }
}
```

