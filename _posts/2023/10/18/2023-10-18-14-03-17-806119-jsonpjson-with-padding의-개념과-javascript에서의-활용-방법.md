---
layout: post
title: "[javascript] JSONP(JSON with Padding)의 개념과 JavaScript에서의 활용 방법"
description: " "
date: 2023-10-18
tags: [javascript]
comments: true
share: true
---

## 개요

JSONP는 JSON 데이터를 외부 도메인에서 로드할 때 발생하는 Same-Origin Policy(SOP) 제약을 우회하기 위한 기술입니다. 이 글에서는 JSONP의 개념과 JavaScript에서의 활용 방법을 소개하겠습니다.

## JSONP의 개념

Same-Origin Policy(SOP)는 웹 브라우저에서 동일한 도메인에서 로드된 문서 또는 스크립트만 서로 간에 상호작용할 수 있다는 보안 정책입니다. 이로 인해 외부 도메인에서 로드된 JSON 데이터에 접근하는 것이 제한됩니다. 하지만 JSONP는 이 제약을 우회하여 외부 도메인에서 로드된 JSON 데이터에 접근할 수 있도록 합니다.

JSONP는 동적 스크립트 태그(`<script>`)를 활용하여 데이터를 로드합니다. 서버 측에서는 JSON 데이터를 JavaScript 함수 호출로 전달하고, 클라이언트 측에서는 해당 함수를 실행하여 데이터를 처리합니다. 이로써 SOP 제약을 우회하고 다른 도메인에서 JSON 데이터를 가져올 수 있게 됩니다.

## JavaScript에서의 JSONP 활용 방법

JSONP는 JavaScript에서 외부 도메인에서 로드된 JSON 데이터에 접근하기 위해 사용됩니다. 다음은 JSONP를 사용하여 데이터를 로드하는 간단한 예제 코드입니다.

```javascript
function handleResponse(data) {
  console.log(data);
}

var script = document.createElement('script');
script.src = 'https://example.com/api/data?callback=handleResponse';
document.head.appendChild(script);
```

위 코드에서 `handleResponse` 함수는 서버 측에서 전달되는 JSON 데이터를 처리하는 함수입니다. `script` 요소의 `src` 속성에 JSONP 요청 URL을 지정하고, `callback` 쿼리 파라미터에는 데이터가 로드된 후 실행될 JavaScript 함수의 이름을 지정합니다.

이렇게 하면 외부 도메인에서 로드된 JSON 데이터를 `handleResponse` 함수에서 처리할 수 있습니다. 클라이언트는 데이터를 정상적으로 가져오고 처리할 수 있게 됩니다.

## 결론

JSONP는 Same-Origin Policy 제약을 우회하여 외부 도메인에서 로드된 JSON 데이터에 접근하는 간단하고 효과적인 방법입니다. JavaScript를 사용하여 JSONP를 구현하면 다른 도메인에서 데이터를 로드하고 처리할 수 있습니다. 이를 활용하여 다양한 웹 애플리케이션 개발에 유용하게 활용할 수 있습니다.

## 참고 자료
- [MDN Web Docs: JSONP](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Fetching_data)
- [Wikipedia: JSONP](https://en.wikipedia.org/wiki/JSONP)