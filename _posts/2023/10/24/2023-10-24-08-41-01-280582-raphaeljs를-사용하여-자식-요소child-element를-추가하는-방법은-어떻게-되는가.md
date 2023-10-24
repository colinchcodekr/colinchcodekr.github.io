---
layout: post
title: "[javascript] Raphael.js를 사용하여 자식 요소(child element)를 추가하는 방법은 어떻게 되는가?"
description: " "
date: 2023-10-24
tags: [javascript]
comments: true
share: true
---
Raphael.js는 SVG 기반의 자바스크립트 라이브러리로, 그래픽을 생성하고 조작하는 데 사용됩니다. 자식 요소를 추가하는 방법은 다음과 같습니다:

1. Raphael 객체를 생성합니다.
```javascript
var paper = Raphael('elementId', width, height);
```
2. 부모 요소를 생성하고 위치를 지정합니다.
```javascript
var parent = paper.rect(x, y, width, height);
```
3. 자식 요소를 생성하고 위치를 지정한 뒤, 부모 요소에 추가합니다.
```javascript
var child = paper.rect(x, y, width, height);
parent.append(child);
```
위 예시에서는 사각형 요소를 생성하여 부모와 자식으로 사용하였습니다. 자세한 내용은 Raphael.js의 공식 문서 [^1^]를 참조하시기 바랍니다.

[^1^]: http://dmitrybaranovskiy.github.io/raphael/ "Raphael.js 공식 문서"