---
layout: post
title: "[javascript] 자바스크립트를 사용하여 Firebase Cloud Messaging을 통해 알림 보내기"
description: " "
date: 2023-10-19
tags: [javascript]
comments: true
share: true
---

Firebase Cloud Messaging(FCM)은 모바일 및 웹 애플리케이션에 실시간으로 알림을 보낼 수 있는 도구입니다. 이를 사용하여 사용자에게 중요한 업데이트를 전달하거나 애플리케이션을 통해 상호작용할 수 있습니다. 이번 블로그 포스트에서는 자바스크립트를 사용하여 Firebase Cloud Messaging을 통해 알림을 보내는 방법에 대해 알아보겠습니다. 

## 필수 사항
Firebase Cloud Messaging을 사용하기 위해 다음 사항이 필요합니다.
- Firebase 프로젝트: Firebase 콘솔에서 새 프로젝트를 생성해야 합니다.
- Firebase SDK: Firebase 통합을 위해 프로젝트에 Firebase SDK를 추가해야 합니다. 
- 서비스 워커: FCM 알림을 사용하기 위해 서비스 워커를 등록하고 설정해야 합니다.

## Firebase SDK 추가하기
Firebase SDK를 추가하려면 `firebase.js` 파일을 다운로드하고 HTML 파일에 포함해야 합니다. 다음은 Firebase SDK의 예시 코드입니다.
```html
<script src="https://www.gstatic.com/firebasejs/7.13.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/7.13.1/firebase-messaging.js"></script>
<script src="firebase-init.js"></script>
```
위 코드에서 `firebase-init.js`는 Firebase 프로젝트에서 제공하는 설정 파일입니다. 

## 서비스 워커 등록하기
Firebase Cloud Messaging을 사용하려면 서비스 워커를 등록해야 합니다. 이를 통해 백그라운드에서 알림을 수신할 수 있습니다. 서비스 워커를 등록하고 설정하는 방법은 다음과 같습니다.

```javascript
// firebase-messaging-sw.js
importScripts('https://www.gstatic.com/firebasejs/7.13.1/firebase-app.js');
importScripts('https://www.gstatic.com/firebasejs/7.13.1/firebase-messaging.js');

firebase.initializeApp({
  // Firebase 프로젝트 설정
  apiKey: 'YOUR_API_KEY',
  authDomain: 'YOUR_AUTH_DOMAIN',
  databaseURL: 'YOUR_DATABASE_URL',
  projectId: 'YOUR_PROJECT_ID',
  storageBucket: 'YOUR_STORAGE_BUCKET',
  messagingSenderId: 'YOUR_MESSAGING_SENDER_ID',
  appId: 'YOUR_APP_ID',
  measurementId: 'YOUR_MEASUREMENT_ID'
});

firebase.messaging();
```
위 코드에서 `YOUR_API_KEY`, `YOUR_AUTH_DOMAIN`, `YOUR_DATABASE_URL` 등의 값을 Firebase 프로젝트에서 확인하고 대체해야 합니다.

## 알림 보내기
Firebase SDK를 추가하고 서비스 워커를 등록한 후에는 자바스크립트를 사용하여 알림을 보낼 수 있습니다. 다음은 알림을 보내는 예시 코드입니다.

```javascript
// 알림 보내기
const messaging = firebase.messaging();

messaging.requestPermission()
  .then(function() {
    console.log('알림 권한이 허용되었습니다.');
    return messaging.getToken();
  })
  .then(function(token) {
    console.log('디바이스 토큰:', token);
    // 토큰을 서버로 전송하여 사용자에게 알림을 보낼 수 있음
  })
  .catch(function(error) {
    console.log('알림 권한이 거부되었습니다.', error);
  });
```

위 코드에서 `requestPermission` 메서드를 호출하여 알림 권한을 요청한 후에 `getToken` 메서드를 사용하여 디바이스 토큰을 가져올 수 있습니다. 이 디바이스 토큰을 사용하여 서버에서 해당 디바이스에 알림을 보낼 수 있습니다.

## 결론
이렇게 자바스크립트를 사용하여 Firebase Cloud Messaging을 통해 알림을 보내는 방법을 알아보았습니다. Firebase의 강력한 기능을 활용하여 사용자에게 중요한 업데이트를 실시간으로 전달할 수 있습니다. Firebase 콘솔에서 애플리케이션에 대한 추가 설정을 진행하고, 서비스 워커 및 자바스크립트 코드를 구현하여 원하는 알림을 보낼 수 있습니다.