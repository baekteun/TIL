## init을 쓰다보면 아래 코드를 자주 봤을거다.

```swift
required init(coder: NSCoder) {
  fatalError("init(coder) has not been implemented")
}
```

## NSCoding

- UIView와 UIViewController는 NSCoding Protocol을 구현하고 있다.
- * 프로토콜에서 init을 구현하면 앞에 required가 붙는다. 즉 반드시 init을 써야한다.
- NSCoding Protocol은 구현하는 클래스로부터 실패 가능한 init을 작성하도록 한다.
- Protocol에 적혀있는 init을 구현하면 required 키워드가 붙이며
- 이 required 키워드가 붙은 init을 상속받는 자식 클래스에서도 이를 구현해야한다.


## init을 안쓰면 required init?(coder: NSCoder)를 안써도 된다

- UIView와 UIViewController는 NSCoding Protocol을 구현하기에
- 이를 상속받은 클래스에서는 `required init?` 를 구현해줘야 할 수 도 있다.
- swift에서는 자식 클래스에서 지정 init을 따로 작성하지 않은 경우, 부모의 init을 자동으로 상속한다.
- 그래서 지정 init을 작성하지 않았을 경우에는 에러가 발생하지 않았던 것이다.
- 즉 자식 클래스에서 새로운 지정 init을 작성하게 된다면 부모 클래스의 init들이 자동 상속되지 않기 때문에
- `required init?` 을 구현하라는 에서가 발생하는 것이다