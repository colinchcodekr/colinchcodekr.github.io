---
layout: post
title: "[javascript] Express.js에서 JWT(Json Web Token) 활용하기"
description: " "
date: 2023-11-03
tags: [javascript]
comments: true
share: true
---

JSON Web Token (JWT)은 웹 애플리케이션에서 인증 및 권한 부여를 위해 사용되는 토큰 기반 인증 방식입니다. Express.js와 같은 Node.js 기반 프레임워크에서 JWT를 사용하여 보안적인 인증을 구현할 수 있습니다.

## JWT란 무엇인가요?

JWT는 세 부분으로 구성된 문자열입니다. Header, Payload, Signature로 이루어져 있으며, 각 부분은 Base64로 인코딩 된 정보입니다.

- **Header**: 토큰의 유형과 해시 알고리즘에 대한 정보를 포함합니다.
- **Payload**: 토큰에 포함되는 클레임(claim) 정보, 예를 들어 사용자 ID, 권한 등의 정보가 포함될 수 있습니다.
- **Signature**: Header와 Payload를 인코딩한 후, 비밀 키로 서명하여 토큰의 무결성을 보장합니다.

## Express.js에서 JWT 사용하기

1. `jsonwebtoken` 모듈을 설치합니다.

```bash
npm install jsonwebtoken
```

2. Express.js 애플리케이션에 `jsonwebtoken` 모듈을 추가합니다.

```javascript
const jwt = require('jsonwebtoken');
```

3. JWT 생성하기

```javascript
const secretKey = 'mySecretKey';
const payload = {
  userId: '123',
  role: 'admin',
};

const token = jwt.sign(payload, secretKey);
```

4. 생성된 JWT를 클라이언트에게 전송합니다.

5. JWT 검증하기

```javascript
const secretKey = 'mySecretKey';
const token = req.headers.authorization; // 클라이언트가 전송한 JWT

jwt.verify(token, secretKey, (err, decoded) => {
  if (err) {
    // 토큰이 유효하지 않은 경우
    res.sendStatus(403); // Forbidden
  } else {
    // 토큰이 유효한 경우
    console.log(decoded.userId); // 123
    console.log(decoded.role); // admin
    // 추가적인 작업 수행
  }
});
```

JWT를 사용하면 클라이언트가 서버로부터 발급받은 토큰을 이용하여 인증 정보를 확인할 수 있으며, 서버에서는 토큰의 유효성을 검사하여 안전한 인증을 수행할 수 있습니다.

더 자세한 내용은 [공식 JWT 사이트](https://jwt.io)를 참조하시기 바랍니다.