# rethrows
- 파라미터로 전달받는 함수(Closure)가 Error를 던질 때 사용
- argument 내부에서 에러가 발생하면, 해당 argument에서 받은 Error를 다시 던질 수 있도록 명시

```swift
enum SomeError: Error {
    case someError
}

func someFunc(callback: () throws -> Void) {

}

func someThrowableFunc() throws {
    throw SomeError.someError
}
```

위와 같이 함수 정의할 시 callback()을 사용하려 하면

```swift
enum SomeError: Error {
    case someError
}

func someFunc(callback: () throws -> Void) {
    do {
        try callback()
    } catch {
        print(error)
    }
}

func someThrowableFunc() throws {
    throw SomeError.someError
}

someFunc(callback: someThrowableFunc)
```

someFunc 내부 에서 Error를 처리해야 한다.
하지만 someFunc가 rethrows를 이용하면

```swift
enum SomeError: Error {
    case someError
}

func someFunc(callback: () throws -> Void) rethrows {
    try callback()
}

func someThrowableFunc() throws {
    throw SomeError.someError
}

do {
    try someFunc(callback: someThrowableFunc)
} catch {
    print(error)
}
```

someFunc를 사용하는 곳에서 Error를 처리할 수 있다.

## throws로 하면 안되나?

```swift
enum SomeError: Error {
    case someError
}

func someFunc(callback: () throws -> Void) throws {
    try callback()
}

func someThrowableFunc() throws {
    throw SomeError.someError
}

do {
    try someFunc(callback: someThrowableFunc)
} catch {
    print(error)
}
```

someFunc를 throws로 처리해도 someFunc를 사용하는 곳에서 Error를 처리할 수 있다.

그렇다면 throws와 rethrows의 차이는 무엇인가?

```swift
import Foundation

enum SomeError: Error {
    case someError
}

func someFunc(callback: () throws -> Void) rethrows {
    try callback()
}

func someThrowableFunc() throws {
    throw SomeError.someError
}

func someNonThrowableFunc() {}

someFunc(callback: someNonThrowableFunc)
```

rethrows를 가진 함수에 throws가 아닌 함수를 전달하면 Error처리를 하지 않는다.
 하지만 throws를 가진 함수에 throws가 아닌 함수를 전달하면 Error처리를 해야한다.

이는 throws를 가진 함수는 내부에서 스스로 throw를 할 수 있고, rethrows를 가진 함수는 내부에서 스스로 throw를 할 수 없는 특성이 있기 때문인거같다.

## 그 외
부모 클래스의 throws는 자식클래스에서 rethrows로 override할 수 있다.
반대로 부모 클래스의 rethrows는 자식클래스에서 throws로 override할 수 없다.

프로토콜 함수에 throws가 있다면 rethrows로 구현할 수 있다.
반대로 프로토콜 함수에 rethrows가 있다면 throws로 구현할 수 없다.