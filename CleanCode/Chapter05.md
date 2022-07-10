##
---
- 형식을 맞추는 목적
- 적절한 행 길이를 유지하라
  - 신문 기사처럼 작성하라
  - 개념은 빈 행으로 분리하라
  - 세로 밀집도
  - 수직 거리
  - 세로 순서
- 가로 형식 맞추기
  - 가로 공백과 밀집도
  - 가로 정렬
  - 들여쓰기
  - 가짜 범위
- 팀 규칙
- 밥 아저씨의 형식 규칙

## Intro
---
질서정연하고 깔끔하며, 일관적인 코드를 본다면 사람들에게 전문가가 짰다는 인상을 심어줄 수 있다.
반대로, 코드가 어수선해 보인다면 프로젝트 전반적으로 무성의한 태도로 작성했다고 생각할 것이다.

프로그래머라면 형식을 깔끔하게 맞춰 코드를 짜야한다.
코드 형식을 맞추기 위한 간단한 규칙을 정하고, 그 규칙을 확실히 따라야 하며,
팀으로 일한다면 팀이 합의해 규칙을 정하고 모두가 그 규칙을 따라야 한다.
필요하다면 규칙을 자동으로 적용하는 도구를 활용한다. (e.g Android Studio의 Code Formatter)

## 형식을 맞추는 목적
---
코드 형식은 중요하다! 너무 중요해서 무시하기 어렵다.
코드 형식은 의사소통의 일환이며, 의사소통은 전문 개발자의 일차적인 의무다.
오늘 구현한 기능이 다음 버전에서 바뀔 확률은 높고, 시간이 지나면 원래 코드의 흔적을 찾아볼 수 없는 경우도 많지만, 
오늘 구현한 코드의 스타일과 가독성 수준은 유지보수의 용이성과 확장성에 지속적인 영향을 미친다.
> 코드는 사라져도 스타일과 규율은 사라지지 않는다!

## 적절한 행 길이를 유지하라 (코드의 세로 길이)
---
소스코드는 얼마나 길어야 적당할까?
500줄은 넘지 않고 대부분 200줄 정도인 파일로도 커다란 시스템을 구축할 수 있다.
(실제로 전문 Java 프로젝트들(JUnit, FitNesse, Time And Money 등)이 이렇게 구현되어있다!)

코드 길이를 200줄 정도로 제한하는 것은 반드시 지킬 엄격한 규칙은 아니지만,
일반적으로 큰 파일보다는 작은 파일이 이해하기가 쉽다.

**신문 기사처럼 작성하라**

좋은 신문 기사는 최상단에 표제(기사를 몇마디로 요약하는 문구),
첫 문단에는 전체 기사 내용을 요약하며, 기사를 읽으며 내려갈 수록 세세한 사실이 조금씩 드러나며 세부사항이 나오게 된다.
소소파일 이름(표제)는 간단하면서도 설명이 가능하게 지어,
이름만 보고도 올바른 모듈을 살펴보고 있는지를 판단 할 수 있도록 한다.
소스파일의 첫 부분(여약 내용)은 고차원 개념과 알고리즘을 설명한다.
아래로 내려갈수록 의도를 세세하게 묘사하며, 마지막에는 가장 저차원 함수(아마 Getter/Setter?)와 세부 내역이 나온다.
신문이 사실, 날짜, 이름 등을 무작위로 뒤섞은 긴 기사 하나만 싣는다면 아무도 신문을 읽지 않을 것이다.

**개념은 빈 행으로 분리하라**

코드의 각 줄은 수식이나 절을 나타내고, 여러 줄의 묶음은 완결된 생각 하나를 표현한다.
생각 사이에는 빈 행을 넣어 분리해야 한다. 그렇지 않다면 단지 줄바꿈만 다를 뿐인데도 코드 가독성이 현저히 떨어진다.
```swift
// 빈 행을 넣지 않을 경우
import Regex
public class BoldWidget: ParentWidget {
    public static let REGEXP = "'''.+?'''"
    private static let pattern = Pattern.compile("'''(.+?)'''", Pattern.MULTILINE + Pattern.DOTALL)
    public init(parent: ParentWidget, text: String) throws {
        super.init(parent: parent)
        var match = pattern.matcher(text)
        match.find()
        addChildWidget(match.group(1))
    }
    public func render() throws -> String {
        var html = StringBuffer("<b>")
        html.append(childHtml()).append("</b>")
        return html
    }
}
```

```swift
// 빈 행을 넣을 경우
import Regex

public class BoldWidget: ParentWidget {
    public static let REGEXP = "'''.+?'''"
    private static let pattern = Pattern.compile("'''(.+?)'''", Pattern.MULTILINE + Pattern.DOTALL)

    public init(parent: ParentWidget, text: String) throws {
        super.init(parent: parent)
        var match = pattern.matcher(text)
        match.find()
        addChildWidget(match.group(1))
    }

    public func render() throws -> String {
        var html = StringBuffer("<b>")
        html.append(childHtml()).append("</b>")
        return html
    }
}
```

**세로 밀집도**

줄바꿈이 개념을 분리한다면, 반대로 세로 밀집도는 연관성을 의미한다.
즉, 서로 밀집한 코드 행은 세로로 가까이 놓여야 한다.

```swift
// 의미없는 주석으로 변수를 떨어뜨려 놓아서 한눈에 파악이 잘 안된다.
public class ReporterConfig {
    /**
    * The class name of ther reporter listener
    */
    private var m_className: String?

    /**
    * The properties of the reporter listener 
    */
    private var m_properties: [Property] = []
    public func addProperty(property: Property) {
        m_properties.append(property)
    }
}
```

```swift
// 의미 없는 주석을 제거함으로써 코드가 한눈에 들어온다.
// 변수 2개에 메서드가 1개인 클래스라는 사실이 드러난다.
public class ReporterConfig {
    private var m_className: String?
    private var m_properties: [Property] = []
    public func addProperty(property: Property) {
        m_properties.append(property)
    }
}
```

**수직 거리**

서로 밀접한 개념은 세로로 가까이 둬야한다.
두 개념이 서로 다른 파일에 속한다면 규칙이 통하지 않지만,
타당한 근거가 없다면 서로 밀접한 개념은 한 파일에 속해야 마땅하다(protected 변수를 피해야 하는 이유)
같은 파일에 속할 정도로 밀접한 두 개념은 세로 거리로 연관성_-한 개념은 이해하는 데 다른 개념이 중요한 정도-_을 표현한다.

##### 변수선언

변수는 사용하는 위치에서 최대한 가까이 선언한다.
우리가 만든 함수는 매우 짧으므로 (Chapter3 - 함수를 공부했다면 말이지)

```swift
// InputStream이 함수 맨 처음에 선언되어 있다.
private static func readPreferences() {
    var `is`: InputStream?
    try {
        is = FileInputStream(file: getPreferencesFile())
        setPreferences(is: is)
        getPreferences().load(is: is)
    } catch(e: IOException) {
        try {
            if `is` != null {
                is.close()
            }
        } catch(e1: IOException) {
        }
    }
}
```

```swift
// 모두들 알다시피 루프 제어 변수는 Test each처럼 루프 문 내부에 선언
public func countTestCases() -> Int {
    var count = 0
    for each in tests {
        count += each.countTestCases()
    }
    return count
}
```

```swift
// 드물지만, 긴 함수에서는 블록 상단 또는 루프 직전에 변수를 선언 할 수도 있다
for test in m_suite.getTests() {
    var tr = m_runnerFactory.newTestRunner(self, test)
    tr.addListener(m_testReporter)
    m_testRunnters.add(tr)

    invoker = tr.getInvoker()

    for m in tr.getBeforeSuiteMethods() {
        beforeSuiteMethods.put(m.getMethod(), m)
    }

    for m in tr.getAfterSuiteMethods() {
        afterSuiteMethods.put(m.getMethod(), m)
    }
}
```

##### 인스턴스 변수

인스턴스 변수는 클래스 맨 처음에 선언한다 (자바의 경우).
변수간 세로로 거리를 두지 않는다 - 잘 설계한 클래스는 대다수 클래스 메서드가 인스턴스 변수를 사용하기 때문.
C++의 경우에는 마지막에 선언하는 것이 일반적이다. 어느 곳이든 잘 알려진 위치에 인스턴스 변수를 모으는 것이 중요하다.

```swift
// 도중에 선언된 변수는 꽁꽁 숨겨놓은 보물 찾기와 같다. 십중 팔구 코드를 읽다가 우연히 발견한다. 발견해보시길.
// 요즘은 IDE가 잘 되어있어서 찾기야 어렵지 않겠지만, 더러운건 마찬가지
public class TestSuite: Test {
    public static func createTest(theClass: TestCase, name: String) -> Test {
        ...
    }
    
    public static func getTestConstructor(theClass: TestCase) throws -> Constructor {
        ...
    }

    public static func warning(message: String) -> Test {
        ...
    }

    private static exceptionToString(t: Throwable) -> String {
        ...
    }

    private var fName: String?

    private var fTests: Vector<Test>? = []

    public init() {}

    public init(theClass: TestCase) {
        ...
    }

    public init(theClass: TestCase, name: String) {
        ...
    }
    ... ... ... ... ...
 }
```

##### 종속 함수

한 함수가 다른 함수를 호출한다면(종속 함수) 두 함수는 세로로 가까이 배치한다. 가능하면 호출되는 함수를 호출하는 함수보다 뒤에 배치한다. (프로그램이 자연스럽게 읽힐 수 있도록) 이러한 규칙을 일관되게 적용한다면 독자는 방금 함수에서 호출한 함수가 잠시 후에 정의될 것이라고 자연스레 예측한다.

```swift
/*첫째 함수에서 가장 먼저 호출하는 함수가 바로 아래 정의된다.
다음으로 호출하는 함수는 그 아래에 정의된다. 그러므로 호출되는 함수를 찾기가 쉬워지며
전체 가독성도 높아진다.*/
	
/*makeResponse 함수에서 호출하는 getPageNameOrDefault함수 안에서 "FrontPage" 상수를 사용하지 않고,
상수를 알아야 의미 전달이 쉬워지는 함수 위치에서 실제 사용하는 함수로 상수를 넘겨주는 방법이
가독성 관점에서 훨씬 더 좋다*/

public class WikiPageResponder: SecureResponder {
    fileprivate var page: WikiPage?
    fileprivate var pageData: PageData?
    fileprivate var pageTitle: String?
    fileprivate var request: Request?
    fileprivate var crawler: PageCrawler?

    public func makeResponse(context: FitNesseContext, request: Request) throws -> Response {
        let pageName = getPageNameOrDefault(request: request, defaultPageName: "FrontPage")
        loadPage(pageName, context)
        if page == null {
            return notFoundResponse(context, request)
        } else {
            return makePageResponse(context)
        }
    }

    private getPageNameOrDefault(request: Request, defaultPageName: String) -> String {
        var pageName = request.getResource()
        if pageName.isBlank {
            pageName = defaultPageName
        }
        return pageName
    }
    fileprivate func loadPage(_ resource: String, context: FitNesseContext) throws {
        let path = PathParser.parse(resource)
        crawler = context.root.getPageCrawler()
        crawler?.setDeadEndStrategy(VirtualEnabledPageCrawler())
        page = crawler?.getPage(context.root, path)
        if page != null {
            pageData = page.getData()
        }
    }

    private func notFoundResponse(context: FitNesseContext, request: Request) throws -> Response {
        NotFoundResponder().makeResponse(context: context, request: request)
    }

    private func makePageResponse(context: FitNesseContext) throws -> SimpleResponse {
        pageTitle = PathParser,render(crawler?.getFullPath(page))
        let html = makeHtml(context)
        var response = SimpleResponse()
        response.setMaxAge(0)
        response.setContent(html)
        return response
    }
}
```

##### 개념의 유사성

개념적인 친화도가 높을 수록 코드를 서로 가까이 배치한다. 앞서 살펴보았듯이 한 함수가 다른 함수를 호출하는 종속성, 변수와 그 변수를 사용하는 함수가 그 예다. 
그 외에도 비슷한 동작을 수행하는 함수 무리 또한 개념의 친화도가 높다.

```swift
// 같은 assert 관련된 동작들을 수행하며, 명명법이 똑같고 기본 기능이 유사한 함수들로써 개념적 친화도가 높다.
// 이런 경우에는 종속성은 오히려 부차적 요인이므로, 종속적인 관계가 없더라도 가까이 배치하면 좋다.

public class Assert {
    public static func assertTrue(message: String? = nil, condition: Bool) {
        if !condition {
            fail(message)
        }
    }
    public static func assertFalse(message: String? = nil, condition: Bool) {
        assertTrue(message, !condition)
    }
}

```

**세로 순서**

일반적으로 함수 호출 종속성은 아래방햘으로 유지하므로, 호출되는 함수를 호출하는 함수보다 뒤에 배치한다.
그러면 소스코드가 자연스럽게 고차원 -> 저차원으로 내려간다.
가장 중요한 개념은 가장 먼저 표현하고, 세세한 사항은 마지막에 표현한다.
그렇게하면 첫 함수 몇개만 읽어도 개념을 파악하기 쉬워질 것이다.

## 가로 형식 맞추기
---

대다수의 프로그래머들은 명백히 짧은 행을 선호하므로 짧은 행이 바람직하다.
Hollerith가 제안한 80자 제한은 다소 인위적이므로 조금 더 늘려도 좋다. 하지만 120자 이상을 넘어간다면 주의 부족이다.
필자 개인적으로는 120자 정도로 길이를 제한한다.

**가로 공백과 밀집도**

가로로는 공백을 사용해 밀집/느슨한 개념을 표현한다.
```swift
private func measureLine(line: String) {
    lineCount += 1

    // 흔히 볼 수 있는 코드인데, 할당 연산자 좌우로 공백을 주어 왼쪽,오른쪽 요소가 확실하게 구분된다.
    let lineSize = line.length()
    totalChars += lineSize

    // 반면 함수이름과 괄호 사이에는 공백을 없앰으로써 함수와 인수의 밀접함을 보여준다
	  // 괄호 안의 인수끼리는 쉼표 뒤의 공백을 통해 인수가 별개라는 사실을 보여준다.
    lineWidthHistogram.addLine(lineSize, lineCount)
    recordWidestLine(lineSize)
}
```

추가로 연산자의 우선순위를 강조하기 위해서도 공백을 사용한다 ```return b*b - 4*a*c```
하지만 Code Formatter등의 도구가 연산자 우선순위까지 고려하기 못하므로 공백을 임의로 넣어주더라도 사라지는 경우가 대부분.
Q. 그렇다면 괄호로 묶어주는 것이 더 바람직하기 않을까?

**가로 정렬**
```swift
public class FitNesseExpediter: ResponseSender {
    private var socker: Socker?
    private var input: InputStream?
    private var output: OutputStream?
    private var request: Request?
    private var response: Response?
    private var context: FitNesseContext?
    private var requestParsingTimeLimit: Int64?
    private var requestProgress: Int64?
    private var requestParsingDeadline: Int64?
    private var hasError: Bool?

    ...
}
```

보기엔 깔끔해 보일지 모르나, 코드가 엉뚱한 부분을 강조해 변수 유형을 자연스레 무시하고 이름부터 일게 된다.
게다가 Code Formatter 대부분들은 이렇게 해놔봤자 무시하고 원래대로 돌려놓는다 (내가 이 문제 때문에 씨름한 경험이 있음)
그러므로 선언문과 할당문을 별도로 정렬할 필요가 없다.
정렬이 필요할 정도로 목록이 길다면(Q. 여기서 말하는 목록은 인스턴스 변수 개수를 말하는 것인가?), 목록의 길이가 문제이지 정렬이 부족해서가 아니다. 선언부가 길다는 것은 클래스를 쪼개야 한다는 것을 의미 한다.

**들여쓰기**

들여쓰기를 잘 해놓으면 - _물론 그러도 있겠지만!_ 구조가 한 눈에 들어온다.

##### 들여쓰기 무시하기

간단한 if문, while문, 짧은 함수에서 들여쓰기를 무시하고픈 유혹이 생긴다. (정말?)
하지만 들여쓰기로 제대로 범위를 표현한 코드가 가독성이 더 높다. 유혹을 뿌리치자

```swift
// 이렇게 한행에 다 넣을 수 있다고 다 때려 박는 것이 멋있는 코드가 아니란 것! 알아두어라
public class CommentWidget: TextWidget {
    public static let REGEXP = "^#[^\r\n]*(?:(?:\r\n)|\n|\r)?"

    public init(parent: ParentWidget, text: String) { super.init(parent: parent, text: text) }
    public func render() -> String throws { return "" }
}
```

```swift
// 한줄이라도 정성스럽게 들여쓰기로 감싸주자. 가독성을 위해
public class CommentWidget: TextWidget {
    public static let REGEXP = "^#[^\r\n]*(?:(?:\r\n)|\n|\r)?"

    public init(parent: ParentWidget, text: String) { 
      super.init(parent: parent, text: text) 
    }
    public func render() -> String throws { 
      return "" 
    }
}
```

**가짜 범위**

빈 while문이나 for문을 접할 때가 있다. 가능한한 피해야 되지만, 피하지 못 할 경우엔 빈 블록을 올바로 들여쓰고 괄호로 감싸라. 그렇지 않으면 찾을 수 없는 버그가 발생할지도...

## 팀 규칙
---

당연한 이야기들이 적혀있는 것 같지만.. 팀에 속해있다면, 
가장 우선시 되어야하고 선호해야할 규칙은 팀 규칙이다.
처음 팀이 이루어졌다면 코딩을 시작하기 전,
코딩 스타일을 의논하여(괄호를 어디에 넣을지, 네이밍은 어떻게 할지 등) IDE Formatter로 지정하여 구현하는 것이 옳은 방식이다.
**좋은 소프트웨어 시스템은 읽기 쉬운 문서로 이뤄지고, 읽기 쉬운 문서는 스타일이 일관적이고 매끄러워야 한다.**

## Bob의 형식 규칙

```swift
public class CodeAnalyzer: SwiftFileAnalysis {
    private var lineCount: Int? { 
        get { return lineCount }
    }
    private var maxLineWidth: Int? {
        get { return maxLineWidth }
    }
    private var widestLineNumber: Int? {
        get { return widestLineNumber }
    }
    private var lineWidthHistogram: LineWidthHistogram?{
        get { return lineWidthHistogram }
    }
    private var totalChars: Int?

    public init() {
        lineWidthHistogram = LineWidthHistogram()
    }

    public static func findSwiftFiles(parentDirectory: File) -> [File] {
        var files: [File] = []
        findSwiftFiles(parentDirectory: parentDirectory, files: &files)
        return files
    }

    private static func findSwiftFiles(parentDirectory: File, inout files: [File]) {
        for file in parentDirectory.listFiles() {
            if file.name.endsWith(".swift") {
                files.append(file)
            } else if file.isDirectory {
                findSwiftFiles(parentDirectory: file, files: &files)
            }
        }
    }

    public func analyzeFile(swiftFile: File) throws {
        let br = BufferedReader(file: swiftFile)
        while let line = br.readLine() {
            measureLine(line)
        }
    }

    private func measureLine(line: String) {
        lineCount += 1
        let lineSize = line.length()
        totalChars += lineSize
        lineWidthHistogram?.addLine(lineSize, lineCount)
        recordWidestLine(lineSize)
    }

    private func recordWidestLine(lintSize: Int) {
        if lineSize > maxLineWidth {
            maxLineWidth = lineSize
            widestLineNumber = lineCount
        }
    }

    public func getMeanLineWidth() -> Double {
        return Double(totalChars!) / Double(lineCount!)
    }

    public func getMedianLineWidth() -> Int {
        let sortedWidths = getSortedWidths()
        var cumulativeLineCount = 0
        for width in sortedWidths {
            cumulativeLineCount += lineCountForWidth(width)
            if cumulativeLineCount > lineCount! / 2 {
                return width.width
            }
        }
        throw CustomError(message: "Cannot get here")
    }

    private func lineCountForWidth(width: Int) -> Int {
        return lineWidthHistogram?.getLinesForWidth(width)?.count ?? 0
    }

    private func getSortedWidths() -> [Int] {
        let widths: Set<Int> = lineWidthHistogram?.getWidths() ?? []
        var sortedWidths = Array(widths)
        return Array(sortedWidths.sorted())
    }
}
