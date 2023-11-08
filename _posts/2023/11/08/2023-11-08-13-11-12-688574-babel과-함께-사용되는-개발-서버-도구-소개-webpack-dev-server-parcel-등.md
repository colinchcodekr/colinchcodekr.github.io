---
layout: post
title: "[javascript] Babel과 함께 사용되는 개발 서버 도구 소개 (webpack-dev-server, Parcel 등)"
description: " "
date: 2023-11-08
tags: [javascript]
comments: true
share: true
---

Babel은 모던 자바스크립트 문법을 이해할 수 없는 구형 브라우저와 호환성을 유지하기 위해 사용되는 도구입니다. Babel은 자바스크립트 코드를 컴파일하여 구형 브라우저에서도 정상적으로 실행될 수 있도록 변환합니다. 하지만 Babel을 사용하면서 코드를 수정할 때마다 매번 수동으로 변환 후 브라우저에서 테스트해야하는 번거로움이 있습니다.

이러한 문제를 해결하기 위해 개발 서버 도구가 등장했습니다. 개발 서버 도구는 코드를 변경하면 자동으로 변환하여 브라우저에서 실시간으로 테스트할 수 있도록 도와줍니다. 여기에서는 Babel과 함께 사용되는 주요 개발 서버 도구인 webpack-dev-server와 Parcel에 대해 소개하겠습니다.

## 1. webpack-dev-server
webpack-dev-server는 webpack으로 번들링된 자바스크립트 파일을 개발 서버로 실행해주는 도구입니다. 설정 파일을 통해 개발 서버의 포트 번호, 라우팅 설정 등을 지정할 수 있습니다. 또한, 개발 서버는 코드를 변경하면 자동으로 번들링 및 페이지 리로딩을 처리해줍니다.
 
다음은 webpack-dev-server를 사용하는 코드 예제입니다:

```javascript
// webpack.config.js
module.exports = {
  // ...웹팩 설정
  devServer: {
    port: 3000, // 개발 서버 포트 번호
    hot: true, // 변경된 모듈만 리로드
    historyApiFallback: true, // 404 에러 시 index.html 반환
  },
  // ...
};
```

```bash
$ webpack-dev-server
```

## 2. Parcel
Parcel은 webpack과 유사한 번들러이며, zero-configuration으로 동작하는 특징이 있습니다. Parcel을 사용하면 별도의 설정 파일 없이도 자동으로 개발 서버가 실행됩니다. 코드 변경 시 자동으로 번들링되고 브라우저에서 실시간으로 테스트할 수 있습니다.

다음은 Parcel을 사용하는 코드 예제입니다:

```bash
$ parcel index.html
```

정적 파일의 경우 자동으로 적절한 로더를 설정하여 번들링해줍니다. 또한, 번들링된 파일의 크기를 최적화하여 퍼포먼스를 향상시킵니다.

## 결론
개발 서버 도구는 Babel과 함께 사용할 경우 코드의 변환 및 테스트를 자동화하여 개발 과정을 효율적으로 진행할 수 있게 도와줍니다. webpack-dev-server와 Parcel은 각각의 특징을 가지고 있으며, 프로젝트의 요구에 맞게 선택하여 사용할 수 있습니다. 참고 문서와 공식 홈페이지를 통해 더 자세한 내용을 확인해보세요.

## 참고 문서
- [webpack-dev-server 공식 문서](https://webpack.js.org/configuration/dev-server/)
- [Parcel 공식 문서](https://v2.parceljs.org/)