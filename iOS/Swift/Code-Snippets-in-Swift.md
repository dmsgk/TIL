# Code Snippets in Swift

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

