# Context (맥락)

Context는 `컨텐츠를 담은 그 무언가` / `어떤 위치에 값이 존재할 수 있는 맥락`

<br>

## 예시
물 - 컨텐츠
물컵 - 컨텍스트

Swift의 옵셔널 (enum Optional)
```swift
...
case some(Value)
case none
...
```
`2`라는 숫자를 옵셔널에 담는다면, `Context(옵셔널)`안에 2라는 컨텐츠가 들어가게 된다.
-> `Context(옵셔널)`는 2라는 값을 가지고 있다.

만약 값이 없는 옵셔널이라면 Context는 존재하지만 안에 값이 없다.

<br>

# Functor (함수 객체)
고차 함수인 `map`을 적용할 수 있는 컨테이너 타입

> [컨테이너 타입](./Container-Type.md)

## Why
`map`을 적용할 수 있는 컨테이너 타입이 왜 Functor인가?

우선, Int? (Optional<Int>) 와 Int는 다른 타입이다.
그렇기에

```swift
let a: Int? = 2
let b: Int = 2
print(a + b)
```

위 코드는 컴파일 에러가 발생한다.
왜? Int?와 Int는 명백히 다른 타입이기 때문이다.

위 코드에서 `a`는 Context이다. 값이 있을수도 있고 없을수도 있다.
이걸 꺼내는 작업이 고차함수 `map`이다.

```swift
let a: Int? = 2
let b: Int = 2
print(a.map { $0 + b })
```

`map`을 사용한다면 Context에 값이 있다면 해당 값을 꺼낸다. 이렇게 값을 꺼내면 그 값으로 연산이 가능하다.

<br>

# Monad
Functor의 일종이다.
값이 있을 수도 있고 없을 수도 있는 Context를 가지는 함수객체 타입.
-> Optional 이 해당 조건을 충족하므로 Optional == Monad라고 할 수 있다.

+ Monad는 flatMap을 적용할 수 있다.