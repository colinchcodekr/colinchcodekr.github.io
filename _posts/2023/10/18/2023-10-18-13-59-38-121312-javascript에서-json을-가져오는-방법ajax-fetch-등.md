---
layout: post
title: "[javascript] JavaScript에서 JSON을 가져오는 방법(ajax, fetch 등)"
description: " "
date: 2023-10-18
tags: [javascript]
comments: true
share: true
---

JavaScript에서 JSON 데이터를 가져오는 것은 웹 개발에서 자주 사용되는 기능 중 하나입니다. JSON은 JavaScript Object Notation의 약자로, 데이터를 효율적으로 저장하고 전송하기 위한 경량의 데이터 형식입니다. 이번 글에서는 JavaScript에서 JSON을 가져오는 여러 방법을 알아보겠습니다.

## 1. XMLHttpRequest를 이용한 AJAX

AJAX(Asynchronous JavaScript And XML)는 비동기적으로 서버와 통신하는 기술입니다. XMLHttpRequest 객체를 사용하여 서버로부터 JSON 데이터를 가져올 수 있습니다.

```javascript
var xhr = new XMLHttpRequest();
xhr.open('GET', 'http://example.com/data.json', true);
xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
    var json = JSON.parse(xhr.responseText);
    // 가져온 JSON 데이터 활용
  }
};
xhr.send();
```

위의 예제에서는 `GET` 메서드를 사용하여 `http://example.com/data.json`에서 JSON 데이터를 비동기적으로 가져오고, `JSON.parse` 함수를 사용하여 JSON 데이터를 JavaScript 객체로 변환합니다.

## 2. fetch API를 이용한 가져오기

fetch API는 AJAX를 좀 더 간편하게 사용할 수 있도록 제공되는 API입니다. fetch 함수를 사용하여 JSON 데이터를 가져올 수 있습니다.

```javascript
fetch('http://example.com/data.json')
  .then(function(response) {
    return response.json();
  })
  .then(function(data) {
    // 가져온 JSON 데이터 활용
  })
  .catch(function(error) {
    console.log('에러 발생:', error);
  });
```

위의 예제에서는 `fetch` 함수를 사용하여 `http://example.com/data.json`에서 JSON 데이터를 가져옵니다. `then` 메서드를 사용하여 응답(response) 객체를 JSON으로 변환하고, 다음 `then` 메서드를 사용하여 JSON을 활용합니다. `catch` 메서드를 사용하여 에러 처리를 할 수도 있습니다.

## 3. axios 라이브러리 사용

axios는 브라우저와 Node.js 모두에서 사용할 수 있는 HTTP 클라이언트 라이브러리입니다. axios를 사용하면 더욱 간편하게 JSON 데이터를 가져올 수 있습니다.

```javascript
axios.get('http://example.com/data.json')
  .then(function(response) {
    var json = response.data;
    // 가져온 JSON 데이터 활용
  })
  .catch(function(error) {
    console.log('에러 발생:', error);
  });
```

위의 예제에서는 `axios.get` 메서드를 사용하여 `http://example.com/data.json`에서 JSON 데이터를 가져옵니다. 응답 객체의 `data` 속성을 활용하여 JSON 데이터에 접근할 수 있습니다.

## 마무리

이번 글에서는 JavaScript에서 JSON 데이터를 가져오는 여러 방법을 알아보았습니다. AJAX를 위한 XMLHttpRequest, fetch API, 그리고 axios 라이브러리를 사용하여 JSON 데이터를 간편하게 가져올 수 있습니다. 각 방법을 잘 활용하여 웹 애플리케이션을 개발하는데 도움이 되기를 바랍니다.

---

## 참고 자료
- [MDN web docs: XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
- [MDN web docs: Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [axios GitHub Repository](https://github.com/axios/axios)