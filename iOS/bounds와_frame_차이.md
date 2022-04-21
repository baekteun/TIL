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

# 정리
- origin (x, y) 기준점
  - frame: SuperView의 좌표계
  - bounds: 자신의 좌표계
- size (width, height) 기준
  - frame: View의 좌표계
  - bounds: View의 영역 그 자체