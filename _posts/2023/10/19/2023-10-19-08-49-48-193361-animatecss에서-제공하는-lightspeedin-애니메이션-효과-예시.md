---
layout: post
title: "[javascript] Animate.css에서 제공하는 lightSpeedIn 애니메이션 효과 예시"
description: " "
date: 2023-10-19
tags: [javascript]
comments: true
share: true
---

Animate.css는 웹 애니메이션 라이브러리로 다양한 애니메이션 효과를 쉽게 적용할 수 있게 해줍니다. 그 중에서도 lightSpeedIn 애니메이션 효과는 요소가 왼쪽에서 오른쪽으로 빠르게 슬라이드하는 효과를 제공합니다.

먼저, Animate.css를 HTML 문서에 추가합니다. `<head>` 태그 내에서 다음 코드를 추가해주세요:

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" />
```

이제 사용할 요소에 `animated` 클래스와 `lightSpeedIn` 클래스를 추가하여 애니메이션 효과를 적용해보겠습니다. 예를 들어, `<h1>` 태그에 애니메이션 효과를 적용하고 싶다면 다음과 같이 작성합니다:

```html
<h1 class="animated lightSpeedIn">안녕, 세계!</h1>
```

이제 웹 페이지를 열어본다면 "안녕, 세계!"라는 텍스트가 왼쪽에서 빠르게 슬라이드되는 애니메이션 효과를 확인할 수 있을 것입니다.

다른 Animate.css 애니메이션 효과도 동일한 방식으로 적용할 수 있습니다. 이를 통해 간편하게 다양한 웹 애니메이션을 만들어낼 수 있습니다.

참고: [Animate.css](https://animate.style/) 공식 웹사이트에서 제공하는 문서를 참고하시면 더 많은 애니메이션 효과를 확인할 수 있습니다.