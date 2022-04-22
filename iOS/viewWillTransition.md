## viewWillTransition
- view의 frame 변화를 감지하는 UIViewController의 콜백.
- 디바이스가 회전될 때, iPad에서 Split View를 쓸 때를 감지할 때 등에 쓸 수 있다.
  
```swift
override func viewWillTransition(to size: CGSize, with coordinator: UIViewControllerTransitionCoordinator) {
	
}
```
- size는 변화 후의 size이다.

```swift
override func viewWillTransition(to size: CGSize, with coordinator: UIViewControllerTransitionCoordinator) {
    // will code
    coordinator.animate(alongsideTransition: nil) { _ in
        // did code
    }
}
```
- didTransition을 쓰기 위해서는 위 처럼 하면 된다.
