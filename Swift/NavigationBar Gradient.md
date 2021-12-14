# NavigationBar Gradient

### 네비게이션 바에 Gradient효과 적용하는 방법


아래 코드를 UINavigationController 에 extension해서 함수를 만들어 준다.

```swift
func configGradientBar(_ colors: [UIColor], locations: [NSNumber]){
        let gradient = CAGradientLayer()
        // 크기를 정해줌
        gradient.frame = navigationBar.bounds
        
        // 들어갈 색깔
        gradient.colors = [
            colors
        ]

        // 시작지점, 끝지점 
        gradient.startPoint = CGPoint(x: 1.0, y: 0.0)
        gradient.endPoint = CGPoint(x: 0.0, y: 0.0)

        // 위치
        gradient.locations = locations
        
        // 그라데이션 UIImage를 background로 지정.
        // * iOS 15.0 기준
        if let image = getImageFrom(gradientLayer: gradient) {
            let appearance = UINavigationBarAppearance()
            appearance.configureWithTransparentBackground()
            appearance.backgroundImage = image
            navigationBar.standardAppearance = appearance
            navigationBar.scrollEdgeAppearance = navigationBar.standardAppearance
            
        }
    }
    
    // 그라데이션 UIImage
    private func getImageFrom(gradientLayer: CAGradientLayer) -> UIImage? {
        var gradientImage:UIImage?
        UIGraphicsBeginImageContext(gradientLayer.frame.size)
        if let context = UIGraphicsGetCurrentContext() {
            gradientLayer.render(in: context)
            gradientImage = UIGraphicsGetImageFromCurrentImageContext()?.resizableImage(withCapInsets: UIEdgeInsets.zero, resizingMode: .stretch)
        }
        UIGraphicsEndImageContext()
        
        return gradientImage
    }

```

### 사용 
```swift
self.navigationController?.configGradientBar()
```