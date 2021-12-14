# RxSwift

## Rx?
Rx : ReactiveX

> An API for asynchronous programming
with observable streams

> Observable한 스트림을 가지고 비동기 프로그래밍을 하기 위한 API

<br>
<br>

# Sync & Async

## 동기(Synchronous)
- 동기란 말 그대로 통신에서의 요청과 그에 대한 결과가 동시에 일어난다는 의미이다. 즉 요청을 하면 시간이 얼마가 걸리든 요청한 자리에서 결과가 주어져야 한다.
- 요청과 결과가 한 자리에서 일어난다.
- A 노드와 B 노드 사이의 작업 처리 단위를 동시에 맞춘다.
  
## 비동기(Asynchronous)
- 비동기는 동기의 반댓말고 요청과 결과가 동시에 일어나지 않는다는 것을 의미한다. 즉 요청의 결과값이 언제오던지 상관않고 내 갈 길 가겠다는 말이다.
- 요청한 그 자리에서 결과가 주어지지 않는다.
- 노드 사이의 작업 처리 단위를 동시에 맞추지 않아도 된다.

## 각각의 장단점
>동기 방식은 설계가 매우 간단하고 직관적이라는 장점을 갖는다. 하지만 결과가 주어질 때 까지 아무것도 못하고 대기해야 하기 때문에 리소스 낭비를 초래하는 단점이 았고, 비동기는 동기보다 복잡하지만 결과가 주어지는데 시간이 걸리더라도 잉여시간을 다른 작업에 투자하여 자원을 효율적으로 사용할 수 있다는 장점이 있다.
## RxSwift를 왜 쓰는가?
- 높은 가독성 -> Rx사용시 선언형 프로그래밍이 가능하기 때문에 / 유지보수성
- 비동기 처리 일원화
  - GCD, KVO, Delegate, NotificationCenter
- 압출력만 체크하면 되기 떄문에 UnitTest에 매우 용이.

## Observable
- RxSwift의 핵심적인 개념
- 이벤트를 시간 흐름에 따라 전달하는 전달자
- 비동기로 동작하는 항목들을 나타내는 시퀀스

Observable은 세 가지 타입의 이벤트를 배출하고 Observer가 Observable을 구독하여 이 이벤트를 받을 수 있다
<br>

- Next : next는 이름 그대로 다음 데이터를 가져온다. 가져온 데이터를 옵저버가 받는다.
- Completed : completed는 시퀀스를 정공적으로 마친다. 더이상 이벤트를 배출하지 않는다.
- Error : error는 오류가 발생하여 마친 경우이다. 이 또한 더이상 이벤트를 배출하지 않는다.

completed와 error이벤트는 observable 라이프 사이클 중 가장 마지막에 전달된다.

작동 방식은 Observer가 Observable을 구독하고, Observable이 이벤트를 배출하면 Observer가 이에 반응하는 방식이다.

## Dispose
observer는 기본적으로 completed또는 error이벤트가 발생할 떄 까지 구독을 유지한다. 그러나 사용자가 이를 직접 제어할 수 있다.

구독을 시작할 때는 subscribe()를 이용하였는데 해당 메소드는 구독 취소를 하기 위해 필요한 Disposable 객체를 반환.

이 Disposable 객체의 dispose()메소드를 사용하면 completed, error 이벤트 발생 이전에도 구독을 취소할 수 있다.

## 연산자
- just : just연산자는 하나의 인자만 수용할 수 있다.
- of : of연산자는 방출할 요소를 원하는 수 만큼 전달할 수 있다.
- from 배열 또는 시퀀스를 전달받고 배열에 포함된 요소들을 하나씩 순차적으로 방출한다.
- filter : 
  - 클로저를 파라미터로 받는다.
  - filter 내에서 True값을 반환하는 요소가 연산자가 리턴하는 observable에 포함된다
- combineLatest : source observable을 결합하여 result observable을 방출한다.
- map : map을 통해 전달받은 요소에 대하여 특정 연산 작업을 한 후 이를 변환하여 계속하여 진행한다.

## Subject
subject는 observer이면서 observable이다.

![async](http://reactivex.io/documentation/operators/images/S.AsyncSubject.png)
- AsyncSubjec
  - AsyncSubject는 소스 Observable로부터 배출된 마지막 값(만)을 배출하고 소스 Observalbe의 동작이 완료된 후에야 동작한다.
  
![Behavior](http://reactivex.io/documentation/operators/images/S.BehaviorSubject.png)
- BehaviorSubject
  - 기본값을 가지며 subscribe당시 데이터가 없을 경우 기본값을 방출한다.

![publish](http://reactivex.io/documentation/operators/images/S.PublishSubject.png)
- PublishSubject 
  - 기본값을 갖지 않으며 subscribe 당시 데이터가 없으면 아무것도 방출하지 않다가 데이터가 생기면 그때 방출한다.
  
![replay](http://reactivex.io/documentation/operators/images/S.ReplaySubject.png)
- ReplaySubject
  - 하나의 subscriber가 있을 경우에는 PublishSubject와 동일하다. 그러나 추가적인 subscriber가 생길 경우 기본의 데이터를 순차적으로 모두 보내준다