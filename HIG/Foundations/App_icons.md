# App icons

### 독특하고 기억에 남는 아이콘은 경험의 목적과 개성을 전달하며 사람들이 App Store와 장치에서 앱이나 게임을 한 눈에 인식할 수 있도록 도와줍니다.

아름다운 앱 아이콘은 모든 Apple 플랫폼에서 사용자 경험의 중요한 부분이며 모든 앱과 게임에는 하나가 있어야 합니다. 각 플랫폼은 앱 아이콘에 대해 약간 다른 스타일을 정의하므로, 강력한 시각적 일관성과 메시징을 유지하면서 다양한 모양과 디테일 수준에 잘 적응하는 디자인을 만들어야합니다. 각 플랫폼의 아이콘을 만드는 데 도움이 되는 템플릿을 다운로드하려면 [Apple Design Resources](https://developer.apple.com/design/resources/)를 참조하십시오. 다른 유형의 아이콘을 만드는 방법에 대한 지침은 [icons](https://developer.apple.com/design/human-interface-guidelines/foundations/icons/)를 참조하십시오.

## 모범 사례
<Strong>단순함을 받아들이기</Strong>. 간단한 아이콘은 사람들이 이해하고 인식하기 쉬운 경향이 있습니다. 앱이나 게임의 본질을 포착하고, 이를 초점에 두고 icon을 만들고, 간단하고 독특한 방식으로 표현하는 개념이나 요소를 찾으세요. 식별하기 어려울 수 있고 특히 더 작은 크기로 아이콘을 진흙투성이로 보이게 할 수 있기 때문에 너무 많은 세부 사항을 추가하지 마십시오. 기본 이미지에 중점을 둔 간단한 배경을 선호합니다. 전체 아이콘을 콘텐츠로 채울 필요는 없습니다.

<Strong>여러 플랫폼에서 잘 작동하는 디자인을 만들어 편안함을 느끼도록 합니다.</Strong> 앱이나 게임이 하나 이상의 플랫폼에서 실행되는 경우, 모든 아이콘에 대해 유사한 이미지와 색상 팔레트를 사용하여 각 플랫폼에 적합한 스타일로 렌더링하세요. 예를 들어, iOS 및 watchOS에서 Mail 앱 아이콘은 파란색 배경에 흰색 봉투를 묘사하기 위해 간소화된 그래픽 스타일을 사용합니다. macOS는 비슷한 파란색 배경을 사용하여 봉투에 깊이와 디테일을 추가하여 현실적인 무게와 질감을 제공합니다.

<Strong>경험이나 브랜드의 필수적인 부분인 경우에만 텍스트를 포함하는 것을 선호합니다.</Strong> 아이콘의 텍스트는 종종 너무 작아서 쉽게 읽을 수 없고, 아이콘이 어수선하게 보일 수 있으며, 접근성이나 현지화를 지원하지 않습니다. 일부 컨텍스트에서는 앱 이름이 아이콘 근처에 나타나며, 그 안에 이름을 표시하는 것은 불필요합니다. 앱 이름의 첫 글자와 같은 mnemonic을 사용하면 사람들이 앱이나 게임을 인식하는 데 도움이 될 수 있지만, "Watch" 또는 "Play"와 같이 사람들에게 무엇을 해야 하는지 알려주는 불필요한 단어나 "New" 또는 "iOS용"와 같은 컨텍스트별 용어를 포함하지 마십시오.

<Strong>사진보다 그래픽 이미지를 선호하고 아이콘에서 UI 구성 요소를 복제하지 마세요.</Strong> 사진은 작은 크기로 볼 때 잘 작동하지 않는 디테일로 가득 차 있습니다. 사진을 사용하는 대신, 사람들이 알아차리길 원하는 기능을 강조하는 콘텐츠의 그래픽 표현을 만드세요. 마찬가지로, 앱에 사람들이 인식하는 인터페이스가 있다면, 표준 UI 구성 요소를 복제하거나 아이콘에 앱 스크린샷을 사용하지 마십시오.

<Strong>필요하다면, 사람들이 만날 수 있는 모든 크기로 멋지게 보이도록 아이콘을 조정하세요.</Strong> 예를 들어 App Store에는 큰 버전이 표시되지만, 시스템은 Spotlight 검색 결과, 설정 및 알림과 같은 장소에 작은 버전을 표시할 수 있습니다. iOS, iPadOS 및 watchOS에서 시스템은 1024×1024 px 앱 아이콘을 사용하여 다른 모든 크기를 생성할 수 있습니다. macOS 및 tvOS에서는 모든 크기를 제공해야 합니다. 시스템 생성 버전의 앱 아이콘을 포기하고 대신 자신만의 아이콘을 만들고 싶다면, 아이콘 크기가 줄어들면서 이미지가 선명하게 유지되도록 하십시오. 예를 들어, 세부 사항과 불필요한 기능을 제거하여 이미지를 단순화하고 기본 기능을 과장할 수 있습니다. 일반적으로, 앱 아이콘이 모든 맥락에서 시각적으로 일관되게 유지되도록 미묘한 변경을 하는 것이 가장 좋습니다.

![](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/images/app-icon-sizes_2x.png)

<Strong>당신의 아이콘을 full-bleed 정사각형 이미지로 디자인하세요.</Strong> 대부분의 플랫폼에서 시스템은 플랫폼의 미학에 맞게 아이콘 모서리를 자동으로 조정하는 마스크를 적용합니다. 예를 들어 watchOS는 원형 마스크를 자동으로 적용합니다. 예외는 macOS입니다: 시스템은 Mac Catalyst로 만든 앱의 아이콘에 둥근 직사각형 모양을 적용합니다, 당신은 올바른 모양으로 macOS 앱 아이콘을 만들어야 합니다. 각 플랫폼에 대한 앱 아이콘을 만드는 데 도움이 되는 다운로드 가능한 프로덕션 템플릿은 [Apple Design Resources](https://developer.apple.com/design/resources/) 를 참조하십시오.

<Strong>대체 앱 아이콘을 제공하는 것을 고려해 보세요.</Strong> iOS, iPadOS 및 tvOS에서 사람들은 앱이나 게임과의 연결을 강화하고 경험을 향상시킬 수 있는 대체 버전의 아이콘을 선택할 수 있습니다. 예를 들어, 스포츠 앱은 다른 팀에 대해 다른 아이콘을 제공할 수 있습니다. 당신이 디자인한 각 대체 앱 아이콘이 당신의 콘텐츠와 경험과 밀접한 관련이 있는지 확인하세요. 사람들이 다른 앱의 아이콘으로 착각할 수 있는 버전을 만들지 마세요. 사람들이 대체 아이콘으로 전환하고 싶을 때, 앱의 설정을 방문할 수 있습니다. 

```md
NOTE
기본 앱 아이콘과 마찬가지로, 대체 앱 아이콘은 앱 심사 대상이며 [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/#design)을 준수해야 합니다. 
```

<Strong>Apple 하드웨어 제품의 복제본을 사용하지 마세요.</Strong> Apple 제품은 저작권이 있으며 앱 아이콘에서 복제할 수 없습니다.

## 플랫폼 고려 사항

### iOS, iPadOS
<Strong>설정 아이콘에 오버레이나 테두리를 추가하지 마세요.</Strong> iOS는 설정의 흰색 배경에 잘 보이도록 모든 아이콘에 1픽셀 스트로크를 자동으로 추가합니다.

### macOS
macOS에서 앱 아이콘은 둥근 직사각형 모양, 전면 관점, 레벨 위치 및 균일한 드롭 섀도우를 포함한 일반적인 시각적 속성 세트를 공유합니다. macOS 디자인 언어에 뿌리를 둔 이러한 속성은 사람들이 macOS에서 기대하는 생생한 렌더링 스타일을 보여주면서 조화로운 사용자 경험을 제공합니다.

<Strong>사람들이 당신의 앱을 사용하여 무엇을 하는지 소통하기 위해 친숙한 도구를 묘사하는 것을 고려해 보세요.</Strong> 앱의 목적에 맞는 컨텍스트를 제공하려면 아이콘 배경을 사용하여 도구의 환경이나 영향을 미치는 항목을 묘사할 수 있습니다. 예를 들어, TextEdit 아이콘은 기계식 연필과 줄지어 있는 종이 한 장을 결합하여 실용적인 글쓰기 경험을 제안합니다. 도구의 상세하고 현실적인 이미지를 만든 후, 종종 배경 바로 위에 떠다니고 아이콘 경계를 약간 지나가도록 하는 것이 잘 작동합니다. 이렇게 하면, 도구가 배경과 시각적으로 통합되어 있고 둥근 직사각형 모양을 압도하지 않는지 확인하세요. 

![](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/images/app-icon-familiar-tool_2x.png)

<Strong>앱 아이콘에서 실제 물체를 묘사한다면, 물리적 재료로 만들어진 것처럼 보이게 하고 실제 질량을 갖도록 하세요.</Strong> 직물, 유리, 종이, 금속과 같은 물질의 특성을 복제하여 물체의 무게와 느낌을 전달하는 것을 고려해 보세요. 예를 들어, Xcode 앱 아이콘에는 스틸 헤드와 폴리머 그립이 있는 것처럼 보이는 망치가 있습니다.

![](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/images/app-icon-realistic-materials_2x.png)

<Strong>icon-design 템플릿에 그림자를 사용하세요.</Strong> app-icon [템플릿](https://developer.apple.com/design/resources/#macos-apps)에는 앱 아이콘이 다른 macOS 아이콘과 조정되는 데 도움이 되는 시스템 정의 드롭 섀도우가 포함되어 있습니다. 

<Strong>내부 그림자와 하이라이트를 사용하여 정의와 리얼리즘을 추가하는 것을 고려해 보세요.</Strong> 예를 들어, Mail 앱 아이콘은 그림자와 하이라이트를 모두 사용하여 봉투에 신뢰성을 부여하고 플랩이 약간 열려 있음을 나타냅니다. 텍스트 편집기 또는 Xcode와 같은 배경 위에 떠 있는 도구가 포함된 아이콘에서 내부 그림자는 깊이에 대한 인식을 강화하고 도구를 실제처럼 보이게 할 수 있습니다. 그림자와 하이라이트는 아이콘을 향하고 중앙 바로 위에 위치하고 약간 아래로 기울어진 광원을 제안해야 합니다.

<Strong>둥근 직사각형 이외의 모양을 제안하는 윤곽을 정의하지 마세요.</Strong> 드물게 기본 앱 아이콘 모양을 미세 조정하고 싶을 수도 있지만, 그렇게 하면 macOS에 속하지 않는 것처럼 보이는 아이콘을 만들 위험이 있습니다. 모양을 변경해야 하는 경우, 둥근 직사각형 실루엣을 계속 표현하는 미묘한 조정을 선호하십시오.

![](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/images/app-icon-consistent-shape_2x.png)

<Strong>기본 콘텐츠를 아이콘 그리드 경계 상자 안에 보관하십시오; 모든 콘텐츠를 외부 경계 상자 안에 보관하십시오.</Strong> 아이콘의 기본 콘텐츠가 아이콘 그리드 경계 상자를 넘어 확장되면, 위치가 어긋나 보이는 경향이 있다. 아이콘에 도구를 오버레이하면, 아래와 같이 도구의 상단 가장자리를 외부 경계 상자와 정렬하고 하단 가장자리를 내부 경계 상자와 정렬하는 것이 좋습니다. 그리드를 사용하여 아이콘 내에 항목을 배치하고 원과 같은 중앙에 있는 내부 요소가 시스템의 다른 아이콘과 일치하는 크기를 사용하도록 할 수 있습니다.

![](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/images/app-icon-layout-guides_2x.png)

### tvOS
tvOS 앱 아이콘은 2개에서 5개의 레이어를 사용하여 사람들이 집중할 때 깊이와 활력을 조성합니다. 지침은 [Layered images](https://developer.apple.com/design/human-interface-guidelines/foundations/images#layered-images)를 참조하십시오.

<Strong>적절한 레이어 분리를 사용하세요.</Strong> 아이콘에 로고가 포함되어 있다면, 배경에서 로고를 분리하세요. 아이콘에 텍스트가 포함되어 있다면, 시차 효과가 발생할 때 다른 레이어에 숨겨지지 않도록 텍스트를 전면으로 가져오세요.

![](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/images/icons-and-images-icon-structure_2x.png)

[video](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/images/icons-and-images-layering.mp4)

<Strong>그라디언트와 그림자를 조심스럽게 사용하세요.</Strong> 배경 그라디언트와 비네트는 시차 효과와 충돌할 수 있다. 그라디언트의 경우, 위에서 아래로, 밝고 어두운 스타일을 선호하세요. 그림자는 보통 배경 레이어로 구워지고 앱 아이콘이 고정되어 있을 때 보이지 않는 날카롭고 딱딱한 색조로 가장 잘 보입니다.

<Strong>다양한 불투명도 수준을 활용하여 깊이와 생동감을 높이세요.</Strong> 불투명도를 창의적으로 사용하면 아이콘이 돋보이게 될 수 있습니다. 예를 들어, 사진 아이콘은 중앙 장식품을 반투명 조각이 포함된 여러 레이어로 분리하여 디자인에 더 큰 생동감을 선사합니다.

<Strong>홈 화면 아이콘이 안전 구역 사양을 준수하는지 확인하세요.</Strong> 초점과 시차 동안, 시스템은 아이콘이 확장되고 움직일 때 앱 아이콘의 가장자리 주변의 콘텐츠를 자를 수 있습니다. 아이콘의 콘텐츠가 너무 단단히 잘리지 않도록 하려면, [Specifications > tvOS](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons#tvos-app-icon-sizes)와 같이 약간의 추가 공간을 허용하십시오.

### watchOS
watchOS 앱 아이콘은 원형이며 첨부된 텍스트가 표시되지 않습니다.

![](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/images/icon-and-image-large-icon-mail-dark_2x.png)

![](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/images/icon-and-image-large-icon-fitness-dark_2x.png)

![](https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons/images/icon-and-image-large-icon-settings-dark_2x.png)

<Strong>아이콘의 배경에 검은색을 사용하지 마세요.</Strong> 아이콘이 디스플레이 배경에 섞이지 않도록 검은색 배경을 밝게 하거나 테두리를 추가하세요. 

## 사양
### 앱 아이콘 속성
모든 플랫폼의 앱 아이콘은 PNG 형식을 사용하고 다음 색 공간을 지원합니다:

- Display P3 (wide-gamut color)
- sRGB (color)
- Gray Gamma 2.2 (grayscale)

앱 아이콘의 레이어, 투명도 및 모서리 반경은 플랫폼에 따라 다를 수 있습니다. 구체적으로:

<img width="553" alt="스크린샷 2022-06-20 오후 7 20 30" src="https://user-images.githubusercontent.com/74440939/174581377-ed478da2-becf-41a2-976d-9d343e8cafdd.png">

### 앱 아이콘 크기

#### iOS, iPadOS 앱 아이콘 크기

App Store에 표시하려면 1024x1024 픽셀 크기의 큰 버전의 앱 아이콘을 제공해야 합니다. 시스템이 큰 앱 아이콘을 자동으로 축소하여 다른 모든 크기를 생성하도록 할 수 있으며, 특정 크기로 아이콘의 모양을 사용자 정의하려면 여러 버전을 제공할 수 있습니다.

<img width="532" alt="스크린샷 2022-06-20 오후 7 21 28" src="https://user-images.githubusercontent.com/74440939/174581514-6064ba8d-7117-4d0f-a8c5-31d224a239aa.png">

#### macOS 앱 아이콘 크기

App Store의 경우, macOS 앱 아이콘의 1024x1024 px 버전을 만드세요. 또한, 다음 크기로 아이콘을 제공해야 합니다.

<img width="533" alt="스크린샷 2022-06-20 오후 7 22 01" src="https://user-images.githubusercontent.com/74440939/174581607-be8fddcc-fdb5-4b2d-9e38-6afdd4367f34.png">

#### tvOS 앱 아이콘 크기

App Store의 경우, tvOS 앱 아이콘의 1280x768 px 버전을 만드세요. 또한, 다음 크기로 아이콘을 제공해야 합니다.

<img width="513" alt="스크린샷 2022-06-20 오후 7 22 40" src="https://user-images.githubusercontent.com/74440939/174581739-cc05c2bb-b914-4433-8db2-1c157b6e740c.png">

<Strong>홈 화면 아이콘에서 안전 지대를 허용하는 것을 고려해 보세요.</Strong> 초점과 시차 동안, 아이콘이 확장되고 움직이면서 앱 아이콘의 가장자리 주변의 콘텐츠가 잘릴 수 있습니다. 아이콘의 콘텐츠가 너무 단단히 잘리지 않도록 하려면, 호흡 공간을 추가로 포함할 수 있습니다.

#### watchOS 앱 아이콘 크기

App Store의 경우, watchOS 앱 아이콘의 1024x1024 px 버전을 만드세요. 시스템이 이 버전을 다른 모든 크기로 자동으로 축소하도록 할 수 있으며, 특정 크기로 앱 아이콘의 모양을 사용자 정의하려면 다음 크기를 제공할 수 있습니다. 모든 크기 값은 @2x입니다.

<img width="524" alt="스크린샷 2022-06-20 오후 7 23 29" src="https://user-images.githubusercontent.com/74440939/174581861-90036eb6-d6e8-4b16-b5c3-36362ee6d27e.png">

연동된 iPhone 앱이 있다면, 다음 크기로 watchOS 앱 아이콘을 제공해야 합니다.

<img width="528" alt="스크린샷 2022-06-20 오후 7 23 53" src="https://user-images.githubusercontent.com/74440939/174581933-2dfcf88c-57e2-487f-a69d-6709c3545169.png">

> https://developer.apple.com/design/human-interface-guidelines/foundations/app-icons