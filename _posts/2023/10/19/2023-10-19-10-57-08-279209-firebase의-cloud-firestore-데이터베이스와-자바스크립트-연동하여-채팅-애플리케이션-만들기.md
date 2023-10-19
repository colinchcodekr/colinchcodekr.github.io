---
layout: post
title: "[javascript] Firebase의 Cloud Firestore 데이터베이스와 자바스크립트 연동하여 채팅 애플리케이션 만들기"
description: " "
date: 2023-10-19
tags: [javascript]
comments: true
share: true
---

Firebase는 많은 웹 개발자들에게 인기있는 백엔드 서비스 플랫폼입니다. 그 중 Cloud Firestore는 NoSQL 데이터베이스이며, 실시간 데이터 동기화 및 강력한 쿼리 기능을 제공합니다. 이번 글에서는 Firebase의 Cloud Firestore 데이터베이스와 자바스크립트를 사용하여 채팅 애플리케이션을 만드는 방법을 알아보겠습니다.

## 1. Firebase 프로젝트 설정하기

먼저, Firebase 프로젝트를 생성하고 콘솔에서 Cloud Firestore를 활성화해야 합니다. Firebase 콘솔에 로그인한 후, "프로젝트 추가" 버튼을 클릭하여 새 프로젝트를 생성합니다. 프로젝트를 생성한 후, "데이터베이스" 메뉴로 이동하여 Cloud Firestore를 활성화합니다.

## 2. Firebase SDK 추가하기

Firebase SDK를 프로젝트에 추가해야 합니다. `firebase`와 `firebase-firestore` 패키지를 설치하기 위해 npm을 사용합니다.

```javascript
npm install firebase firebase-firestore
```

## 3. Firebase 구성 및 인증 설정하기

Firebase에 연결하려면 Firebase 구성 정보와 인증 설정이 필요합니다. 아래의 코드를 사용하여 Firebase 구성 및 인증 설정을 수행합니다.

```javascript
import firebase from 'firebase/app';
import 'firebase/firestore';

const firebaseConfig = {
  // Firebase 구성 정보 입력
};

firebase.initializeApp(firebaseConfig);

// Firebase 인증 설정
// 예시로 구글 로그인 사용
const provider = new firebase.auth.GoogleAuthProvider();

firebase.auth().signInWithPopup(provider);
```

## 4. 채팅 애플리케이션 UI 만들기

Firebase 연결 및 사용자 인증이 완료되었으므로 이제 채팅 애플리케이션의 UI를 만들어야 합니다. HTML과 CSS를 사용하여 채팅 메시지를 표시하고 사용자가 메시지를 입력할 수 있는 입력 창을 만듭니다.

## 5. 채팅 데이터 저장 및 읽기

Firestore 데이터베이스를 사용하여 채팅 메시지를 저장하고 읽는 작업을 구현해야 합니다. 아래의 코드는 메시지를 저장하고 읽는 함수를 구현하는 방법을 보여줍니다.

```javascript
// Firestore 데이터베이스 인스턴스 가져오기
const db = firebase.firestore();

// 메시지 저장하기
function saveMessage(message) {
  db.collection('messages').add({
    message: message,
    timestamp: firebase.firestore.FieldValue.serverTimestamp(),
  });
}

// 메시지 읽어오기
function fetchMessages(callback) {
  db.collection('messages')
    .orderBy('timestamp')
    .onSnapshot(snapshot => {
      const messages = [];
      snapshot.forEach(doc =>
        messages.push({
          id: doc.id,
          ...doc.data(),
        })
      );
      callback(messages);
    });
}
```

## 6. 채팅 데이터 표시하기

Firestore에서 채팅 메시지를 읽어온 후, HTML에서 해당 메시지를 표시하는 작업을 수행해야 합니다. 아래의 코드는 채팅 메시지를 표시하는 함수를 구현하는 방법을 보여줍니다.

```javascript
// 채팅 메시지 표시하기
function displayMessages(messages) {
  const chatContainer = document.getElementById('chat-container');
  chatContainer.innerHTML = '';

  messages.forEach(message => {
    const messageElement = document.createElement('div');
    messageElement.innerText = message.message;

    chatContainer.appendChild(messageElement);
  });
}
```

## 7. 채팅 애플리케이션 실행하기

이제 Firebase와 Cloud Firestore가 연동된 채팅 애플리케이션이 완성되었습니다. 실제로 애플리케이션을 실행하고 테스트해보세요.

```javascript
// 메시지 입력 이벤트 처리
const messageInput = document.getElementById('message-input');
const sendButton = document.getElementById('send-button');

sendButton.addEventListener('click', () => {
  const message = messageInput.value;

  saveMessage(message);

  messageInput.value = '';
});

// 채팅 메시지 읽기
fetchMessages(messages => {
  displayMessages(messages);
});
```

## 결론

이제 Firebase의 Cloud Firestore 데이터베이스와 자바스크립트를 사용하여 채팅 애플리케이션을 만드는 방법을 알게 되었습니다. Firebase를 사용하면 백엔드 작업을 간소화하고, 실시간 데이터 동기화 및 강력한 쿼리 기능을 쉽게 사용할 수 있습니다. 이를 통해 채팅 애플리케이션이나 다른 실시간 기능을 갖춘 웹 애플리케이션을 구축할 수 있습니다.

더 자세한 내용은 [Firebase 문서](https://firebase.google.com/docs)를 참고하시기 바랍니다.