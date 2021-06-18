---
layout: post
title: "[web] Shape file 웹페이지에 띄우기"
description: " "
date: 2021-06-17
tags: [web]
comments: true
share: true
---


# Shape file 웹페이지에 띄우기

d3 라이브러리를 이용하여 지도를 띄우기 위해서는 shape 파일을 json 파일로 변환할 필요가 있다.
본인은 topoJson 라이브러리를 이용하여 작성하였으므로, topoJson 파일로 변환하였다.
6개월 전에 작업할 때는 커맨드라인에서 변환툴을 이용했던 기억이었는데, 이번(2016년 11월)에 작업할 때는 아래 웹서비스를 이용하였다.

## mapshaper

- 웹사이트: [http://mapshaper.org/](http://mapshaper.org/)
- 웹 페이지에 간단하게 드래그드랍으로 로딩이 가능하다.
- 폴리곤 생성을 위해서 shp 파일과 속성 할당을 위해서 dbf 파일이 필요하다.
- simplify를 이용하여 용량을 줄일 수 있으며, export 메뉴를 이용하여 json 파일 추출이 가능하다.
- 지도 위에 올려보면 속성을 확인할 수 있다. 속성에서 폴리곤의 고유 코드를 메모해 둘 필요가 있다.