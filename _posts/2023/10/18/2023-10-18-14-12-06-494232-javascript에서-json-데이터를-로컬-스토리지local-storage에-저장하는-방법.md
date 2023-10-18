---
layout: post
title: "[javascript] JavaScript에서 JSON 데이터를 로컬 스토리지(local storage)에 저장하는 방법"
description: " "
date: 2023-10-18
tags: [javascript]
comments: true
share: true
---

로컬 스토리지(local storage)는 웹 브라우저에서 제공하는 저장소입니다. JavaScript를 사용하여 JSON 데이터를 로컬 스토리지에 저장하고 불러오는 방법에 대해 알아보겠습니다.

## JSON 데이터를 로컬 스토리지에 저장하기
JSON 데이터를 로컬 스토리지에 저장하기 위해서는 `JSON.stringify()` 메서드를 사용하여 데이터를 문자열로 변환해야 합니다. 다음은 간단한 예제 코드입니다.

```javascript
var data = { name: "John", age: 30 };
var jsonData = JSON.stringify(data); // JSON 데이터를 문자열로 변환

localStorage.setItem("userData", jsonData); // 로컬 스토리지에 데이터 저장
```

위의 코드에서 `data` 객체는 JSON 데이터를 저장할 변수입니다. `JSON.stringify()` 메서드를 사용하여 데이터를 문자열로 변환한 후, `localStorage.setItem()` 메서드를 사용하여 `userData`라는 키로 데이터를 로컬 스토리지에 저장합니다.

## 로컬 스토리지에서 JSON 데이터 가져오기
로컬 스토리지에서 저장된 JSON 데이터를 가져오려면 `JSON.parse()` 메서드를 사용하여 문자열을 JSON 객체로 변환해야 합니다. 다음은 예제 코드입니다.

```javascript
var jsonData = localStorage.getItem("userData"); // 로컬 스토리지에서 데이터 가져오기
var data = JSON.parse(jsonData); // 문자열을 JSON 객체로 변환

console.log(data.name); // "John"
console.log(data.age); // 30
```

위의 코드에서 `localStorage.getItem()` 메서드를 사용하여 `userData` 키로 저장된 JSON 데이터를 가져옵니다. 그 후 `JSON.parse()` 메서드를 사용하여 문자열을 JSON 객체로 변환합니다. 변환된 JSON 객체를 사용하여 데이터를 활용할 수 있습니다.

## 참고 자료
- [MDN Web Docs: localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
- [MDN Web Docs: JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- [MDN Web Docs: JSON.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)