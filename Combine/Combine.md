# Combine
비동기 이벤트들을 결합된 이벤트 처리 연산자를 통해 핸들링하는 것

지원 버전
- iOS 13.0+
- iPadOS 13.0+
- macOS 10.15+
- Mac Catalyst 13.0+
- tvOS 13.0+
- watchOS 6.0+

# 개요
Combine 프레임워크는 시간에 따른 값 처리 위한 선언적 Swift API를 제공한다. 이 값들은 많은 종류의 비동기 이벤트를 나타낸다.
Combine은 시간이 지남에 따라 변경될 수 있는 값을 노출하는 _publishers_ 를 선언하고, _subsribers_ 를 선언해 publishers로부터 값울 받는다.

- `Publisher` 프로토콜은 시간에 따른 값의 흐름을 전달할 수 있는 타입을 선언하는 프로토콜이다. Publisher는 상류 publishers에게 받은 값에 따라 행동하고 다시 게시할 수 있는 _operators_ 를 가지고 있다.
- publishers 체인의 끝에서, subscriber는 요소를 받을 때 행동한다. `Publisher`는 오직 subscribers에게 명시적으로 요청받을 때만 값을 내보낸다. 이렇게 당신의 subsriber 코드는 연결된 publishers로부터 이벤트를 전달하는 속도를 제어할 수 있다.


Timer, NotificationCenter, URLSession을 비롯한 여러 Foundation 타입은 publishers를 통해 기능을 노출한다. Combine은 또한 Key-Value Observing을 준수하는 property에 대한 내장 publisher를 제공한다.

여러 publishers의 출력을 결합하고 상호작용을 조정할 수 있습니다. 예를 들어, 텍스트필드의 publisher를 구독하여 URL 요청을 수행할 수 있습니다. 그런다음 publisher를 사용하여 응답을 처리하고 해당 응답을 사용하여 앱을 업데이트할 수 있다.

Combine을 채택하면 이벤트 처리 코드를 중앙 집중화하고 중첩된 클로져 및 컨벤션 기반 콜백과 같은 성가신 기술을 제거하여 코드를 더 쉽게 읽고 유지할 수 있습니다.