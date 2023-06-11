# Swift project update

swift-evolution 에서 애플한테 제안을 하는데, 이 제안을 애플에서 검토 후 받아들이는데 이번에 추가된 새로운 기능이 다수 존재
대시보드 : https://www.swift.org/swift-evolution/

작년에 Swift 언어와 표준 라이브러리의 발전에 대한 책임 소재를 확실히 하기 위해서 Language Steering Group을 구성
https://www.swift.org/blog/evolving-swift-project-workgroups/

때로는 여러 proposal이 합쳐져서 광범위한 변화가 일어나기도 함
concurrency는 10개의 proposal을 통해서 도입
이 proposal 들을 묶어줄 수 있는 vision이라는 문서 추가

이는 Swift 커뮤니티가 하는 일의 일부일 뿐이다. 성공적인 언어를 위해서는 더 많은 것들이 필요
    도구 지원
    다양한 플랫폼 지원
    풍부한 문서
이를 위해서 Language Steering Group과 동시에 Ecosystem Steering Group이 추가되었다.

# Expressive code
## Using if/else and switch statements as expressions
if나 switch를 expression으로 사용 가능

기존
```swift
let bullet =
  isRoot && (count == 0 || !willExpand) ? ""
    : count == 0    ? "- "
    : maxDepth <= 0 ? "▹ " : "▿ "
```
읽기 어렵고 복잡한 코드이다.

신규
```swift
let bullet =
  if isRoot && (count == 0 || !willExpand) { "" }
  else if count == 0 { "- " }
  else if maxDepth <= 0 { "▹ " }
  else { "▿ " }
```
기존에 비해 훨씬 가동성이 높게 작성할 수 있다.

<br>

또다른 것으로 stored 전역 변수를 생성할 때, 만약 조건이 필요하다면 closure를 사용해서 해야한다.
```swift
let attributedName = {
    if let displayName, !displayName.isEmpty {
        AttributedString(markdown: displayName)
    } else {
        "Untitled"
    }
}()
```

하지만 이를
```swift
let attributedName =
    if let displayName, !displayName.isEmpty {
        AttributedString(markdown: displayName)
    } else {
        "Untitled"
    }
```
이런식으로 간단하게 만들 수 있다.

## Result Builders
- 더 빠른 타입 체크
- code 자동완성 개선
- 더 나은 에러 메시지

- 기존에는 type checker가 에러의 위치를 정확하게 잡아주지 않는다.
```swift
struct ContentView: View {
    enum Destination { case one, two }

    var body: some View {
        List {
            NavigationLink(value: .one) { // Swift 5.9에서는 여기에 에러가 발생한다.
                Text("one")
            }
            NavigationLink(value: .two) {
                Text("two")
            }
        }
        .navigationDestination(for: Destination.self) {
            $0.view // Swift 5.7에서는 여기에 에러가 발생한다.
        }
    }
}
```

## type parameter packs
기존에는 인수타입과 반환타입이 여러개 생길때마다 개수별로 일일이 다 작성해줘야 했다.
```swift
func evaluate<Result>(_:) -> (Result)
func evaluate<R1, R2>(_:_:) -> (R1, R2)
func evaluate<R1, R2, R3>(_:_:_:) -> (R1, R2, R3)
func evaluate<R1, R2, R3, R4>(_:_:_:_:) -> (R1, R2, R3, R4)
...
```

새로 추가된 `each` 키워드를 사용해 제네릭의 개수를 추상화 가능
```swift
func evaluate<each Result>(_: repeat Request<Result>) -> (repeat each Result)

let result = requestEvaluate.evaluate(r1, r2, r3)
```

## Swift macros
- macro를 통해 보일러 플레이트를 줄이면서 언어의 표현력을 높일 수 있다.

E.g. assert
```swift
assert(max(a, b) == c) // max assert/max assert.swift:5: Assertion failed
XCTAssertEqual(max(a, b) == c) // XCTAssertEqual failed: ("10") is not equal to ("17")
#assert(max(a, b) == c) /*
    #assert(max(a, b) == c)
                |  |  |  |
                10 -1 |  17
                    false
*/
```

Swift에서 macro는 함수와 동일한 api기 때문에 패키지를 통해 배포하고, import해서 사용할 수 있다.

정의부를 보면 함수랑 크게 다를게 없다.
```swift
public macro assert(_ condition: Bool)
```

리턴타임이 필요하면 함수처럼 -> 를 달아주면 된다.

```swift
#assert(max(a, b)) // Type 'Int' cannot be a used as a boolean; test for '!= 0' instead
```

### macro 정의 및 동작 원리
매크로가 정의된 모듈과 해당 매크로를 정의한 타입을 String으로 명시한다.
```swift
public macro assert(_ condition: Bool) = #externalMacro(
  module: “PowerAssertPlugin”,
  type: “PowerAssertMacro"
)
```

macro는 별도 프로그램으로 정의되어 컴파일러의 플러그인으로 들어간다.

컴파일러가 소스코드를 넘기면 macro 프로그램이 새로운 코드를 반환해서 컴파일러가 이 코드를 통합하는 방식.
```swift
// input
#assert(a == b)

// output
PowerAssert.Assertion(
  "#assert(a == b)"
) {
  $0.capture(a, column: 8) == $0.capture(b, column: 13)
}
```

macro의 선언에는 해당 macro의 역할도 명시한다.

E.g. assert는 freestanding(expression)이다. 
> freestanding(expression)? : 독립적으로 expression으로 쓰인다는 뜻

```swift
// Freestanding macro roles

@freestanding(expression)
public macro assert(_ condition: Bool) = #externalMacro(
  module: “PowerAssertPlugin”,
  type: “PowerAssertMacro"
)
```

- freestanding(expression) : 값을 반환하는 코드 조각
- freestanding(declaration) : 하나 이상의 선언

<br>

E.g. CaseDetection
```swift
@CaseDetection
enum Path {
  case relative(String)
  case absolute(String)
}
```

CaseDetection은 attached macro이다.

### attached macro 역할
- attached(member) : 타입이나 extension에 새로운 멤버를 추가
- attached(peer) : 해당 선언에 맞는 추가적인 선언을 추가 (ex. async함수의 completion handler버전, 혹은 반대)
- attached(accessor) : stored property를 computed property로 바꿔서 접근 과정에서의 추가 로직
  - Property Wrapper와 비슷하지만 조금 더 유연
- attached(memberAttribute) : 특정 멤버나 타입에 속성 추가
- attached(comformance) : 프로토콜 채택 추가

attached macro는 여러개를 합칠 수도 있다.
E.g Observable macro
```swift

// Observable 매크로
@attached(member, names: ...)
@attached(memberAttribute)
@attached(conformance)
public macro Observable() = #externalMacro(...)
```

Xcode에서는 매크로를 자동으로 펼쳐줄 수 있는 기능을 제공한다.
  매크로에서 발생한 오류는 펼쳐진 코드에서도 볼 수 있고, 디버거를 통해서 step-in&out이 가능하다.

# Swift everywhere
Swift는 확장할 수 있는 언어로 설계되었다.

## Swift Foundation Framework 오픈소스화
애플 플랫폼과 비애플 플랫폼이 코드를 공유한다.

기존 Foundation은 Objective-C와 C로 작성됨 -> 이를 Swift로 재작성한다.

macOS sonoma와 iOS 17부터 Date, Calendar,  Locale, AttributedString, JSON 인코딩 및 디코딩 등이 Swift로 돌아간다.
  Calendar 계산: value semantic 덕분에 중간 할당을 줄여서 20% 정도 성능 향상
  Date formatting: 표준 datetime 기준 150% 향상
  JSON: 200~500%. 향상

이러한 속도 향상은 브릿징 비용 뿐 아니라 Swift 구현체 자체가 더 효율적이여서 그렇다.

## Ownership
low-level에서 좀 더 최적화를 잘 해주기 위한 opt-in 기능

E.g. FileDescriptor
```swift
struct FileDescriptor {
  private var fd: CInt

  init(descriptor: CInt) { self.fd = descriptor }

  func write(buffer: [UInt8]) throws {
    let written = buffer.withUnsafeBufferPointer {
      Darwin.write(fd, $0.baseAddress, $0.count)
    }
    // ...
  }

  func close() {
    Darwin.close(fd)
  }
}
```

위처럼하면 실수가 일어나기 쉬운 API다.
예를들어서 close를 호출하고 나서 write를 호출한다는 것이 있다. 그리고 사용을 끝내면 매번 수동으로 close를 호출하지 않으면 리소스 누수가 일어날 수 있다.

이를 해결하기 위한 방안 중 하나는 타입을 class로 만들고 deinit이 되면 close를 호출하는 방안이 있다.

```swift
class FileDescriptor {
  private var fd: CInt

  init(descriptor: CInt) { self.fd = descriptor }

  func write(buffer: [UInt8]) throws {
    let written = buffer.withUnsafeBufferPointer {
      Darwin.write(fd, $0.baseAddress, $0.count)
    }
    // ...
  }

  func close() {
    Darwin.close(fd)
  }

  deinit {
    self.close()
  }
}
```

다만 이러면
- 추가적인 메모리 할당 (다만 이는 아주 제한된 시스템이 아닌이상 크게 문제될 것은 없다.)
- reference sementic이기 때문에 여러 스레드간에 공유가 가능하여 race condition이 발생할 수 있음
- 다른 곳에 보관해서 해제가 안될 수도 있음
등의 문제가 발생할 수 있다.

이를 해결하기 위해 Swift 5.9에서는 `NonCopyable`를 struct에 적용할 수 있다.

```swift
struct FileDescriptor: ~Copyable {
  private var fd: CInt
  
  init(descriptor: CInt) { self.fd = descriptor }

  func write(buffer: [UInt8]) throws {
    let written = buffer.withUnsafeBufferPointer {
      Darwin.write(fd, $0.baseAddress, $0.count)
    }
    // ...
  }
  
  func close() {
    Darwin.close(fd)
  }
  
  deinit {
    Darwin.close(fd)
  }
}
```

복사할 수 없는 타입으로 만듦으로써 class와 마찬가지로 해당 유형의 값이 범위를 벗어날 때 실행되는 deinit을 지정할 수 있다.

또한 NonCopyable은 close() 를 호출한 다음에 다른 메서드를 사용할 수 있는 문제를 해결할 수 있다.

```swift
struct FileDescriptor: ~Copyable {
  private var fd: CInt
  
  init(descriptor: CInt) { self.fd = descriptor }

  func write(buffer: [UInt8]) throws {
    let written = buffer.withUnsafeBufferPointer {
      Darwin.write(fd, $0.baseAddress, $0.count)
    }
    // ...
  }
  
  consuming func close() {
    Darwin.close(fd)
  }
  
  deinit {
    Darwin.close(fd)
  }
}
```

consuming을 붙인 close 메서드를 호출하면 호출한 메서드에 대한 값의 소유권을 포기하게 된다.
이 타입은 복사할 수 없으므로 소유권을 포기한다는 것은 더 이상 값을 사용할 수 없다는 것을 의미한다.

```swift
let file = FileDescriptor(fd: descriptor)
file.close()
file.write(buffer: data) // Compiler error: 'file' used after consuming
```

# C++ interoperability (상호운용)
Swift는 Objective-C와의 상호 운용을 지원해서 점진적으로 마이그레이션이 가능해서 성공적으로 안착할 수 있었다.
근데 기존 코드에서는 C++도 많다. 이에 대한 상호 운용을 위해서는 중간에 Objective-C 레이어를 거쳐야 했다.

5.9부터 Swift에서 직접 C++로의 브릿징을 지원한다.
기본적인 것들은 잘 이해하지만, 추가적인 어노테이션으로 원하는 의미를 커스텀해줄 필요가 있다.

```swift
// Person.h
struct Person {
  Person(const Person &);
  Person(Person &&);
  Person &operator=(const Person &);
  Person &operator=(Person &&);
  ~Person();
  
  std::string name;
  unsigned getAge() const;
};
std::vector<Person> everyone();

// Client.swift
func greetAdults() {
  for person in everyone().filter { $0.getAge() >= 18 } {
    print("Hello, \(person.name)!")
  }
}
```

반대도 된다

```swift
// Geometry.swift
struct LabeledPoint {
  var x = 0.0, y = 0.0
  var label: String = “origin”
  mutating func moveBy(x deltaX: Double, y deltaY: Double) { … }
  var magnitude: Double { … }
}

// C++ client
#include <Geometry-Swift.h>

void test() {
  Point origin = Point()
  Point unit = Point::init(1.0, 1.0, “unit”)
  unit.moveBy(2, -2)
  std::cout << unit.label << “ moved to “ << unit.magnitude() << std::endl;
}
```

또한 CMake도 지원된다.
CMake 지원을 위해서 CMake Community와 협업하고 C++ 코드를 직접 넣는 것도 가능하다.

# Actors and concurrency

## 추상 concurrency model
Tasks: Sequential unit of work that can run anywhere
- 어디서든 실행할 수 있는 작업의 순차적 단위

Actors: Mutually exclusive access to isolated state
- 고립된 상태에 대한 상호 배제적인 접근

하지만 각 추상화는 플랫폼에 맞추기 위해서 다르게 구현되어 있다.
- global concurrent pool이 어떻게 작업을 스케쥴링할지는 환경에 따라 다르다.
  - 애플 플랫폼의 Dispatch
  - 제한적인 시스템에서 싱글 스레드 기반의 cooperative 큐

기존 callback 시스템과의 상호운용을 위해 CheckContinuation을 제공한다.

표준 라이브러리에서 actor 구현은 lock-free queue다.
하지만 실제 구현에서는 여러 방법으로 구현될 수 있다.
- 제한된 환경에서는 atomic이 없어서, spinlock을 사용해야 될 수도 있다.
- 아니면 단일 스레드여서 동기화가 필요 없을 수도 있다.

5.9 부터는 actor의 executor를 커스텀할 수 있게 된다.
-> 자체적인 동기화 매커니즘을 구현해서 현재 환경에 좀 더 유연하게 동작하게 만들 수 있다.
예시로 특정 dispatchQueue를 전용으로 할당할 수 있다.

```swift
// Custom actor executors

actor MyConnection {
    private var database: UnsafeMutablePointer<sqlite3>
  
    init(filename: String) throws { … }
  
    func pruneOldEntries() { … }
    func fetchEntry<Entry>(named: String, type: Entry.Type) -> Entry? { … }
}

await connection.pruneOldEntries()
```

```swift
actor MyConnection {
  private var database: UnsafeMutablePointer<sqlite3>
  private let queue: DispatchSerialQueue
  
  nonisolated var unownedExecutor: UnownedSerialExecutor { queue.asUnownedSerialExecutor() }

  init(filename: String, queue: DispatchSerialQueue) throws { … }
  
  func pruneOldEntries() { … }
  func fetchEntry<Entry>(named: String, type: Entry.Type) -> Entry? { … }
}

await connection.pruneOldEntries()
```

dispatchQueue는 Serial Executor를 채택하기 때문에 위 코드가 가능하다.

```swift
// Executor protocols

protocol Executor: AnyObject, Sendable {
    func enqueue(_ job: consuming ExecutorJob)
}

protocol SerialExecutor: Executor {
    func asUnownedSerialExecutor() -> UnownedSerialExecutor
    func isSameExclusiveExecutionContext(other executor: Self) -> Bool
}

extension DispatchSerialQueue: SerialExecutor { … }
```

# FoundationDB: A case study
C++ 기반 대규모 크로스 플랫폼 Key-Value DB
- macOS, Linux, Windows 지원

C++ 코드베이스고, 자체적인 분산 액터와 런타임을 가지고 있음

Swift를 통해서 성능, 안전성, 가독성을 높이고 싶지만, 전체 재작성은 리스크가 너무 크다.
대신 Swift와의 상호운용을 통해 기존 코드베이스를 함께 다룬다.
```cpp
// C++ implementation of FoundationDB’s “master data” actor

ACTOR Future<Void> getVersion(Reference<MasterData> self, GetCommitVersionRequest req) {
  	state std::map<UID, CommitProxyVersionReplies>::iterator proxyItr = self->lastCommitProxyVersionReplies.find(req.requestingProxy);
  	++self->getCommitVersionRequests;

  	if (proxyItr == self->lastCommitProxyVersionReplies.end()) {
      	req.reply.send(Never());
    	  return Void();
  	}
  	wait(proxyItr->second.latestRequestNum.whenAtLeast(req.requestNum - 1));
  
  	auto itr = proxyItr->second.replies.find(req.requestNum);
  	if (itr != proxyItr->second.replies.end()) {
    		req.reply.send(itr->second);
    		return Void();
  	}

  	// ...
}
```

```swift
// Swift implementation of FoundationDB’s “master data” actor
func getVersion(
    myself: MasterData, req: GetCommitVersionRequest
) async -> GetCommitVersionReply? {
    myself.getCommitVersionRequests += 1

    guard let lastVersionReplies = lastCommitProxyVersionReplies[req.requestingProxy] else {
        return nil
    }

    // ...
    var latestRequestNum = try await lastVersionReplies.latestRequestNum
          .atLeast(VersionMetricHandle.ValueType(req.requestNum - UInt64(1)))

    if let lastReply = lastVersionReplies.replies[req.requestNum] {
        return lastReply
    }
}
```