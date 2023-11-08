---
layout: post
title: "[javascript] Braintree JavaScript SDK로 특정 고객의 결제 정보를 조회하는 방법은 무엇인가요?"
description: " "
date: 2023-11-08
tags: [javascript]
comments: true
share: true
---

Braintree JavaScript SDK는 간편하게 결제 처리를 관리할 수 있는 도구입니다. 특정 고객의 결제 정보를 조회하기 위해서는 고객 ID를 사용하여 Braintree의 Customer API를 호출해야 합니다.

```javascript
// Braintree SDK 초기화
var braintree = require('braintree');
var gateway = braintree.connect({
  environment: braintree.Environment.Sandbox, // or Production
  merchantId: 'your_merchant_id',
  publicKey: 'your_public_key',
  privateKey: 'your_private_key'
});

// 특정 고객의 결제 정보 조회
gateway.customer.find('customer_id', function (err, customer) {
  if (err) {
    console.log(err);
    return;
  }
  
  var paymentMethods = customer.paymentMethods;
  // 결제 정보를 사용하여 필요한 작업 수행
});
```

위의 코드에서 `customer_id`를 특정 고객의 ID로 변경하고, `your_merchant_id`, `your_public_key`, `your_private_key`를 생성된 Braintree 계정의 정보로 대체하면 됩니다.

위의 코드는 Braintree SDK를 사용하여 특정 고객의 결제 정보를 조회하는 방법을 보여줍니다. 반환된 `customer` 객체에는 해당 고객의 결제 정보 (paymentMethods) 등이 포함되어 있습니다.

더 자세한 내용은 Braintree JavaScript SDK 문서를 참고하시기 바랍니다. (https://developers.braintreepayments.com/guides/overview)