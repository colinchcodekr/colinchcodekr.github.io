---
layout: post
title: "[javascript] JSON(JavaScript Object Notation)의 개념과 사용법"
description: " "
date: 2023-10-18
tags: [javascript]
comments: true
share: true
---

## 1. JSON이란?
JSON은 JavaScript Object Notation의 준말로, 데이터를 저장하고 교환하기 위한 경량의 데이터 형식입니다. JSON은 일반 텍스트로 작성되며, 사람과 기계 모두가 쉽게 읽을 수 있습니다. 또한, 다양한 프로그래밍 언어와 플랫폼에서 지원하고 사용할 수 있습니다.

## 2. JSON 형식
JSON은 이름-값 쌍으로 이루어진 데이터 객체의 집합입니다. 이러한 데이터 객체는 중괄호 `{}`로 감싸져 있으며, 각 객체는 콤마 `,`로 구분됩니다. 각각의 이름-값 쌍은 콜론 `:`으로 구분되며, 이름은 문자열로 작성되어야 합니다. 값은 다양한 데이터 타입을 가질 수 있습니다.

다음은 JSON의 예시입니다.

```javascript
{
   "name": "John Doe",
   "age": 30,
   "city": "Seoul",
   "isStudent": false,
   "hobbies": ["programming", "reading", "gaming"]
}
```

위의 예시에서 `name`은 문자열, `age`는 숫자, `city`는 문자열, `isStudent`는 boolean, `hobbies`는 배열로 각각의 값이 지정되어 있습니다.

## 3. JSON 사용법
JSON 데이터는 다양한 방법으로 사용할 수 있습니다. 자바스크립트에서 JSON 데이터를 다루는 방법은 매우 간단합니다. JSON 데이터를 JavaScript 객체로 파싱하려면 `JSON.parse()` 메서드를 사용하면 됩니다. 

다음은 JSON 데이터를 JavaScript 객체로 파싱하는 예시입니다.

```javascript
var jsonString = '{ "name": "John Doe", "age": 30, "city": "Seoul" }';
var jsonObject = JSON.parse(jsonString);

console.log(jsonObject.name); // John Doe
console.log(jsonObject.age); // 30
console.log(jsonObject.city); // Seoul
```

반대로, JavaScript 객체를 JSON 문자열로 변환하려면 `JSON.stringify()` 메서드를 사용합니다.

다음은 JavaScript 객체를 JSON 문자열로 변환하는 예시입니다.

```javascript
var person = {
   name: "John Doe",
   age: 30,
   city: "Seoul"
};

var jsonString = JSON.stringify(person);

console.log(jsonString); // {"name":"John Doe","age":30,"city":"Seoul"}
```

## 4. JSON의 활용
JSON은 웹 애플리케이션에서 데이터를 교환하는데 매우 유용하게 사용됩니다. 서버와 클라이언트 간의 데이터 통신에 JSON 형식을 사용하여 데이터를 전송하고, 클라이언트에서는 받은 JSON 데이터를 파싱하여 사용할 수 있습니다. 또한, 다양한 외부 API에서 제공하는 데이터도 JSON 형식으로 제공되는 경우가 많습니다.

또한, JSON은 데이터를 파일로 저장하는데에도 사용될 수 있습니다. 많은 프로그래밍 언어에서 JSON 데이터를 파일로 읽고 쓸 수 있는 라이브러리를 지원하고 있습니다.

## 5. 참고 자료
- [JSON - MDN Web Docs](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/JSON)
- [JSON(JavaScript Object Notation) 소개](http://www.json.org/json-ko.html)