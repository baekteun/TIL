## some
- 명확하지 않은 타입이 프로토콜에 정의되어 있고 함수나 연산 프로퍼티를 만들어서 이 프로토콜을 반환 타입으로 갖고 싶을때 아직 명확하지 않은 타입이라서 컴파일 과정에서 오류가 발생하게 되는데 그 오류를 없애기 위해서는 타입을 명확하게 만들어줘야하고 그 역할을 해주는 것이 `some`이다.
  
- 이것을 쓰게되면 컴파일러에게 이 함수 또는 연산 프로퍼티는 동일한 명확한 타입을 가진 값만을 반환한다는 것을 알려주는 것이다

- SwiftUI에서 body 라는 연산 프로퍼티를 보면 `var body: some View`라고 선언되어 있는데 이유는 `Text`, `Image`등 다양한 View 프로토콜을 만족하는 struct가 존재하는데 얼마나 많은 struct들이 선언되었는지 알 수 없으니 `some`이라는 키워드를 붙여 줘서 다양한 struct들을 생성하고 없애고 할 수 있는 것이다.


```swift
import SwiftUI

struct ContentView: View {
    var body: Text {
        Text("Hello World")
    }
}
```

위 코드는 body가 명확하게 `Text`를 반환타입으로 가진다고 명시해 주었기 때문에 따로 `some` 키워드를 작성하여 줄 필요가 없다.


하지만 아래처럼 작성하면
```swift
import SwiftUI

struct ContentView: View {
    var body: Text {
        VStack(content: {
            Text("Hello World")
        })
    }
}
```

`Cannot convert return expression of type 'VStack<Text>' to return type 'Text'` 라는 오류 메세지를 맞이한다.

body 타입을 Text로 명시해줘서 그런데, 저 내용대로라면 VStack\<Text>로 선언을 해줘야 한다. 하지만 이것은 매우 귀찮아 보이기에 

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack(content: {
            Text("Hello World")
        })
    }
}
```
위 처럼 `some`키워드를 붙여주면 다양한 View 프로토콜을 준수하는 struct를 사용할 수 있다.

> https://medium.com/@PhiJay/whats-this-some-in-swiftui-34e2c126d4c4