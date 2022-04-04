# Dependency
- 객체 지향 프로그래밍에서 Dependency, 의존성은 서로 다른 객체 사이에 의존 관계가 있다는 것을 말한다.
즉, 의존하는 객체가 수정되면, 다른 객체도 영향을 받는다는 것이다.

```Swift
import UIKit

struct Eat {
    func coffee() {
        print("아메리카노")
    }

    func meal() {
        print("피자")
    }
}

struct Person {
    var todayEat: Eat
    
    func coffee() {
        todayEat.coffee()
    }
    
    func meal() {
        todayEat.meal()
    }
}
````

- `Person`객체는 `Eat`객체를 인스턴스로 사용하고 있으므로, Eat객체에 의존성이 생긴다.
- 만약 이때, `Eat`객체에 중요한 수정이나 오류가 발생한다면, `Person`객체도 영향을 받을 수 있다.
- 의존성을 가지는 코드가 많아진다면, 재활용성이 떨어지고 매번 의존성을 가지는 객체들을 함계 수정해야한다는 문제가 발생한다.
- 이러한 의존성을 해결하기 위해 나온 개념이 바로 `Dependency Injection`, 의존성 주입이다.


## Injection이란?
- Injection, 주입은 외부에서 객체를 **생성** 해서 넣는 것을 의미한다.

```swift
class  Eat: Menu {
    var coffee: String
    var meal: String

    init(coffee: String, meal: String) {
        self.coffee = coffee
        self.meal = meal
    }

    func printCoffee() {
        print("아메리카노")
    }

    func printMeal() {
        print("피자")
    }
}
let menu = Eat(coffee: "아메리카노", meal: "피자")
```

- 위 코드와 같이 생성자 등을 활용해서 외부에서 주입할 수 있다.

## Dependency Injection, 의존성 주입의 장점
- Unit Test용이. iOS 개발자들에게 필요한 `테스트용이한 코드 작성하기`의 핵심
- 코드의 재활용성을 높여준다.
- 객체간의 의존성(종속성)을 줄이거나 없앨 수 있다.
- 객체 간의 결합도를 낮추면서 유연한 코드를 작성할 수 있다.
- 그렇다면 내부에서 만든 객체를 외부에서 넣어저 의존성을 주입하는 것은 어떻게?
- 이전에 `DIP: 의존 관계 역전 법칙`을 알아야 한다.

## Dependency Inversion Principle: 의존관계 역전 법칙
- DIP, 의존 관계 역전 법칙은 객체 지향 프로그래밍 설계의 다섯가지 기본 원칙(SOLID)중 하나이다.
- 추상화된 것은 구체적인 것에 의존하면 안되고 구체적인 것이 추상화된 것에 의존해야 한다.
- 즉 구체적인 객체는 추상화된 객체에 의존 해야 한다는 것이 핵심이다.
- Swift에서 추상화된 객체는 Protocol이 있다.
- 우리는 이 Protocol을 활용해서 의존성 주입을 구현하려고 한다.
- 우선 Protocol을 활용해서 추상적인 객체를 만들어야 한다.
- Menu라는 Protocol은 printCoffee()와 printMeal() 함수를 가지고 있다.
- 
```Swift
protocol Menu {
    func printCoffee()
    func printMeal()
}
```

이후 Eat 클래스는 Menu Protocol을 채택한 후,

Protocol에 정의한 함수를 실체화 시켜준다.

```Swift
class Eat: Menu {
    var coffee: String
    var meal: String

    init(coffee: String, meal: String) {
        self.coffee = coffee
        self.meal = meal
    }

    func printCoffee() {
        print(coffee)
    }

    func printMeal() {
        print(meal)
    }
}
```

이제부터 중요한 부분이 나온다.

기존의 방식과 다르게 todayEat 변수는 추상적인 객체인 Menu타입에 의존하게 된다.

여기서 changeMenu함수를 활용해서 의존성 주입을 시킬 수 있다.

```Swift
struct Person {
    var todayEat: Menu

    func printCoffee() {
        todayEat.printCoffee()
    }
    func printMeal() {
        todayEat.printMeal()
    }

    mutating func changeMenu(menu: Menu) {
        self.todayEat = menu
    }
}
```

이렇게 구현한다면 Eat객체와 Person객체는 거의 독립적인 객체가 된다.

Eat 객체를 수정하거나 Person을 수정한다고 해서 상대 객체를 함께 수정해야 하는 문제를 방지할 수 있다.

```Swift
let menu = Eat(coffee: "아메리카노", meal: "피자")
let anotherMenu = Eat(coffee: "라떼", meal: "햄버거")

var suhshin = Person(todayEat: menu)

suhshin.printCoffee() // 아메리카노
suhshin.changeMenu(menu: anotherMenu)
suhshin.printCoffee() // 라떼
```