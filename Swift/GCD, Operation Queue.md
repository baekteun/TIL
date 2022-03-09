
## 애플에서의 동기, 비동기 큐
- 쉽고 편리한 멀티 스레딩 처리를 위해 애플은 3가지의 API를 제공
- 첫번째로 GCD(Grand Central Dispatch)라는 C기반의 저수준 API
- 두번째로 NSOperation이라는 Objc 기반으로 만들어진 고수준 API
  - NSOperation은 GCD보다 약간의 오버헤드가 더 발생되고 느리지만 GCD에서 직접 처리해야 하는 작업들을 지원하기 때문에 (KVO관찰, 작업취소 등) 그 정도는 감수하고 NSOpration을 사용할만하다.
- 세번째로 Swift 5.5의 `async/await` API
- `async/await`은 순수 Swift로 작성되었다.

## GCD API
- **main queue** : 메인 스레드(UI Thread)에서 사용되는 Serial Queue로 모든 UI 처리는 메인 스레드에서 처리.
```swift
DispatchQueue.main.sync {...} // 대부분에서 사용 불가능 
DispatchQueue.main.async {...}
```
- **global queue** : Concurrent Queue이다.
```swift
DispatchQueue.global().sync {}
DispatchQueue.global(qos: .background).async {}
```
- **Custom Dispatch Queue** : Serial Queue, Concurrent Queue 정의 생성 가능. default는 Serial Queue
```swift
Dispatch Queue(label: "com.serialQueue").async {}
Dispatch Queue(label: "com.concurrentQueue",
              qos: .default,
              attributes: .concurrent,
              autoreleaseFrequency: .inherit,
              target: nil).async {}
```

## Operation Queue API
- GCD와 비교했을때는 추가적인 오버헤드가 있으나,
- 다양한 작업들 가운데 의존성을 추가할 수 있고, 재사용, 취소, 중지 시킬 수 있다.
- Operation을 일시 중지, 다시 시작 및 취소를 할 수 있다.
- KVO를 사용할 수 있는 많은 Properties가 있다.

`isCancelled, isAsynchronous, isExecuting, isFinished, isReady, dependencies, queuePriority, completionBlock`