---
layout: post
title: "[javascript] Angular.js를 이용하여 AJAX (Asynchronous JavaScript and XML) 요청 처리하기"
description: " "
date: 2023-10-18
tags: [javascript]
comments: true
share: true
---

Angular.js는 클라이언트 측 JavaScript 애플리케이션 개발에 사용되는 인기 있는 프레임워크입니다. 이를 통해 AJAX 요청을 쉽게 처리할 수 있습니다. 이번 블로그 포스트에서는 Angular.js를 이용하여 AJAX 요청을 어떻게 처리하는지 알아보겠습니다.

## 1. Angular.js 설치하기

먼저, Angular.js를 사용하기 위해 프로젝트에 Angular.js를 설치해야 합니다. Angular.js를 사용하기 위해 `<script>` 태그를 이용하여 Angular.js를 다운로드하거나, CDN(Content Delivery Network)을 이용할 수 있습니다.

```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.9/angular.min.js"></script>
```

위의 코드는 Google CDN에서 호스팅되는 Angular.js 버전 1.7.9를 사용하는 방법입니다. 필요에 따라 Angular.js의 다른 버전을 사용할 수도 있습니다.

## 2. AJAX 요청 처리하기

Angular.js에서 AJAX 요청을 처리하기 위해서는 `$http` 서비스를 사용해야 합니다. 이 서비스는 AJAX 요청을 수행하고 응답을 처리하는 데에 사용됩니다.

```javascript
angular.module('myApp', [])
    .controller('myController', function($scope, $http) {
        // AJAX 요청 수행
        $http.get('/api/data')
            .then(function(response) {
                // 요청 성공 시 처리 로직
                $scope.data = response.data;
            }, function(error) {
                // 요청 실패 시 처리 로직
                console.error('AJAX 요청 실패:', error);
            });
    });
```

위의 코드는 Angular.js 애플리케이션에서 AJAX 요청을 수행하는 예시입니다. `$http.get()` 함수를 이용하여 GET 메서드를 사용한 AJAX 요청을 수행하고, 요청이 성공하면 `.then()` 메서드를 통해 응답 데이터를 처리합니다.

## 3. 서버 응답 처리하기

서버로부터 받은 응답 데이터는 `$scope` 객체를 통해 사용할 수 있습니다. 위의 예시에서는 `$scope.data`에 응답 데이터를 할당하였습니다. 이렇게 할당된 데이터는 Angular.js 템플릿에서 사용할 수 있습니다.

```html
<div ng-app="myApp" ng-controller="myController">
    <ul>
        <li ng-repeat="item in data">{{ item.name }}</li>
    </ul>
</div>
```

위의 코드는 Angular.js 템플릿에서 `$scope.data`에 할당된 데이터를 반복하여 출력하는 예시입니다. `ng-repeat` 디렉티브를 사용하여 데이터를 반복 처리할 수 있습니다.

## 결론

이번 블로그 포스트에서는 Angular.js를 이용하여 AJAX 요청을 처리하는 방법에 대해 알아보았습니다. `$http` 서비스를 사용하여 AJAX 요청을 수행하고 응답을 처리할 수 있습니다. 이를 통해 Angular.js를 활용하여 다양한 AJAX 요청 처리가 가능하며, 클라이언트 측 JavaScript 개발을 더욱 효율적이고 간편하게 할 수 있습니다.

---

* [Angular.js 공식 사이트](https://angularjs.org/)