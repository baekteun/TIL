## 더블(Double)?
할리우드에서 배우들의 대역을 해주는 사람을 더블이라 한다.

## 테스트 더블?
위의 더블에서 유래하여 Test를 할 때 실제 도메인(주연)을 사용하지 않고 더블(대역)을 사용하여 테스트를 하는 것을 말한다.

## 테스트 더블의 종류 
- Dummu
- Stub
- Spy
- Fack
- Mock

### Dummy
- 아무런 동작(기능)도 하지 않음
- 인스턴스화 하여 구현한 가짜 객체
- 인스턴스화된 객체만 필요하면서 기능까지는 필요하지 않을 경우 Dummy를 사용
- ex) 로깅을 하는 객체

```swift
protocol Logger {
    func log(_ message: String)
}

struct DummyLogger: Logger {
    func log(_ message: String) { }
}
```
테스트할때 log()는 아무런 영향을 끼치지 않는다. 

### Stub
- Dummy 객체가 실제로 동작하는 것처럼 보이게 만든 객체
- 미리 반환할 데이터가 정의돼 있으며, 메서드를 호출할 경우 그대로 반환
- **상태 검증**을 위한 객체

> 상태 검증 - 메서드가 수행된 후, 객체의 상태를 보며 올바르게 동작했는지 확인하는 것

### Spy
- 실제 객체를 부분적으로 Sutbbing하면서 동시에 약간의 정보를 기록
- 스파이처럼 기록을 하는 역할을 가진 객체
- 테스트에서 특정 객체가 사용되었는지, 그리고 그 객체의 예상된 메서드가 정상적으로 호출됐는지를 확인해야 하는 상황이 생기는 경우 사용

### Mock
- Stub이 상태 검증을 위한 객체라면 Mock은 **행위 검증**을 위한 객체
> 행위 검증이란 메서드의 리턴 값으로 판단할 수 없는 경우 특정 동작을 수행하는지 확인하는 것

### Fake
- 복잡한 로직이나 객체 내부에서 필요로 하는 다른 외부 객체들의 동작을 단순화하여 구현한 객체
- 동작의 구현을 가지고 있지만 실제 프로덕션에는 적합하지 않은 객체
- ex) Inmemory DB