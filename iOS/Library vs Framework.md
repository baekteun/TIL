# Library
- 프로그램이 연결할 수 있는 패키징된 Object 파일들의 모음

# Framework
- 헤더파일, Localizable파일, 이미지, 문서와 같은 리소스까지 이 모든 것을 하나의 Bundle로 묶어 놓은 것
- Bundle: 서브 디렉토리 내부의 파일 디렉토리
- iOS에서 Bundle에 관련 파일을 하나의 패키지 (이미지, 컴파일된 코드)로 편리하게 함께 제공

Framework가 몸집이 크고 Library가 몸집이 작으며, Framework안에 Library가 속할 수 있음

## Static Library
1. 컴파일 시간에 
2. Static linker가 library 코드 + 앱 코드를 merge하고
3. 단일 executable file을 만든다.
4. 앱이 실행되면 library 코드 + 앱 코드가 앱 주소공간에 로드된다.

## Dynamic Library
1. 앱을 실행함
2. 앱 코드 + Dynamic library에 대한 참조가 앱 주소공간에 로드 된다. 
3. 참조를 이용해 Dynamic library를 로드함

> https://zeddios.tistory.com/1308
> https://ios-development.tistory.com/1004