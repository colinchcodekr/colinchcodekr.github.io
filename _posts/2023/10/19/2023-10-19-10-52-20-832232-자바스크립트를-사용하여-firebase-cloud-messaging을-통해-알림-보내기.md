---
layout: post
title: "[javascript] 자바스크립트를 사용하여 Firebase Cloud Messaging을 통해 알림 보내기"
description: " "
date: 2023-10-19
tags: [javascript]
comments: true
share: true
---

Firebase Cloud Messaging(FCM)은 개발자가 안드로이드, iOS 및 웹 앱에 알림을 보낼 수 있는 플랫폼입니다. 이 문서에서는 자바스크립트를 사용하여 FCM을 통해 알림을 보내는 방법을 알려드리겠습니다.

## 1. Firebase 프로젝트 설정

Firebase 콘솔에 로그인하여 새 프로젝트를 생성하고, 웹 앱을 추가하세요. 이 과정을 통해 Firebase Cloud Messaging을 활성화할 수 있습니다. 프로젝트 설정에서 서비스 계정 키를 생성하고 다운로드 받으세요.

## 2. 웹 앱에 FCM 추가하기

웹 앱의 `index.html` 파일에 다음 스크립트를 추가하세요.

```html
<script src="https://www.gstatic.com/firebasejs/8.7.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.7.1/firebase-messaging.js"></script>
```

## 3. Firebase 구성하기

`firebase.js` 파일을 생성하고 다음 내용으로 Firebase를 구성하세요. 다운로드 받은 서비스 계정 키를 사용하여 `firebase.initializeApp()`를 호출하세요.

```javascript
import firebase from 'firebase/app';
import 'firebase/messaging';

const firebaseConfig = {
  // Firebase 구성 정보 입력
};

// Firebase 초기화
firebase.initializeApp(firebaseConfig);
const messaging = firebase.messaging();
```

## 4. FCM 토큰 가져오기

FCM 토큰은 디바이스별로 고유하게 생성되며, 알림을 받을 대상을 식별하는 데 사용됩니다. 이를 위해 다음 함수를 `firebase.js` 파일에 추가하세요.

```javascript
export const getToken = () => {
  messaging
    .getToken({ vapidKey: 'YOUR_PUBLIC_VAPID_KEY' })
    .then((currentToken) => {
      if (currentToken) {
        // 토큰 가져오기 성공
        console.log('FCM 토큰:', currentToken);
      } else {
        // 토큰 가져오기 실패
        console.log('토큰 가져오기 실패');
      }
    })
    .catch((error) => {
      console.error('토큰 가져오기 에러:', error);
    });
};
```

## 5. 알림 보내기

알림을 보내기 위해 다음 함수를 `firebase.js` 파일에 추가하세요.

```javascript
export const sendNotification = (title, body) => {
  const notification = {
    title: title,
    body: body,
    icon: '/path/to/icon.png',
  };

  messaging
    .getToken()
    .then((currentToken) => {
      return fetch('https://fcm.googleapis.com/fcm/send', {
        method: 'POST',
        headers: {
          Authorization: `Bearer YOUR_SERVER_KEY`,
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          to: currentToken,
          notification: notification,
        }),
      });
    })
    .then((response) => {
      console.log('알림 보내기 성공:', response);
    })
    .catch((error) => {
      console.error('알림 보내기 에러:', error);
    });
};
```

보내려는 알림의 제목(title)과 내용(body)을 파라미터로 전달하여 `sendNotification()` 함수를 호출하면 알림이 사용자 디바이스로 전송됩니다.

## 6. 사용자에게 알림 허용 요청하기

웹 앱에 알림을 표시하기 위해 사용자에게 허용을 요청해야 합니다. 다음 함수를 `firebase.js` 파일에 추가하세요.

```javascript
export const requestNotificationPermission = () => {
  Notification.requestPermission().then((permission) => {
    if (permission === 'granted') {
      console.log('알림 허용');
    } else {
      console.log('알림 거부');
    }
  });
};
```

## 7. 알림 보내기 예제

다음은 `index.html` 파일에서 알림 보내기를 위해 위에서 작성한 함수들을 사용하는 예제입니다.

```javascript
import { getToken, sendNotification, requestNotificationPermission } from './firebase.js';

// 알림 보내기 버튼 클릭 이벤트 핸들러
document.getElementById('sendNotificationButton').addEventListener('click', () => {
  const title = '새로운 알림';
  const body = '알림 내용입니다.';

  sendNotification(title, body);
});

// FCM 토큰 가져오기 버튼 클릭 이벤트 핸들러
document.getElementById('getTokenButton').addEventListener('click', () => {
  getToken();
});

// 알림 허용 요청 버튼 클릭 이벤트 핸들러
document.getElementById('requestPermissionButton').addEventListener('click', () => {
  requestNotificationPermission();
});
```

알림 보내기 버튼을 클릭하면 `sendNotification()` 함수를 호출하여 알림을 보낼 수 있습니다. `getTokenButton` 버튼을 클릭하면 `getToken()` 함수를 호출하여 FCM 토큰을 가져올 수 있고, `requestPermissionButton` 버튼을 클릭하면 `requestNotificationPermission()` 함수를 호출하여 알림 허용을 요청할 수 있습니다.

이제 자바스크립트를 사용하여 Firebase Cloud Messaging을 통해 알림을 보낼 수 있습니다. 자세한 내용은 [Firebase 문서](https://firebase.google.com/docs/cloud-messaging)를 참조하세요.