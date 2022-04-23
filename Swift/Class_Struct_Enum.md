# 유사점 (Similarity)

- Class, Struct, Enum 모두 Swift의 기본 자료구조 블럭이다.

```swift
class A {
}
struct B{
}
enum C{
}
```
- 세가지 자료구조 모두 Properties와 functions을 가질 수 있다.
> 하지만 enum은 Stored Property를 가질 수 없다. 하지만 Computed Property는 가질 수 있다. enum은 연관값(associated value)로서 값을 저장하고 있다.
- 속성값에 접근할 수 있는 방법을 제공하는 subscript를 정의할 수 있다.
- extension을 통해 기능을 확장할 수 있다.
- 프로토콜을 채택할 수 있다.

# 차이점 (Differences)
1. Initializer (초기화함수)
> class와 struct는 initializer를 갖지만 enum은 initializer를 갖지 않는다. 왜냐하면 enum은 연관값을 구별되는 값(discrete values)들에 할당하기 때문이다. class나 struct에서 인스턴스를 생성할 때 Stored Property가 초기화되지 않으면 생헝할 수 없는 등의 문제가 발생해서 기본적으로 초기화에 필요한 정보들을 세팅할 함수가 필요하다. 하지만 enum의 경우 각 case가 애초부터 구별되는 rawValue를 가지며 설정이 안되더라도 default로 정수값이 할당되므로 초기화의 필요성이 없다.

2. Inheritance (상속)
> class에서는 상속이 가능하지만 struct나 enum에서는 불가능하다.

3. Value Type VS Reference Type
> struct와 enum은 값 타입이지만 class는 참조 타입이다. class는 참조 타입으로서 포인터로 전달되고 정보는 heap메모리 영역에 저장한다.
>> 1. heap 영역: 동적으로 할당되는 메모리 영역
>> 2. 동적 메모리 할당: 프로그램 실행 시간 동안 사용할 메모리 공간을 할당하는 것을 말한다. 사용이 끝나면 운영체제가 쓸 수 있도록 반납하고 다음에 요구가 오면 재할당을 받을 수 있다.
>> 3. 정적 메모리 할당: 프로그램을 실행하는 순간 프로그램이 사용할 메모리 크기를 고려하여 메모리의 할당이 이루어지는 것을 말한다. 해제하지 않음으로 인한 메모리 누수와 같은 문제를 신경쓰지 않아도 된다. 하지만 메모리의 크기가 하드 코딩되어 있어서 나중에 조절할 수 없다. 또한 스택 영역에 할당된 메모리이므로 동적 할당에 비해 할당받을 수 있는 최대 메모리에 제약을 받는다.

- 값 타입은 함수에서 인자로 전달될 때 값이 복사된다. 또한 다른 변수에 할당될 때 역시 복사된다.
- 참조 타입은 heap영역에 저장되며 자동적으로 reference count를 한다.
- Swift에는 Garbage Collection이 없다.

4. Type Casting (타입 캐스팅)
> class는 실행 시 컴파일러가 클래스 인스턴스의 타입을 미리 파악하고 검사할 수 있다.

5. deinit (소멸화)
> class는  인스턴스가 소멸되기 직전에 처리해야할 구문들을 미리 등록할 수 있다.

6. Memberwise init (멤버와이즈 초기화)
> struct는 memberwise init을 통해 자동으로 초기화 구문을 생성해준다. 값이 존재하지 않은 Property가 존재할 때(Optional 포함), struct의 경우 자동으로 인스턴스 생성 시 해당 Proeprty의 값을 받는 init을 생성하지만, class는 따로 init을 정의하지 않으면 오류가 발생한다. 
> 
> struct는 상속이 불가능하기 때문에 해당 struct에서 init을 꼭 필요로 한다. 그래서 Swift 자체에서 자동화된 기능을 제공한다. 하지만 class의 경우 상속이 가능하므로, 설계상 해당 클래스가 서브클래스에서만 초기화되어야할 필요성이 있을 수 있다. 즉, 상속 가능성에서 차이가 발생한다.


- 일반적으로 객체지향에서 사용하던 class를 사용하면 되지만 struct는 좀 더 기본적인 타입으로 사용된다. 여기서 기본적인 타입이랑 Stirng, Double, Int, Array, Dicrionary와 그림을 그리기 위한 점, 직사각형 같이 클래스보다는 더 작지만 스스로 자립하며 (self-contained)값으로 복사되는게 말이 되고 값 타입을 원하는 영역들이다. 즉, 전달하고 다닐 때 값 개념을 원하는 상황을 의미한다. enum은 구별되는 값을 가진 타입을 사용할 경우 사용한다.

> ## https://jayb-log.tistory.com/216