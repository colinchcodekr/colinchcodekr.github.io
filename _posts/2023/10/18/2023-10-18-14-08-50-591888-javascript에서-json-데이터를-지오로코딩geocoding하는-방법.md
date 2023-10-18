---
layout: post
title: "[javascript] JavaScript에서 JSON 데이터를 지오로코딩(Geocoding)하는 방법"
description: " "
date: 2023-10-18
tags: [javascript]
comments: true
share: true
---

**지오로코딩(Geocoding)**은 주소나 장소 이름을 위도와 경도로 변환하는 프로세스를 말합니다. JavaScript에서 지오로코딩을 수행하기 위해서는 외부 API를 사용해야 합니다. 이 글에서는 **Google Maps Geocoding API**를 사용하여 JavaScript에서 JSON 데이터를 지오로코딩하는 방법을 설명하겠습니다.

## Google Maps Geocoding API 키 발급

먼저, Google Maps Geocoding API를 사용하기 위해서는 자신의 Google 계정에 프로젝트를 만들고 API 키를 발급받아야 합니다. 아래 단계를 따라 API 키를 발급받아주세요.

1. [Google Cloud Console](https://console.cloud.google.com/)에 접속합니다.
2. 프로젝트를 만들고 해당 프로젝트를 선택합니다.
3. "사용자 인증 정보"로 이동합니다.
4. "사용자 인증 정보 만들기" 버튼을 클릭하고 "API 키"를 선택합니다.
5. 발급받은 API 키를 안전한 곳에 보관합니다.

## JavaScript에서 Geocoding 수행하기

이제 JavaScript에서 Geocoding을 수행하는 방법을 알아보겠습니다.

```javascript
async function geocode(address) {
  const apiKey = "여기에_발급받은_API_키_입력";
  const baseUrl = "https://maps.googleapis.com/maps/api/geocode/json";
  
  const url = `${baseUrl}?address=${encodeURIComponent(address)}&key=${apiKey}`;

  try {
    const response = await fetch(url);
    const data = await response.json();
    
    if (data.results.length > 0) {
      const { lat, lng } = data.results[0].geometry.location;
      console.log("위도:", lat);
      console.log("경도:", lng);
    } else {
      console.log("주소를 찾을 수 없습니다.");
    }
  } catch (error) {
    console.error("지오코딩 요청 에러:", error);
  }
}

geocode("서울특별시 강남구 역삼동 123-456");
```

위의 코드에서는 `geocode` 함수를 정의하고, 주소를 매개변수로 받아와서 Geocoding을 수행합니다. 먼저, `apiKey`와 `baseUrl` 변수를 설정합니다. 그다음, `fetch` 함수를 사용하여 API 요청을 보내고, 응답을 JSON 형식으로 파싱합니다. 

데이터의 `results` 배열은 여러 개의 결과를 가질 수 있으며, 첫 번째 결과를 사용하여 위도와 경도 정보를 추출합니다. 결과가 없는 경우에는 "주소를 찾을 수 없습니다."라는 메시지를 출력합니다.

마지막으로, `geocode` 함수를 호출하여 주소를 전달하면 이에 대한 Geocoding 결과가 콘솔에 출력됩니다.

Google Maps Geocoding API를 사용하여 JavaScript에서 JSON 데이터를 지오로코딩하는 방법을 알아보았습니다. 이를 응용하여 위치 정보 기반 서비스를 개발할 수 있습니다.

더 자세한 정보는 [Google Maps Geocoding API 문서](https://developers.google.com/maps/documentation/geocoding/overview)를 참고하세요.