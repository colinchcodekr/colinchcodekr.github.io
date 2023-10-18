---
layout: post
title: "[javascript] JSON.stringify()와 JSON.parse()의 차이점"
description: " "
date: 2023-10-18
tags: [javascript]
comments: true
share: true
---

자바스크립트에서 JSON.stringify() 함수와 JSON.parse() 함수는 각각 JSON 문자열을 생성하고, JSON 문자열을 자바스크립트 객체로 변환하는 역할을 합니다. 이 둘은 JSON 데이터를 다룰 때 매우 유용한 함수이지만, 각각의 역할과 사용법에는 몇 가지 차이점이 있습니다.

## JSON.stringify()

JSON.stringify() 함수는 자바스크립트 객체를 JSON 포맷의 문자열로 변환하는 기능을 합니다. 즉, 객체를 직렬화하여 문자열로 반환합니다. 이 함수는 다음과 같은 형태로 사용합니다.

```javascript
let obj = {
  name: "John",
  age: 30,
  city: "New York"
};

let jsonString = JSON.stringify(obj);
console.log(jsonString); // {"name":"John","age":30,"city":"New York"}
```
JSON.stringify() 메서드는 객체의 프로퍼티를 JSON 형식으로 변환합니다. 이 때, 객체의 프로퍼티가 함수 또는 심볼 값인 경우에는 해당 프로퍼티는 JSON.stringify() 함수에 의해 무시됩니다.

## JSON.parse()

JSON.parse() 함수는 JSON 포맷의 문자열을 자바스크립트 객체로 변환하는 기능을 합니다. 즉, 문자열을 역직렬화하여 객체로 반환합니다. 이 함수는 다음과 같은 형태로 사용합니다.

```javascript
let jsonString = '{"name":"John","age":30,"city":"New York"}';

let obj = JSON.parse(jsonString);
console.log(obj.name); // John
console.log(obj.age); // 30
console.log(obj.city); // New York
```

JSON.parse() 메서드는 JSON 포맷의 문자열을 자바스크립트 객체로 변환합니다. 이 때, 문자열이 유효한 JSON 형식이 아닌 경우에는 에러가 발생합니다.

## 주의할 점

JSON.stringify() 함수와 JSON.parse() 함수를 사용할 때에 주의할 점이 몇 가지 있습니다.

첫째, JSON.stringify() 함수는 변환 중에 객체의 순환 참조(circular reference)를 처리하지 못합니다. 따라서 변환하려는 객체에 순환 참조가 있는 경우, TypeError가 발생할 수 있습니다.

둘째, JSON.parse() 함수에 넘겨줄 문자열이 유효한 JSON 형식이 아닌 경우, SyntaxError가 발생합니다. 따라서 JSON.parse() 함수를 사용하기 전에 문자열이 유효한 JSON 형식인지 확인하는 것이 좋습니다.

## 결론

JSON.stringify() 함수와 JSON.parse() 함수는 자바스크립트에서 JSON 데이터를 다루는 데 매우 유용하게 사용됩니다. JSON.stringify()는 객체를 문자열로 변환하고, JSON.parse()는 문자열을 객체로 변환합니다. 이 두 함수를 올바르게 사용하면 JSON 데이터를 쉽게 처리할 수 있습니다.

> 참고: [MDN Web Docs - JSON.stringify()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
> 참고: [MDN Web Docs - JSON.parse()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)