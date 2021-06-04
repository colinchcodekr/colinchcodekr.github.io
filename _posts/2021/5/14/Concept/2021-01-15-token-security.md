---
layout: post
title: "[보안] Local Storage??"
description: " "
date: 2021-05-14
tags: [보안]
comments: true
share: true
---

# Token

## Local Storage??
jwt 토큰과 같이 토큰으로 로그인을 할때, 이 데이터를 어디에 저장해야할까?

우선 local Storage에 대해서 간략히 알아보자면,  로컬 스토리지는 브라우저에 저장되는 일종의 저장소인데 이는 자바스크립트 객체를 통해서 접근이 가능하다.

그렇기 때문에, 페이지의 자바스크립트 코드가 언제든 이를 접근할 수 있어서 보안상 이슈가 생긴다.

그렇기 때문에, 민감한 정보는 로컬 스토리지에 저장해서는 안되고, 공개적으로 사용하는 데이터들을 넣어야 한다.

결론: XSS <- 이런 해킹 기술에 취약하다.

리액트는 기본적으로 XSS를 통한 공격이 불가능하도록 설계되어 있지만,
기타 외부에서 가져오는 코드들 ( css 링크, 구글 어낼러틱스, 그 외 트랙커 등)

## 어떤 데이터를 어디에 저장할 것인가?

민감 데이터의 구체적인 예

* 사용자 ID
* 세션 ID
* JWT
* 개인 정보
* 신용 카드 정보
* API 키
* 그리고 페이스 북에 공개적으로 공유하고 싶지 않은 모든 것


위의 데이터들을 다루기 위해서 사용해야하는 방법

- 백엔드에서 세션 생성 -> 서명된 쿠키 사용
- 백엔드에서 쿠키를 보내줄때는 `httpOnly`  와 같은 옵션을 걸어준다.  
  이렇게 설정을 해주면, 자바 스크립트 코드를 통해서 쿠키를 수정하는 것을 막을 수 있다.

#보안