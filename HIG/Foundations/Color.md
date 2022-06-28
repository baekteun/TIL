# 색

### 색상을 현명하게 사용하면 커뮤니케이션을 향상시키고, 브랜드를 불러일으키며, 시각적 연속성을 제공하며, 상태와 피드백을 전달하고, 사람들이 정보를 이해하는 데 도움이 됩니다.

이 시스템은 다양한 배경과 외관 모드에서 멋지게 보이는 색상을 정의하며, 진동와 접근성 설정에 자동으로 적응할 수 있습니다. 사람들은 시스템 색상에 익숙하며, 그것들을 사용하는 것은 디바이스에서 편안한 경험을 느낄 수 있게하는 편리한 방법입니다. 

또한 사용자 지정 색상을 사용하여 앱이나 게임의 시각적 경험을 향상시키고 독특한 개성을 표현할 수 있습니다. 다음 지침은 시스템 정의 또는 사용자 지정 색상을 사용 여부에 관계없이 사람들이 좋아하는 방식으로 색상을 사용하는 데 도움이 될 수 있습니다.

## 모범 사례

**게임 이외의 앱에서 색을 적게 사용하세요.** 비게임 앱에서 색상 과용은 커뮤니케이션을 덜 명확하게 만들고 산만해질 수 있습니다. 중요한 정보에 주의를 기울이거나 인터페이스 부분 간의 관계를 보여주기 위해 색상 터치를 사용하는 것을 선호합니다.

**다른 것을 의미하기 위해 같은 색을 사용하지 마세요.** 특히 상태나 상호 작용과 같은 정보를 전달하는 데 도움이 될 때 인터페이스 전반에 걸쳐 색상을 일관되게 사용하세요. 예를 들어, 앱은 사람들이 텍스트를 탭하여 더 많은 것을 볼 수 있음을 나타내기 위해 파란색을 사용할 수 있습니다. 앱이 대화형 텍스트에 파란색 이외의 색상을 사용하여 -- 쉐브론이나 화살표 아이콘 -- 과 같은 색상에 의존하지 않는 시각적 표시기를 사용하여 상호 작용을 통신하는 경우에도 혼란스럽습니다.

**앱의 색상이 밝고 어두운 모양 모드 모두에서 잘 작동하는지 확인하세요.** 항상 순수한 검은색 배경을 사용하는 watchOS를 제외하고, 플랫폼은 기본 조명 외관에 대한 어두운 대안을 제공합니다. 다크 모드는 모든 화면, 보기, 메뉴 및 컨트롤에 더 어두운 색상 팔레트를 사용하며, 전경과 배경색을 동적으로 혼합한 미묘한 효과인 활력을 증가시켜 전경 콘텐츠를 어두운 배경에서 돋보이게 할 수 있습니다. 시스템 색상은 자동으로 두 모드를 모두 지원합니다; 사용자 지정 색상을 사용하는 경우, 라이트 모드과 다크 모드를 모두 제공해야 합니다. 지침은 [Dark Mode](https://developer.apple.com/design/human-interface-guidelines/foundations/dark-mode)를 참조하십시오.

**다양한 조명 조건에서 앱의 색 구성표를 테스트하세요.** 화창한 날이나 희미한 빛 속에서 앱을 실행할 때 색상이 다르게 보일 수 있습니다. 대부분의 사용 사례에서 최적의 시청 경험을 제공하기 위해 색상을 조정하세요.

**디스플레이가 다른 디바이스에서 앱을 테스트하세요.** 예를 들어, 특정 iPhone, iPad 및 Mac 모델에서 사용할 수 있는 True Tone 디스플레이는 주변광 센서를 사용하여 디스플레이의 화이트 포인트를 자동으로 조정하여 현재 환경의 조명 조건에 맞게 조정합니다. 주로 읽기, 사진, 비디오 및 게임에 중점을 둔 앱은 화이트 포인트 적응 스타일을 지정하여 이 효과를 강화하거나 약화시킬 수 있습니다(개발자 지침은 [UIWhitePointAdaptivityStyle](https://developer.apple.com/documentation/bundleresources/information_property_list/uiwhitepointadaptivitystyle) 참조). 여러 브랜드의 HD 및 4K TV와 다른 디스플레이 설정으로 tvOS 앱을 테스트하세요. 시스템 설정 > 디스플레이에서 프로필을 선택하여 P3 및 표준 RGB(sRGB)와 같은 Mac의 다양한 색상 프로필을 사용하여 앱의 모양을 테스트할 수도 있습니다. 지침은 [Color Management](#색상-관리)를 참조하십시오.

**아트워크와 반투명성이 주변 색상에 어떤 영향을 미치는지 생각해 보세요.** 아트워크의 변화는 때때로 시각적 연속성을 유지하고 인터페이스 요소가 압도적이거나 압도당하는 것을 방지하기 위해 주변 색상의 변화를 보증합니다. 예를 들어, 지도는 지도 모드에 있을 때 밝은 색 구성표를 표시하지만 위성 모드에서는 어두운 색 구성표로 전환합니다. 도구 모음과 같은 반투명 요소 뒤에 배치하거나 적용할 때도 색상이 다르게 나타날 수 있습니다.

**앱에서 사람들이 색상을 선택할 수 있다면, 가능한 경우 시스템에서 제공하는 색상 컨트롤을 선호하세요.** 내장된 색상 선택기를 사용하면 사람들이 모든 앱에서 액세스할 수 있는 색상 세트를 저장할 수 있도록 하는 것 외에도 일관된 사용자 경험을 제공합니다. 개발자 지침은 [NSColorPanel](https://developer.apple.com/documentation/appkit/nscolorpanel) (macOS), [UIColorWell](https://developer.apple.com/documentation/uikit/uicolorwell) 및 [UIColorPickerViewController](https://developer.apple.com/documentation/uikit/uicolorpickerviewcontroller) (iOS, iPadOS 및 Mac Catalyst)를 참조하십시오.

## 포용적인 색상

**물체를 구별하거나, 상호 작용을 나타내거나, 필수 정보를 전달하기 위해 색상에만 의존하지 마세요.** 색을 사용하여 정보를 전달할 때, 색맹이나 기타 시각 장애가 있는 사람들이 이해할 수 있도록 다른 방법으로 동일한 정보를 제공해야 합니다. 예를 들어, 라벨이나 글리프 모양을 사용하여 물체나 상태를 식별할 수 있습니다.

**앱에서 콘텐츠를 인식하기 어렵게 만드는 색상을 사용하지 마세요.** 예를 들어, 대비가 불충분하면 아이콘과 텍스트가 배경과 혼합되어 콘텐츠를 읽기 어렵게 만들 수 있으며, 색맹인 사람들은 일부 색상 조합을 구별하지 못할 수도 있습니다. 지침은 [Color and effects](https://developer.apple.com/design/human-interface-guidelines/foundations/accessibility/#color-and-effects)를 참조하십시오.

**사용하는 색상이 다른 국가와 문화에서 어떻게 인식될 수 있는지 생각해 보세요.** 예를 들어, 빨간색은 일부 문화권에서 위험을 전달하지만, 다른 문화권에서는 긍정적인 의미를 가지고 있다. 앱의 색상이 의도한 메시지를 보내는지 확인하세요.

## 시스템 색상

**앱에서 하드 코딩 시스템 색상 값을 피하세요.** 문서화된 색상 값은 앱 디자인 과정에서 참조를 위한 것입니다. 실제 색상 값은 다양한 환경 변수에 따라 릴리스에서 릴리스로 변동될 수 있습니다. [Color](https://developer.apple.com/documentation/swiftui/color)와 같은 API를 사용하여 시스템 색상을 적용하세요. 각 동적 색상은 모양이나 색상 값이 아닌 목적에 의해 의미론적으로 정의됩니다. 예를 들어, 일부 색상은 다른 수준의 계층에서 보기 배경을 나타내고 다른 색상은 라벨, 링크 및 구분 기호와 같은 전경 콘텐츠를 나타냅니다. 

**동적 시스템 색상을 복제하지 마세요.** 동적 시스템 색상(일부 중 일부는 패턴일 수 있음)은 다양한 환경 변수에 따라 릴리스에서 릴리스로 변동될 수 있습니다. 

**동적 시스템 색상의 의미론적 의미를 재정의하지 마세요.** 일관된 경험을 보장하고 향후 macOS의 모양이 바뀔 때 인터페이스가 멋지게 보이도록 하려면, 의도한 대로 동적 시스템 색상을 사용하세요.

## 색상 관리

색 공간은 RGB 또는 CMYK와 같은 색상 모델의 색상을 나타냅니다. 일반적인 색 공간은 sRGB와 디스플레이 P3입니다.

색상 프로필은 예를 들어 수학적 공식이나 색상을 숫자 표현에 매핑하는 데이터 테이블을 사용하여 색 공간의 색상을 설명합니다. 이미지는 장치가 이미지의 색상을 올바르게 해석하고 디스플레이에서 재현할 수 있도록 색상 프로필을 삽입합니다.

**이미지에 색상 프로파일을 적용하세요.** 색상 프로필은 앱의 색상이 다른 디스플레이에서 의도한 대로 표시되도록 도와줍니다. sRGB 색 공간은 대부분의 디스플레이에서 정확한 색상을 생성합니다.

**넓은 색상을 사용하여 호환되는 디스플레이의 시각적 경험을 향상시키세요.** 와이드 컬러 디스플레이는 sRGB보다 더 풍부하고 포화된 색상을 생산할 수 있는 P3 색 공간을 지원합니다. 결과적으로, 넓은 색을 사용하는 사진과 비디오는 더 생생하며, 넓은 색상을 사용하는 시각적 데이터와 상태 표시기가 더 의미가 있을 수 있습니다. 적절한 경우 픽셀당 16비트(채널당)의 디스플레이 P3 색상 프로파일을 사용하고 PNG 형식으로 이미지를 내보냅니다. 넓은 색상 이미지를 디자인하고 P3 색상을 선택하려면 와이드 컬러 디스플레이를 사용해야 합니다.

**필요한 경우 색 공간별 이미지 및 색상 변화를 제공하세요 .** 일반적으로, P3 색상과 이미지는 sRGB 디스플레이에서 잘 나타납니다. 가끔, sRGB 디스플레이에서 볼 때 두 가지 매우 유사한 P3 색상을 구별하기 어려울 수 있습니다. P3 색상을 사용하는 그라디언트는 때때로 sRGB 디스플레이에 잘린 것처럼 보일 수 있습니다. 이러한 문제를 피하고 넓은 색상과 sRGB 디스플레이 모두에서 시각적 충실도를 보장하기 위해 Xcode 프로젝트의 자산 카탈로그를 사용하여 각 색 공간에 대해 다양한 버전의 이미지와 색상을 제공할 수 있습니다.

자세한 내용은 [How to start designing assets in Display P3](https://developer.apple.com/news/?id=5cda5ipr)을 참조하십시오.

## 플랫폼 고려 사항

### iOS, iPadOS

iOS는 시스템 및 그룹화된 두 가지 동적 배경색을 정의하며, 각 색상에는 정보의 계층 구조를 전달하는 데 도움이 되는 기본, 보조 및 3차 변형이 포함되어 있습니다. 일반적으로 그룹화된 테이블 보기가 있을 때 그룹화된 배경색([systemGroupedBackground](https://developer.apple.com/documentation/uikit/uicolor/3173145-systemgroupedbackground), [secondarySystemGroupedBackground](https://developer.apple.com/documentation/uikit/uicolor/3173138-secondarysystemgroupedbackground) 및 [tertiarySystemGroupedBackground](https://developer.apple.com/documentation/uikit/uicolor/3173155-tertiarysystemgroupedbackground))을 사용하십시오. 그렇지 않으면 시스템 배경색 세트([systemBackground](https://developer.apple.com/documentation/uikit/uicolor/3173140-systembackground), [secondarySystemBackground](https://developer.apple.com/documentation/uikit/uicolor/3173137-secondarysystembackground) 및 [tertiarySystemBackground](https://developer.apple.com/documentation/uikit/uicolor/3173154-tertiarysystembackground))를 사용하십시오.

두 배경색 세트 모두 일반적으로 변형을 사용하여 다음과 같은 방법으로 계층 구조를 나타냅니다:

- 전체 보기의 기본

- 전체 보기 내에서 콘텐츠나 요소를 그룹화하는 데 보조

- 보조 요소 내에서 콘텐츠나 요소를 그룹화하기 위한 3차

Foreground 콘텐츠의 경우, iOS는 다음과 같은 동적 색상을 정의합니다:

### macOS

macOS는 다음과 같은 동적 시스템 색상을 정의합니다 (표준 색상 패널의 개발자 팔레트에서도 볼 수 있습니다):

**앱 악센트 색상**

macOS 11부터 악센트 색상을 지정하여 앱 버튼의 모양, 선택 강조 표시 및 사이드바 아이콘을 사용자 정의할 수 있습니다. 이 시스템은 일반 > 악센트 색상 설정의 현재 값이 다색일 때 악센트 색상을 적용합니다.

![](https://developer.apple.com/design/human-interface-guidelines/foundations/color/images/app-accent-colors-podcasts_2x.png)

![](https://developer.apple.com/design/human-interface-guidelines/foundations/color/images/app-accent-colors-podcasts-preferences_2x.png)

사람들이 악센트 색상 설정을 다색 이외의 값으로 설정하면, 시스템은 앱 전체의 관련 항목에 선택한 색상을 적용하여 악센트 색상을 대체합니다. 예외는 지정한 고정 색상을 사용하는 사이드바 아이콘입니다. 고정 색상 사이드바 아이콘은 의미를 제공하기 위해 특정 색상을 사용하기 때문에, 사람들이 악센트 색상 설정의 값을 변경할 때 시스템은 색상을 무시하지 않습니다. 지침은 [Sidebars](https://developer.apple.com/design/human-interface-guidelines/components/navigation-and-search/sidebars)를 참조하십시오.

### tvOS

**앱 로고와 조정되는 제한된 색상 팔레트를 선택하는 것을 고려해 보세요.** 색상의 미묘한 사용은 콘텐츠를 참고하면서 브랜드를 알리는 데 도움이 될 수 있습니다.

**초점을 나타내기 위해 색상만 사용하지 마세요.** 미묘한 스케일링과 반응형 애니메이션은 요소가 초점을 맞출 때 상호 작용을 나타내는 주요 방법입니다. 

### watchOS

**앱의 배경색에 순수한 검은색을 사용하세요.** 순수 블랙, 즉 #000000 육각은 Apple Watch 베젤과 매끄럽게 조화를 이루며 날카로운 화면의 환상을 만들어냅니다.

**사람들이 풀 컬러 대신 색조 모드를 사용하는 것보다 그래픽 컴플리케이션을 선호할 수 있다는 것을 인식하세요.** 이 시스템은 그래픽 컴플리케이션의 이미지, 게이지 및 텍스트에서 착용자가 선택한 색상을 기반으로 한 단일 색상을 사용할 수 있습니다. 지침은 [Complications](https://developer.apple.com/design/human-interface-guidelines/components/system-experiences/complications)을 참조하십시오.

> https://developer.apple.com/design/human-interface-guidelines/foundations/color