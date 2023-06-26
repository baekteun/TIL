# View Drawing Cycle?
> View가 처음 표시되거나 일부를 다시 그려야 할 때, 화면에 그려지는 Cycle

1. View가 로드되면 시스템이 UIView에게 `draw(_:)` 메서드를 통해 컨텐츠를 그려달라고 요청
2. 시스템은 이 컨텐츠의 스냅샷을 캡쳐하고, 해당 스냅샷을 View의 시각적 표현으로 사용
3. 컨텐츠가 바뀌었다면 View가 변경되었음을 시스템에 알림 (SetNeedsLayout, SetNeedsDisplay, layoutIfNeeded 등)
4. 다음 Drawing Cycle에서 업데이트 요청을 받은 View를 업데이트
1번부터 계속 반복

## View 컨텐츠 변경 관련한 업데이트 트리거 종류
- `setNeedsLayout()`
  - View의 레이아웃(크기 및 위치)이 변경되었음을 시스템에 알림
  - 다음 Drawing Cycle에 `layoutSubviews()` 메서드를 자동 호출
- `setNeedsDisplay()`
  - View의 컨텐츠가 변경되었음(Drawing이 필요함)을 시스템에 알림
  - 다음 Drawing Cycle에 `draw(_:)` 메서드를 자동 호출
- `layoutIfNeeded()`
  - `setNeedsLayout()`과 같은 기능
  - 다만, `setNeedsLayout()`은 다음 Drawing Cycle에 `layoutSubviews()`를 호출하지만, `layoutIfNeeded()`는 즉시 실행
- `displayIfNeeded()`
  - `setNeedsDisplay()`와 같은 기능
  - 다만, `setNeedsDisplay()`는 다음 Drawing Cycle에 `draw(_:)`를 호출하지만, `displayIfNeeded()`는 즉시 실행

## View가 화면에 그려지는 원리
- View는 Constraint 값을 이용해 Layout(Size, Position)을 결정
- 결정된 Layout을 기반으로 Drawing 정의
- View는 모두 사각형으로 그려지므로, 메서드도 `draw(_ rect:)` 로 정의된 것
![](https://github.com/GSM-MSG/GCMS-iOS/assets/74440939/c2bc304d-b131-4a82-9df6-32ef29736992)

## 알아두어야 할 점
- View의 Drawing은 on-demand 방식으로 요청 필요에 의해 발생하는 것이다.
- layoutIfNeeded는 다음 사이클을 기다리지 않고 즉시 실행되기에 애니메이션 효과처럼 View가 변한다 (Drawing Cycle에 따라 일괄적으로 확 바뀌는게 아님)
- View가 처음 로드되거나 변경으로 다시 그릴 때 draw()를 호출해야 하는데, 시스템이 이를 호출하도록 해야한다. (직접 draw 호출 금지!)


## References
- https://developer.apple.com/library/archive/documentation/2DDrawing/Conceptual/DrawingPrintingiOS/GraphicsDrawingOverview/GraphicsDrawingOverview.html#//apple_ref/doc/uid/TP40010156-CH14-SW1
- https://green1229.tistory.com/67