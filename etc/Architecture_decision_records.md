# Architecture Decision Records
소프트웨어를 만들 떄 Software Requirements Specification (SW 요구사항 명세)의 baseline이 정해지면 Architecture 설계 단계에 들어서며, 이떄 중요한 결정들을 한다.
어떤 언어를 쓸지부터 어떤 framework/library, architecture pattern 사용할지 등 이후 개발의 방향을 정하게 된다.

구현 단계에서 소스 코드는 버전 관리를 철저히 하면서, 정작 이 Architecture Design 단계에서는 산출물 정도만 (SDS, Software Design Specifiation) 있지, 그 결정을 하기까지의 이력 관리는 보통 간과한다.
SW 프로젝트가 변경없이 가는 것은 매우 드문 경우인지라, 변경에 대한 history를 모르면 같은 실수를 반복하기도 하고, 인원이 바뀐 경우에도 시간이 적지 않게 걸린다.

이때 Architecture Decision Records이 있으면 시행착오를 줄이고, 새로 Join한 사람도 ADR을 보면서 따라가기가 그나마 수월하다.

## ADR 작성방법
마크다운 템플릿은 여러개인데 그중 하나를 예시로하면

```md
## Title
Date

## Status

## Context

## Decision

## Consequences
```

Title : 가능하면 짧고 간결한 문구로 ADR의 제목

Status : `PROPOSED`, `ACCEPTED`, `SUPERSEDED`로 

Context : 문제에 대한 설명 및 가능한 대체 솔루션

Dicision : 정당화 (이유)

Consequences : 결정의 장단점 및 영향

예시
```md
# 3. spa mobile web framework
Date: 2021-03-26

## Status
Accepted

## Context
고객은 React, Vue중 learning curve가 완만하여 유지보수가 용이할 것이라는 이유로 Vue 선호
Concerning points
- 인력 소싱 : Vue 경력 인력이 없다
- 협력사에서 sourcing된 개발자의 의견을 물었을 때 자사에서 leading을 하면 Vue 개발을 배우며 할 수 있다는 답변
- 개발 기간 : 리브의 기존 화면(200본)을 대부분 재개발해야 하는데, 기간내 가능할 것인가?
Vue 2 or 3
- Vue.js 3.0이 release되었지만 아직 대부분의 component들이 아직 Vue2까지만 지원하여, 2021 말까지 Vue3로 가는 것은 위험하다
- 기존 SPA 솔루션 사용 방안
  - JSP와 jQuery 기반 코드로 Techinical Debt를 안고 가야 함

## Decision
Vue.js 2.0을 SPA framework으로 택하여 개발한다

## Consequences
Benefits
- 고객 요청 사항 만족
- 충분한 개발 참고 사례 구글 검색 가능
- 향후 유지 보수 용이
Risks and Migigation
- Vue 경력 없는 개발 인력
-> 큰 구조를 자사 인원이 잡고, 초반 집중 교육과 Code Review를 통해 개발 역량 키운다
- Vue publishing이 없는 디자이너
-> Figma로 component 디자인, publishing하고 storybook을 통해 개발자와 협업한다
```

> References by https://sungyong.medium.com/architecture-decision-records-adr-실무-적용-45fc0dad090