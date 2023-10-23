---
layout: post
title: "[javascript] PayPal Adaptive Payments API를 이용한 자바스크립트로 결제 분리 기능 개발하기"
description: " "
date: 2023-10-23
tags: [javascript]
comments: true
share: true
---

PayPal은 온라인 결제를 처리하기 위해 다양한 API를 제공합니다. 그 중 하나인 Adaptive Payments API를 사용하여 자바스크립트로 결제 분리 기능을 개발하는 방법에 대해 알아보겠습니다.

## 개요

결제 분리 기능은 판매자와 수취인에 대한 결제를 분리하여 관리할 수 있는 기능입니다. 이를 통해 판매자는 수수료를 자동으로 공제하고 수취인에게 정산을 보낼 수 있습니다.

## 준비 사항

1. [PayPal 개발자 계정](https://developer.paypal.com/)을 등록하고 액세스 토큰을 발급받아야 합니다.
2. 장바구니 또는 결제 관련 정보를 포함한 HTML 페이지를 작성해야 합니다.

## 자바스크립트 코드

```javascript
// PayPal API 액세스 토큰
const accessToken = "YOUR_ACCESS_TOKEN";

// 결제 정보 생성
const createPayment = async () => {
  try {
    const response = await fetch("https://api.paypal.com/v1/payments/payment", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${accessToken}`
      },
      body: JSON.stringify({
        intent: "sale",
        payer: {
          payment_method: "paypal"
        },
        transactions: [
          {
            amount: {
              total: "10.00",
              currency: "USD"
            }
          }
        ]
      })
    });
    
    const data = await response.json();
    return data.links.find(link => link.rel === "approval_url").href;
  } catch (error) {
    console.error("Error creating payment:", error);
  }
};

// 결제 페이지로 리다이렉트
const redirectToPaymentPage = async () => {
  const paymentUrl = await createPayment();
  window.location.href = paymentUrl;
};
```

위 코드는 PayPal API에 액세스 토큰을 사용하여 결제 정보를 생성하고 결제 페이지로 리다이렉트하는 기능을 구현한 것입니다. 전체 코드를 사용하기 전에 `YOUR_ACCESS_TOKEN`을 발급받은 액세스 토큰 값으로 대체해야 합니다.

## 사용 방법

1. `createPayment` 함수를 호출하여 결제 정보를 생성합니다.
2. 생성된 결제 정보에서 `approval_url` 링크를 찾아 사용자를 결제 페이지로 리다이렉트합니다.

## 결론

PayPal Adaptive Payments API를 사용하여 자바스크립트로 결제 분리 기능을 개발하는 방법에 대해 알아보았습니다. 이를 통해 판매자와 수취인의 결제를 분리하고 관리할 수 있습니다.

더 자세한 내용은 [PayPal 개발자 문서](https://developer.paypal.com/docs/api/reference/)를 참조하세요.