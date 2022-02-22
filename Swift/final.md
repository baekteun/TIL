# final

### final?
- 해당 클래스에서 하위 클래스로의 전체 클래스 또는 일부 (메서드, 프로퍼티)가 상속 또는 상속에 따른 재정의가 될 필요 없다고 판단될 경우 `final`키워드를 각 요소 앞에 추가함으로써 상속을 방지.

### 성능에 미치는 영향

`final`로 선언된 요소들은 직접 호출하는 반면, 그렇지 않은 요소들은 `vtable`을 통해 간접 호출되어 직접 호출하는 경우보다 느리게 작동한다.
> https://github.com/apple/swift/blob/main/docs/OptimizationTips.rst#advice-use-final-when-you-know-the-declaration-does-not-need-to-be-overridden

### vtable?
`vtable`은 가상 메서드 테이블을 이르는 것으로, virtual method table, virtual function table, virtual call table, dispatch table, vftable 등으로 부르기도 한다.
메서드 오버라이딩에 따라 실행 시점에 어떤 메서드를 실행할지 결정하는 동적 디스패치를 지원하기 위해 프로그래밍 언어에서 사용하는 메커니즘이다.