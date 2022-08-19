# Factory?
- 객체를 사용하는 코드에서 `객체 생성 부분`을 떼어내 `추상화`한 패턴
- 상속 관계에 있는 두 클래스에서 `상위 클래스가 중요한 뼈대`를 결정하고, `하위 클래스에서 객체 생성에 관한 구체적인 내용`을 결정하는 패턴
- 상위 클래스와 하위 클래스가 분리되기 때문에 `느슨한 결합`을 가지며 상위 클래스에서는 인스턴스 생성 방식에 대해 `전혀 알 필요가 없기 때문`에 더 많은 유연성을 갖게 된다
- `객체 생성 로직이 따로 떼어져` 있기 때문에 코드를 리팩토링하더라도 한 곳만 고칠 수 있게 되니 `유지보수성`이 증가한다.

# Example
```swift
import UIKit

enum UIComponent {
    case label, button, textField
}

protocol MyAppUIComponent {

    var component: UIComponent { get }
    var textColor: CGColor { get set }
    var backgroundColor: UIColor { get set }
}


final class MyAppLabel: UILabel, MyAppUIComponent {
    
    var component: UIComponent { .label }
    
    init(textColor: CGColor = UIColor.label.cgColor, backgroundColor: UIColor = .systemBackground) {
        self.textColor = textColor
        self.backgroundColor = backgroundColor
    }
}


final class MyAppButton: UIButton, MyAppUIComponent {

    var component: UIComponent { .button }

    init(textColor: CGColor, backgroundColor: UIColor = .systemBackground) {
        self.textColor = textColor
        self.backgroundColor = backgroundColor
    }
}

final class MyAppTextField: UITextField, MyAppUIComponent {
    
    var component: UIComponent { .textField }

    init(textColor: CGColor = UIColor.label.cgColor, backgroundColor: UIColor) {
        self.textColor = textColor
        self.backgroundColor = backgroundColor
    }
}

struct ComponentFactory {
    
    func make(_ component: UIComponent) -> MyAppUIComponent {
        switch component {
        case .label:
            return MyAppLabel()
        case .button:
            return MyAppButton(textColor: UIColor.systemPink.cgColor)
        case .textField:
            return MyAppTextField(backgroundColor: .systemTeal)
        }
    }
}
```
```swift
let factory = ComponentFactory()

let label = factory.make(.label)
let button = factory.make(.button)
let textField = factory.make(.textField)
```
