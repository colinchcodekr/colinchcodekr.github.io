---
layout: post
title: "[javascript] Braintree JavaScript SDK를 이용하여 결제내역을 조회하는 방법은 무엇인가요?"
description: " "
date: 2023-11-08
tags: [javascript]
comments: true
share: true
---

먼저, Braintree JavaScript SDK를 웹사이트에 추가해야 합니다. `<script>` 태그를 사용하여 SDK를 가져올 수 있습니다. 아래는 예시입니다:

```html
<script src="https://js.braintreegateway.com/web/3.57.0/js/client.min.js"></script>
<script src="https://js.braintreegateway.com/web/3.57.0/js/data-collector.min.js"></script>
<script src="https://js.braintreegateway.com/web/3.57.0/js/hosted-fields.min.js"></script>
<script src="https://js.braintreegateway.com/web/3.57.0/js/paypal.min.js"></script>
<script src="https://js.braintreegateway.com/web/3.57.0/js/paypal-checkout.min.js"></script>
<script src="https://js.braintreegateway.com/web/3.57.0/js/three-d-secure.min.js"></script>
<script src="https://js.braintreegateway.com/web/3.57.0/js/us-bank-account.min.js"></script>
```

다음으로, Braintree 클라이언트를 초기화합니다. `braintree.client.create` 메서드를 사용하여 클라이언트를 생성할 수 있습니다. API 키를 사용하여 인증을 처리합니다. 아래는 예시입니다:

```javascript
var braintreeClient;
var paymentMethodNonce;

braintree.client.create({
  authorization: 'YOUR_API_KEY'
}, function (err, clientInstance) {
  if (err) {
    console.error(err);
    return;
  }

  braintreeClient = clientInstance;

  // 클라이언트 생성 완료 후 추가 작업을 수행하세요.
});
```

클라이언트가 생성되면, `braintree.Client` 객체를 사용하여 결제 내역을 조회할 수 있습니다. `braintree.Client` 객체의 `transaction` 메서드를 사용하여 내역을 가져올 수 있습니다. 아래는 예시입니다:

```javascript
braintreeClient.transaction.find('transaction_id', function (err, transaction) {
  if (err) {
    console.error(err);
    return;
  }

  // 결제 내역 조회 후 수행할 작업을 수행하세요.
});
```

위의 예시에서 `transaction_id`를 실제 거래 ID로 바꿔야 합니다. `transaction` 객체에서는 거래의 세부 정보를 확인할 수 있습니다.

Braintree JavaScript SDK를 사용하여 결제 내역을 조회하는 방법에 대해 알아보았습니다. Braintree 개발자 문서를 참조하면 더 많은 정보를 얻을 수 있습니다.