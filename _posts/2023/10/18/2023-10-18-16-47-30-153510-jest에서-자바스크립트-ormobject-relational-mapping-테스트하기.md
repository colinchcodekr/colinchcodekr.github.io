---
layout: post
title: "[javascript] Jest에서 자바스크립트 ORM(Object-Relational Mapping) 테스트하기"
description: " "
date: 2023-10-18
tags: [javascript]
comments: true
share: true
---

## 소개
Jest는 자바스크립트 프레임워크로, 유닛 테스트를 작성하고 실행하는 데 사용됩니다. 이번 글에서는 Jest를 사용하여 자바스크립트 ORM 테스트를 작성하는 방법에 대해 알아보겠습니다.

## Jest 설치하기
Jest는 npm을 통해 설치할 수 있습니다. 다음 명령어를 사용하여 Jest를 설치해주세요.

```javascript
npm install --save-dev jest
```

## ORM 테스트 준비하기
자바스크립트 ORM을 사용하여 데이터베이스와 상호 작용하는 코드를 작성하기 전에, 테스트를 위한 테스트 데이터베이스를 설정해야 합니다. 예를 들어, SQLite 데이터베이스를 사용하여 ORM 테스트를 진행하려면 다음과 같이 SQLite 데이터베이스를 설정해야 합니다.

```javascript
const { Sequelize } = require('sequelize');

const sequelize = new Sequelize('database', 'username', 'password', {
  dialect: 'sqlite',
  storage: ':memory:',
});
```

위 코드에서는 Sequelize를 사용하여 SQLite 데이터베이스를 설정하고, `:memory:` 옵션을 통해 메모리에서 동작하는 임시 데이터베이스를 생성합니다.

## ORM 테스트 작성하기
이제 Jest를 사용하여 자바스크립트 ORM 테스트를 작성해보겠습니다. 다음은 Sequelize ORM을 사용한 유저 모델을 테스트하는 예제입니다.

```javascript
const { DataTypes, Model } = require('sequelize');
const sequelize = require('./sequelize');

class User extends Model {}
User.init({
  username: DataTypes.STRING,
  email: DataTypes.STRING,
}, { sequelize, modelName: 'user' });

describe('User Model', () => {
  beforeEach(async () => {
    await sequelize.sync({ force: true });
  });

  test('should create a user', async () => {
    const user = await User.create({
      username: 'john',
      email: 'john@example.com',
    });
    expect(user.username).toBe('john');
    expect(user.email).toBe('john@example.com');
  });

  test('should update a user', async () => {
    const user = await User.create({
      username: 'john',
      email: 'john@example.com',
    });
    user.username = 'jane';
    await user.save();
    expect(user.username).toBe('jane');
  });

  test('should delete a user', async () => {
    const user = await User.create({
      username: 'john',
      email: 'john@example.com',
    });
    await user.destroy();
    const fetchedUser = await User.findByPk(user.id);
    expect(fetchedUser).toBeNull();
  });
});
```

위 코드에서는 `beforeEach` 함수를 사용하여 각 테스트 실행 전에 데이터베이스를 초기화합니다. 그리고 `test` 함수를 사용하여 각 유저 모델 메소드를 테스트합니다.

## 테스트 실행하기
테스트 코드를 작성한 후, 다음 명령어를 사용하여 Jest를 실행해주세요.

```javascript
npx jest
```

Jest는 테스트를 자동으로 실행하고, 각 테스트의 결과를 출력합니다.

## 결론
이 글에서는 Jest를 사용하여 자바스크립트 ORM(Object-Relational Mapping) 테스트를 작성하는 방법에 대해 알아보았습니다. Jest를 사용하면 쉽고 간편하게 ORM 테스트를 작성하고 실행할 수 있습니다. 자바스크립트 프로젝트에서 ORM을 사용할 때는 Jest를 통한 테스트 코드 작성을 고려해보세요.

## 참고자료
- [Jest 공식 문서](https://jestjs.io/)
- [Sequelize 공식 문서](https://sequelize.org/)