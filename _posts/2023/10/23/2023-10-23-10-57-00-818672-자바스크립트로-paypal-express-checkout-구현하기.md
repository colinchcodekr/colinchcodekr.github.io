---
layout: post
title: "[javascript] 자바스크립트로 PayPal Express Checkout 구현하기"
description: " "
date: 2023-10-23
tags: [javascript]
comments: true
share: true
---

이 블로그 포스트에서는 자바스크립트를 사용하여 PayPal Express Checkout을 구현하는 방법에 대해 알아보겠습니다. PayPal Express Checkout은 사용자가 웹 사이트에서 간편하게 결제를 완료할 수 있는 방법 중 하나입니다.

## PayPal Express Checkout란?

PayPal Express Checkout은 PayPal의 결제 플랫폼 중 하나로, 사용자가 PayPal 계정으로 로그인하여 간편하게 결제를 완료할 수 있게 해줍니다. 이를 통해 사용자는 카드 번호나 개인 정보를 입력하지 않고도 결제를 완료할 수 있습니다.

## 구현 단계

1. PayPal 개발자 계정 생성 및 API 키 발급
2. 클라이언트 사이드 라이브러리 추가
3. 구매 정보 확인 및 결제 처리 요청
4. 결제 완료 후 리디렉션 처리

### 1. PayPal 개발자 계정 생성 및 API 키 발급

먼저, PayPal 개발자 계정을 생성해야 합니다. 개발자 계정 생성 후에는 Express Checkout을 사용할 수 있는 API 키를 발급받을 수 있습니다. API 키는 후에 클라이언트 사이드 라이브러리를 추가할 때 사용됩니다.

### 2. 클라이언트 사이드 라이브러리 추가

PayPal Express Checkout을 구현하려면 클라이언트 사이드에서 제공되는 라이브러리를 추가해야 합니다. 이 라이브러리는 PayPal 인증 및 결제 처리를 담당하며, 웹 사이트와 PayPal 간의 통신을 보안하고 도와줍니다. 이 라이브러리를 웹 사이트에 추가하기 위해서는 script 태그를 사용하면 됩니다.

```javascript
<script src="https://www.paypal.com/sdk/js?client-id=YOUR_CLIENT_ID"></script>
```

`YOUR_CLIENT_ID` 부분에는 앞서 발급받은 API 키를 넣어주어야 합니다.

### 3. 구매 정보 확인 및 결제 처리 요청

PayPal Express Checkout을 사용하기 위해서는 구매 정보를 확인하고 결제 처리를 요청해야 합니다. 이를 위해서는 PayPal SDK에서 제공하는 `createOrder` 및 `onApprove` 함수를 사용할 수 있습니다.

```javascript
paypal.Buttons({
  createOrder: function(data, actions) {
    // 구매 정보를 생성하고 반환하는 로직을 작성합니다.
    return actions.order.create({
      purchase_units: [{
        amount: {
          value: '10.00' // 결제 금액을 입력합니다.
        }
      }]
    });
  },
  onApprove: function(data, actions) {
    // 결제가 승인된 후에 실행되는 로직을 작성합니다.
    return actions.order.capture().then(function(details) {
      // 결제 완료 시 처리할 로직을 작성합니다.
      alert('결제가 완료되었습니다!');
    });
  }
}).render('#paypal-button-container');
```

### 4. 결제 완료 후 리디렉션 처리

결제가 완료된 후에는 사용자를 특정 페이지로 리디렉션시킬 수 있습니다. PayPal에서는 `return_url` 및 `cancel_url` 파라미터를 사용하여 결제 완료 및 취소 시 이동할 페이지를 지정할 수 있습니다. 이를 사용하여 결제 완료 후 리디렉션 처리를 설정할 수 있습니다.

```javascript
paypal.Buttons({
  createOrder: function(data, actions) {
    // ...
  },
  onApprove: function(data, actions) {
    // ...
  },
  onCancel: function(data) {
    // 결제 취소 시 실행될 로직을 작성합니다.
    window.location.href = "https://example.com/cancel";
  }
}).render('#paypal-button-container');
```

위의 예제에서는 결제 취소 시 `https://example.com/cancel`로 리디렉션됩니다.

## 결론

이렇게 JavaScript를 사용하여 PayPal Express Checkout을 구현하는 방법에 대해 알아보았습니다. PayPal Express Checkout을 사용하면 사용자가 웹 사이트에서 손쉽게 결제를 완료할 수 있으며, 개발자는 간단한 코드만으로 결제 플랫폼을 구현할 수 있습니다.

더 자세한 내용은 [PayPal 개발자 문서](https://developer.paypal.com/docs/business/checkout/add-paypal-checkout/)를 참조하십시오.