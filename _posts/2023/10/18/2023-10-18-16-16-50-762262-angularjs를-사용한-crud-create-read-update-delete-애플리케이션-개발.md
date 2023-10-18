---
layout: post
title: "[javascript] Angular.js를 사용한 CRUD (Create, Read, Update, Delete) 애플리케이션 개발"
description: " "
date: 2023-10-18
tags: [javascript]
comments: true
share: true
---

## 목차

- [소개](#소개)
- [설치](#설치)
- [CREATE](#CREATE)
- [READ](#READ)
- [UPDATE](#UPDATE)
- [DELETE](#DELETE)
- [결론](#결론)

## 소개

Angular.js는 웹 개발에 사용되는 자바스크립트 프레임워크 중 하나로, CRUD (Create, Read, Update, Delete) 애플리케이션 개발에 매우 유용합니다. 이번 블로그 포스트에서는 Angular.js를 사용하여 CRUD 애플리케이션을 개발하는 방법에 대해 알아보겠습니다.

## 설치

먼저, Angular.js를 사용하기 위해서는 해당 라이브러리를 설치해야 합니다. 설치는 다음과 같은 명령을 사용하여 진행할 수 있습니다.

```bash
npm install angular
```

혹은 CDN을 사용하는 경우, HTML 파일의 `<head>` 태그 내에 다음 스크립트 태그를 추가해주세요.

```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.9/angular.min.js"></script>
```

## CREATE

애플리케이션에서 생성(Create) 기능을 구현하기 위해서는 HTML에 form 태그를 추가하고, Angular.js의 `ng-model` 디렉티브를 사용하여 입력 필드와 데이터를 바인딩해줍니다. 예를 들어, 다음과 같은 코드를 작성할 수 있습니다.

```html
<form ng-submit="createItem()">
  <input type="text" ng-model="newItemName" placeholder="이름" required>
  <input type="number" ng-model="newItemQuantity" placeholder="수량" required>
  <button type="submit">추가</button>
</form>
```

Angular.js 컨트롤러에서는 `createItem` 함수를 정의하고, 이 함수 내에서 새로운 아이템을 생성하고 데이터베이스에 저장하는 로직을 작성합니다. 예를 들어, 다음과 같은 코드를 작성할 수 있습니다.

```javascript
$scope.createItem = function() {
  // 새로운 아이템 생성 및 데이터베이스에 저장하는 로직 작성
};
```

## READ

애플리케이션에서 읽기(Read) 기능을 구현하기 위해서는 Angular.js의 `ng-repeat` 디렉티브를 사용하여 데이터를 반복하여 표시해줍니다. 예를 들어, 다음과 같은 코드를 작성할 수 있습니다.

```html
<ul>
  <li ng-repeat="item in items">{{ item.name }} - {{ item.quantity }}</li>
</ul>
```

Angular.js 컨트롤러에서는 초기 데이터를 가져오는 로직을 작성하고, 이 데이터를 `items` 변수에 할당합니다. 예를 들어, 다음과 같은 코드를 작성할 수 있습니다.

```javascript
$scope.items = [];

// 초기 데이터 가져오는 로직 작성
```

## UPDATE

애플리케이션에서 업데이트(Update) 기능을 구현하기 위해서는 HTML에 수정할 항목을 표시하고, Angular.js의 `ng-model` 디렉티브를 사용하여 데이터와 입력 필드를 바인딩해줍니다. 예를 들어, 다음과 같은 코드를 작성할 수 있습니다.

```html
<div ng-repeat="item in items">
  <input type="text" ng-model="item.name">
  <input type="number" ng-model="item.quantity">
  <button ng-click="updateItem(item)">수정</button>
</div>
```

Angular.js 컨트롤러에서는 `updateItem` 함수를 정의하고, 이 함수 내에서 수정된 아이템을 데이터베이스에 업데이트하는 로직을 작성합니다. 예를 들어, 다음과 같은 코드를 작성할 수 있습니다.

```javascript
$scope.updateItem = function(item) {
  // 수정된 아이템을 업데이트하는 로직 작성
};
```

## DELETE

애플리케이션에서 삭제(Delete) 기능을 구현하기 위해서는 Angular.js의 `ng-click` 디렉티브를 사용하여 삭제 버튼을 클릭할 때 해당 아이템을 삭제하는 함수를 호출해줍니다. 예를 들어, 다음과 같은 코드를 작성할 수 있습니다.

```html
<div ng-repeat="item in items">
  <span>{{ item.name }} - {{ item.quantity }}</span>
  <button ng-click="deleteItem(item)">삭제</button>
</div>
```

Angular.js 컨트롤러에서는 `deleteItem` 함수를 정의하고, 이 함수 내에서 아이템을 데이터베이스에서 삭제하는 로직을 작성합니다. 예를 들어, 다음과 같은 코드를 작성할 수 있습니다.

```javascript
$scope.deleteItem = function(item) {
  // 아이템을 삭제하는 로직 작성
};
```

## 결론

이렇게 Angular.js를 사용하여 CRUD (Create, Read, Update, Delete) 애플리케이션을 개발하는 방법을 소개하였습니다. 각 기능을 구현할 때에는 Angular.js의 다양한 디렉티브와 컨트롤러를 활용하여 원하는 동작을 구현해야 합니다. 코드 예제를 참고하여 직접 CRUD 애플리케이션을 개발해보세요!