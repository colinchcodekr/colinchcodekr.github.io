---
layout: post
title: "[javascript] JavaScript onMouseOver 이벤트를 사용하여 요소의 스타일을 변경하는 방법"
description: " "
date: 2023-11-03
tags: [javascript]
comments: true
share: true
---

JavaScript를 사용하여 요소에 마우스를 올렸을 때 해당 요소의 스타일을 변경하는 방법을 알아보겠습니다.

```javascript
// HTML 요소 가져오기
var element = document.getElementById("elementId");

// onMouseOver 이벤트 핸들러 추가
element.onmouseover = function() {
  // 스타일 변경
  element.style.backgroundColor = "red";
  element.style.color = "white";
};
```

위의 예제 코드에서는 `elementId`라는 ID를 가진 HTML 요소를 가져온 후, `onmouseover` 이벤트 핸들러를 추가합니다. 이벤트 핸들러는 마우스가 해당 요소 위로 올라갈 때 실행됩니다.

이벤트 핸들러 내부에서는 요소의 `style` 속성을 사용하여 스타일을 변경할 수 있습니다. 위의 예제에서는 요소의 배경색을 빨간색으로, 텍스트 색상을 흰색으로 변경하고 있습니다.

이제 마우스를 해당 요소 위에 올리면 스타일이 변경됩니다.

---

## 참고 자료
- [MDN 웹 문서 - onMouseOver 이벤트](https://developer.mozilla.org/ko/docs/Web/API/Element/mouseover_event)