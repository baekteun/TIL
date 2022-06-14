# Publisher
- Publisher는 protocol이다.
- Publisher protocol은 시간에 따른 값의 흐름을 전달할 수 있다.
-  Subscription을 만들고 Subscriber에게 값과 completion을 내보내는 타입을 위한 protocol이다.
- Publisher는 값을 받아 처리하고 다시 전달하는 operators를 가진다.


## 미리 정의된 Publisher 구현체
- Just
- Future
- Deferred
- Empty
- Fail
- Record
- AnyPublisher

### Just (struct)
- 가장 단순한 형태의 Publisher이다.
- 자신을 subscribe하는 Subscriber들에게 한 번에 값을 내보낸 후 finish를 보내는 Publisher이다.
- Failure 타입은 항상 Never이다.

### Future (class)
- 하나의 결과를 비동기로 생성한 후 completion을 보내는 Publisher이다.
- 값을 내보낼 때 호출할 클로저를 매개변수로 받아서 그걸 값을 내보낼 때마다 계속 호출하는 Publisher이다.
- 클로저를 전달하는 과정에서 completion handler를 사용하는 경우 Future를 사용할 시 더욱 깔끔한 코드 작성이 가능하다.
  
### Deferred (struct)
- 구독이 일어나기 전까지 대기상태로 있다가 구독이 일어 났을 때 Publisher가 결정이 된다. 클로저 안에는 지연 실행 할 Publisher 를 반환합니다.
- Swift의 lazy와 비슷하게 Publisher가 실제 사용될 때 Publisher를 생성하기에 메모리를 효율적으로 사용할 수 있다.

### Empty (struct)
- 값을 게시하지 않고 선택적으로 즉시 완료되는 Publisher이다.

### Fail (struct)
- Error를 즉시 보낼 수 있는 Publisher이다. 

### Record (struct)
- 각각의 Publisher가 나중에 내보낼 수 있도록 input과 completion을 저장해두는 Publisher이다.