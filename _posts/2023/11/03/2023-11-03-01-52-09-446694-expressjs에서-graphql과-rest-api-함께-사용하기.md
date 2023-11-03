---
layout: post
title: "[javascript] Express.js에서 GraphQL과 REST API 함께 사용하기"
description: " "
date: 2023-11-03
tags: [javascript]
comments: true
share: true
---

Express.js는 Node.js를 위한 유명한 웹 어플리케이션 프레임워크로, 많은 개발자들이 REST API를 구축하기 위해 사용하고 있습니다. 그런데 최근에는 GraphQL이 더욱 인기를 얻고 있어 GraphQL을 사용하여 데이터를 처리하고 싶을 수도 있습니다.

이번 글에서는 Express.js를 사용하여 GraphQL과 REST API를 함께 사용하는 방법에 대해 알아보겠습니다.

## 1. 기본 설정

먼저, Express.js 프로젝트를 생성하고 필요한 의존성을 설치해야 합니다. 아래와 같이 명령어를 실행하여 작업을 시작합니다.

```shell
mkdir express-graphql-rest-api
cd express-graphql-rest-api
npm init -y
```

그리고 Express와 GraphQL 관련 라이브러리를 설치합니다.

```shell
npm install express express-graphql graphql
```

## 2. GraphQL 스키마 정의하기

GraphQL 스키마는 API에 어떤 데이터가 주고받을 수 있는지를 정의하는데 사용됩니다. 아래와 같이 `schema.graphql` 파일을 생성하고 스키마를 정의합니다.

```graphql
type User {
  id: ID!
  name: String!
  age: Int!
}

type Query {
  getUser(id: ID!): User
  getUsers: [User]
}

type Mutation {
  createUser(name: String!, age: Int!): User
  updateUser(id: ID!, name: String, age: Int): User
  deleteUser(id: ID!): User
}
```

## 3. GraphQL 미들웨어 설정하기

Express.js 애플리케이션에서 GraphQL 미들웨어를 설정하여 GraphQL API를 사용할 수 있도록 합니다. 아래와 같이 `server.js` 파일을 생성하고 필요한 설정을 추가합니다.

```javascript
const express = require('express');
const { graphqlHTTP } = require('express-graphql');
const { buildSchema } = require('graphql');

const app = express();

// GraphQL 스키마 가져오기
const schema = buildSchema(`
  // 스키마 내용은 앞서 생성한 schema.graphql 파일의 내용을 가져옵니다.
`);

// GraphQL 미들웨어 설정
app.use('/graphql', graphqlHTTP({
  schema: schema,
  graphiql: true,
}));

// 서버 실행
app.listen(3000, () => {
  console.log('GraphQL API 서버가 http://localhost:3000/graphql 주소에서 실행되었습니다.');
});
```

## 4. REST API 추가하기

이제 GraphQL API와 함께 REST API도 추가해보겠습니다. REST API는 기존의 Express.js 라우터를 사용하여 정의할 수 있습니다.

```javascript
// REST API 라우터 설정
app.get('/users', (req, res) => {
  // 사용자 목록을 가져오는 로직 추가
});

app.get('/users/:id', (req, res) => {
  // 특정 사용자를 가져오는 로직 추가
});

app.post('/users', (req, res) => {
  // 사용자를 생성하는 로직 추가
});

app.put('/users/:id', (req, res) => {
  // 특정 사용자를 업데이트하는 로직 추가
});

app.delete('/users/:id', (req, res) => {
  // 특정 사용자를 삭제하는 로직 추가
});
```

## 5. 실행 및 테스트

모든 설정이 완료되었습니다. 이제 아래와 같이 명령어를 실행하여 Express.js 서버를 시작합니다.

```shell
node server.js
```

그리고 브라우저나 API 테스트 도구를 사용하여 GraphQL과 REST API를 테스트해보세요. GraphQL API는 `http://localhost:3000/graphql`에 접속하며, REST API는 `http://localhost:3000`에 접속할 수 있습니다.

## 마무리

이번 글에서는 Express.js에서 GraphQL과 REST API를 함께 사용하는 방법에 대해 간단하게 알아보았습니다. GraphQL과 REST API를 모두 사용하여 각각의 장단점을 활용하면 더욱 유연하고 효율적인 웹 어플리케이션을 개발할 수 있습니다. 만약 프로젝트에 따라 선택적으로 사용하는 것도 가능하니, 필요에 맞게 조합해보세요!

## 참고 자료

- [Express.js 공식 사이트](https://expressjs.com/)
- [GraphQL 공식 사이트](https://graphql.org/)
- [GraphQL과 REST의 비교 (번역)](https://velopert.com/3623)