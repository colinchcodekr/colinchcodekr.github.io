---
layout: post
title: "[CleanCode] 동시성"
description: " "
date: 2021-06-09
tags: [CleanCode]
comments: true
share: true
---


동시성
------

-	다중 스레드 코드는 올바로 구현하기 어렵다.
-	스레드 코드는 최대한 집약되고 작아야 한다.
-	동시성 오류를 일으키는 잠정적인 원인을 철저히 이해한다.
-	사용하는 라이브러리와 기본 알고리즘을 이해한다.
-	보호할 코드 영역을 찾아내는 방법과 특정 코드 영역을 잠그는 방법을 이해한다.
-	스레드 코드는 많은 플랫폼에서 많은 설정으로 반복해서 계속 테스트해야 한다.

---

점진적인 개선
-------------

-	깨끗한 코드를 짜려면 먼저 지저분한 코드를 짠 뒤에 정리해야 한다.
	1.	코드를 짜다가 코드가 점점 엉망이 되어 간다.
	2.	계속 밀어붙이면 프로그램은 어떻게든 완성하겠지만 그랬다가는 넘무 커서 손대기 어려운 골칫거리가 생겨날 수 있다. 그래서 기능을 더이상 추가하지 않고 리팩터링을 시작한다.
	3.	점진적으로 개선한다. 리팩터링은 루빅 큐브 맞추기와 비슷한다. 큰 목표 하나를 이루기 위해 자잘한 단계를 수 없이 거친다. 각 단계를 거쳐야 다음 단계가 가능하다.
-	그저 돌아가는 코드만으로는 부족하다.
-	나쁜 코드보다 더 오랫동안 더 심각하게 개발 프로젝트에 악영향을 미치는 요인도 없다.
-	너무 서두르다가 이후로 영원히 자신들의 운명을 지배할 악성 코드라는 굴레를 짊어진다.
-	물론 나쁜 코드도 깨끗한 코드로 개선할 수 있다. 하지만 비용이 엄청나게 많이 든다.
-	반면 처음부터 코드를 깨끗하게 유지하기란 상대적으로 쉽다.얼마전에 엉망으로 만든 코드는 지금 당장 정리하기 아주 쉽다.
-	그러므로 코드는 언제나 최대한 깔끔하고 단순하게 정리해야한다. 절대로 썩어가게 방치하면 안 된다.