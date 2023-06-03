# Capture?

> 여기에서 Capture는 Closure Capture를 의미한다.

클로저 캡처란 클로저가 파라미터가 로컬 변수가 아닌 주변 외부의 context를 `참조`하는 것을 의미한다.

## 캡처 방식
값을 캡처할때 `Reference Capture`를 한다. 

Value 타입, Reference 타입 구분없이 Reference Capture를 하며, 일반적인 Value 타입이더라도 클로저가 캡처한다면 내부에 Reference Count가 생기고 Reference 타입으로 취급하여 Heap에 올라간다.

## Capture List
기본적으로 클로저에서 캡처를 하면 클로저를 실행할 때 캡처한다.

그렇기에 
```swift
var a = 0
let closure = { print(a) }
a = 1
closure() // 1
```

위 코드에서 클로저를 실행할때 a는 1로 출력된다.

이런 상황에서 만약 a가 0으로 출력되길 원한다면 어떻게 해야할까?

이럴때 사용하는 것이 `Capture List`이다.

```swift
var a = 0
let closure = { [a] in print(a) }
a = 1
closure() // 0
```

위 코드에서 `closure`의 Capture List에 `[a]`를 추가했다.
이렇게하면 클로저가 생성될때 a를 캡처하여 사용한다.

이때 캡처하는 값이 Value 타입이라면 `값을 복사`하고, Reference 타입이라면 `참조`(RC += 1)한다.
만약, Reference 타입이라면 weak, unowned 로 캡처가 가능하다.

<br>

# Self Capturing
위에서 Capture를 알아봤는데 Self Capturing은 말그대로 `self`를 Capture하는 것이다.

## Self Capturing을 할 때 주의점
```swift
class A {
    var closure: (() -> Void)?
    
    func doSomething() {
        closure = {
            self.someFunction()
        }
    }

    func someFunction() {
        print("someFunction")
    }
    
    deinit {
        print("deinit")
    }
}

var a: A? = A()
a?.doSomething()
a = nil
```

해당 코드에서 `a = nil`을 할 때 deinit이 호출되지 않는다.
왜냐하면 클로저에서 A를 강하게 참조하며 Reference Count가 0이되지 않기 때문이다.

```swift
class A {
    var closure: (() -> Void)?
    
    func doSomething() {
        closure = { [weak self] in
            self?.someFunction()
        }
    }

    func someFunction() {
        print("someFunction")
    }
    
    deinit {
        print("deinit")
    }
}

var a: A? = A()
a?.doSomething()
a = nil
```

closure에서 self를 weak로 캡처하면 Reference Count를 +하지 않기때문에, a = nil을 할 때 RC가 0이되어 deinit이 정상적으로 호출된다.

> escaping closure라고 '무조건' weak로 캡처해야하는 것은 아니다. 핵심은 closure가 살아있으면서 self를 참고하고 있으면, self의 RC가 1이상 남아있어서 self가 죽지 않는 것이다.