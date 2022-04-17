
## 네트워크 상태 모니터링

iOS 12 이상부터는 `NWNetworkMonitor`라는 내부 라이브러리를 통해서 현재 인터넷 상태 변경에 대한 감지를 할 수 있도록 제공해준다.
> https://developer.apple.com/documentation/network/nwpathmonitor/

사용하기 위해선 클래스를 초기화해준다

```swift
import Network

let networkMonitor = NWPathMonitor()
```

<br>

모니터링을 시작하려면 

```swift
networkMonitor.start(queue: DispatchQueue.global())
```
를 시작해주면 그때부터 네트워크 변경 사항에 대한 체크를 시작한다.

<br>

변화된 네트워크 상태는
```swift
networkMonitor.start(queue: DispatchQueue.global())
.pathUpdateHandler = { path in }

```
로 변경사항에 대한 알림을 받을 수 있다.

<br>

모니터링을 그만둘 경우
```swift
networkMonitor.stop()
```


> https://magicmon.tistory.com/229