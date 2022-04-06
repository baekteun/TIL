# 왜 Clean Architecture를 사용하나?

1. ### Independent of Frameworks - 아키텍쳐는 소프트웨어 라이브러리의 존재에 의존하지 않음.
2. ### Testable - 비지니스 로직은 UI, DB, 웹 서버 또는 기타 외부 요소 없이 테스트할 수 있음.
3. ### Independent of UI - UI를 시스템을 변경하지 않고도 쉽게 변경할 수 있음. (ex: 비지니스 로직을 바꾸지 않고 웹 UI를 콘솔 UI로 바꿀 수 있음)
4. ### Independent of Database - 비지니스 로직이 DB에 바인딩되지 않음.
5. ### Independent of any external agency - 비지니스 로직은 외부세계(Out World)에 대해 전혀 알지 못함.
