# Swift Composable Architecture (SCA)

## 알아보게 된 이유?
SwiftUI와 Combine을 사용하는 아키텍쳐들을 찾아보다 발견하였다.

## Composable Architecture?
- State Management: 앱 상태를 간단한 값 유형을 사용해 관리하여 여러 화면에서 상태를 공유해 즉시 변화를 줄 수 있음.
- Composition: 큰 기능을 분리하여 자체 모듈로 추출해 작은 구성요소로 나누거나 붙여 기능을 합성할 수도 있음.
- Testing: 전체 및 부분으로 구성된 기능에 대해 통합 및 부분적 테스트 작성이 가능.
- Side Effects: 앱의 특정 부분이 테스트 가능하고 이해하기 쉬운 방식으로 외부와 대화하도록 하는 방법.
- Ergonomics: 위의 모든 것을 가능한 한 적은 개념과 움직이는 부분으로 간단한 API에서 수행하는 방법.

## Swift Composable Architecutre란?
- Point-Free에서 구현된 상태 관리 기반 아키텍쳐
- Elm, Redux 등에서 영감을 받았으며 모든 Apple Platform에서 사용가능(SwiftUI, UIKit 등)
- SwiftUI 프레임워크 선언형 형태에 적합한 뷰 업데이트 방식에 맞는 아키텍쳐 
- 뷰의 변화를 크고 작은 기능을 붙여 작은 도메인으로 나누어 보여줄 수 있음
- Combine 프레임워크에 의존하기에 iOS 13.0, macOS 10.15, Mac Catalyst 13.0, tvOS 13.0, watchOS 6.0 이상에서 가능

> https://github.com/pointfreeco/swift-composable-architecture

## Swift Composable Architecture의 기본 구성
일반적으로 Swift Composable Architecture, 줄여서 SCA라 부른다.
SCA를 사용하여 기능 구성 및 도메인 모델링을 한다.

- State: 기능이 로직을 수행하고 UI를 렌더링 하기 위해 필요한 데이터 타입.
- Action: 사용자 작업, 알림, 이벤트 소스 등 기능에서 발생할 수 있는 모든 작업을 나타내는 타입.
- Environment: 기능에서 API Client, 분석 Client와 같이 Side Effects를 동반하는 모든 Dependency를 보유하는 타입.
- Reducer: 액션에서 상태 업데이트를 해주는 로직 함수로 모든 결과가 Effect타입으로 반환.
- Store: 실제로 기능을 구동하는 런타임으로 Store와 Reducer가 Effect를 실행하도록 사용자의 액션을 Store에 보내고 Store에서 상태를 관찰하여 UI를 업데이트.

## SCA의 데이터 흐름
![image](https://cdn.discordapp.com/attachments/814148170711695411/934970911508004975/unknown.png)


1. View 정의
2. Store를 사용하여 작업 전달 : 액션으로 핸들러 및 작업 전달
3. Reducer에서 비지니스 로직 코드 처리
4. Side Effect 및 종속성 처리 : Effect 처리 및 Environment를 통해 주입
5. 상태 업데이트 : 자동으로 동기화하여 State에 따른 View 업데이트

## Pullback
SCA에서 제공하는 pullback Operator에서는 큰 Reducer를 작은 Reducer로 분해하는 중요한 작업을 한다.
Combine 연산자와 함계 사용하면 작은 도메인에서 작업하는 많은 Reducer를 정의한 후 다시 끌어와서 큰 도메인에서 동작하는 하나의 큰 Reducer로 결합할 수 있다.

## SCA의 장점
- 아키텍쳐의 룰이 있기 때문에 코드를 작성하거나 읽는 방식이 동일해져 커뮤니케이션 비용이 낮아진다.
- pullback Operator로 특정 단위에 한정된 도메인이 다른 도메인에 쉽게 연결될 수 있고 재사용될 수 있다.
- 작은 도메인에서 이벤트 트래킹이라 로깅에 신경쓰지 않아도 글로벌 도메인에서 higher-order reducer 적용으로 한 곳에서 처리할 수 있다.
- Reducer가 Pure하기 때문에 항상 동일한 결과를 보장하므로 unit test 작성이 쉬워진다.















