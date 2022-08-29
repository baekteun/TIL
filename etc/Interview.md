# bounds와 frame의 차이점을 설명하시오.
## frame의 의미
- The frame rectangle, which describes the view’s location and size in its superview’s coordinate system.
- SuperView의 좌표계에서의 View의 위치와 크기를 나타낸다.
- SuperView는 자신의 부모View (RootView가 아님)

### frame의 origin
- SuperView의 원점으로 얼마 떨어져있는가를 의미.

### frame의 size
- View 영역을 모두 감싸는 사각형으로 나타낸 것.
- View를 회전시키면 size도 변한다. 이런식으로 size가 변경되면 origin도 변경될 수 있다.

## bounds의 의미
- The bounds rectangle, which describes the view’s location and size in its own coordinate system.
- 자신의 좌표계에서의 View의 위치와 크기를 나타낸다

### bounds의 origin
- 자신의 좌표계를 기준으로 삼아서 처음에는 (0, 0)으로 초기화된다.

### bounds의 size
- View 자체의 영역을 나타낸 것.
- View가 회전하든 안하든 자신의 원점이 곧 좌표의 시작점.

<br>

## 정리
- origin (x, y) 기준점
  - frame: SuperView의 좌표계
  - bounds: 자신의 좌표계
- size (width, height) 기준
  - frame: View의 좌표계
  - bounds: View의 영역 그 자체

<br>
<br>

# 실제 디바이스가 없을 경우 할 수 있는 것과 없는 것.

## 하드웨어
- 가속도 센서, 가압계 센서, 주변광 센서, GPS 센서 기능을 이용 불가.
- 마우스로 시뮬레이터의 터치를 하기 때문에 두 손가락으로 하는 줌인 줌아웃 등의 기능을 테스트 하기 쉽지 않다.
- 카메라를 이용할 수 없다.
- 마이크를 지원하지 않는다.
- 전화기능을 사용할 수 없다.

## API
- Apple의 푸시알림 받기/보내기 불가.
- 사진,연락처,캘린더에 액세스하기 위해 개인 정보 보호 알림을 지원하지 않습니다.
- Handoff 기능을 지원하지 않습니다.
- MessageUI 기능을 지원하지 않습니다

## 외
- 맥의 성능이 아이폰의 성능보다 훨씬 뛰어나 CPU나 메모리 부담이 얼마나 되는지 알 수 없습니다.
- 네트워크 속도 테스를 할 수 없습니다.
-  페이스 아이디는 직접 얼굴 인식은 안되지만 인식됨,안됨 처리는 해볼 수 있습니다.

<br>
<br>

# 앱의 콘텐츠나 데이터를 저장, 보관하는 특별한 객체

## UserDefaults
- Key-Value 쌍으로 저장하는 인터페이스 이다. 런타임 시 개체를 이용하여 기본 DB에서 사용하는 기본값을 읽어오기 때문에 값이 필요할 떄 마다 DB를 열 필요가 없다.
- 대용량의 데이터보다 자동로그인 여부, 아이디, 환경설정에서의 설정 데이터 값과 같은 단일데이터를 등을 저장한다.

## CoreData
- 객체 그래프를 관리하기 위한 Framework이다.
- SQLite와 같이 테이블을 이용하지 않고 객체를 생성하여 데이터를 운영하기에 더 많은 저장공간과 메모리를 필요로 한다. 그렇지만 더욱 빠르게 데이터를 가져온다.
- Data Model을 생성한 후 Entity를 생성한다.

## SQLite
- Swift에서 특별한 설치없이 바로 사용할 수 있다.
- C언어로 작성되어 있기에 매우 가벼운 것이 특징이며, 전체 DB를 디스크파일 1개에 저장하고, 설정 자체가 매우 간편하기에 관리하기에 수월하다.
- SQLite는 iOS, Android, Linux, Window 등과 같이 다양한 운영체제에서 사용된다.
- 수많은 프로세스와 스레드의 접근으로부터 안전하다.

## Realm
- SQLite와 같이 오픈소스이며, 모바일에 최적화된 라이브러리이다. SQLite, CoreData보다 속도가 빠르고 성능면에서 더 우수하다.
- 많은 작업들을 처리하기 위해 코드가 많이 필요하지 않으며, 메인 스레드에서 데이터의 읽기, 쓰기 작업을 모두 할 수 있어 편리하다.
- 대용량의 데이터에 대해 무료로 사용할 수 있으며, 용량이 적고 큼에 상관없이 속도와 성능이 유지된다.


# 앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?
- UIViewController 
UIKit앱의 뷰 계층 구조를 관리하는 객체이다.

<br>
<br>

# App thinning
- App이 디바이스에 설치될 때, 앱스토어와 운영체제가 디바이스의 특성에 맞게 설치되도록 하는 `설치 최적화 기술`을 의미한다.
- 최소한의 디스크 사용과 빠른 다운로드를 제공할 수 있다.
- App thinning은 Slicing, Bitcode, on-demand-resource가 있다.

<br>
<br>

# 앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가?
- UIApplicationMain함수는 앱의 라이프 사이클을 시작하는 함수.
- UIApplication 객체를 만든다.

<br>
<br>

# @Main에 대해서 설명하시오.
- 타입 기반의 프로그램 진입점.
- 탑 레벨의 코드 작성(main함수) 대신 single type에 @main 속성을 사용 가능.

<br>
<br>

# 앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요?
foreground: 리소스에 대해 background앱 보다 높은 우선순위를 가지고 리소스를 사용할 수 있도록 필요에 따라 background앱을 종료 시킨다.
background: 가능한 적은 메모리 공간을 사용해야한다.