---
layout: post
title: "[javascript] Braintree JavaScript SDK를 사용하여 특정 결제 거래의 상태를 조회하는 방법은 무엇인가요?"
description: " "
date: 2023-11-08
tags: [javascript]
comments: true
share: true
---

먼저, Braintree 클라이언트 객체를 초기화해야 합니다. 이를 통해 Braintree의 기능을 사용할 수 있습니다. 아래는 초기화하는 방법을 보여주는 코드입니다.

```javascript
var clientToken = "<YOUR_CLIENT_TOKEN>";
var braintreeClient;


// Braintree 클라이언트 객체 초기화
braintree.client.create({
  authorization: clientToken
}, function (err, clientInstance) {
  if (err) {
    console.error(err);
    return;
  }

  braintreeClient = clientInstance;
  // Braintree 클라이언트 객체를 사용하여 결제 거래를 조회하는 함수 호출
  fetchTransactionStatus("<TRANSACTION_ID>");
});
```

Braintree 클라이언트 객체를 초기화한 후, `fetchTransactionStatus` 함수를 호출하여 특정 결제 거래의 상태를 조회할 수 있습니다. 아래는 `fetchTransactionStatus` 함수의 예시 코드입니다.

```javascript
function fetchTransactionStatus(transactionId) {
  // Braintree 클라이언트 객체를 사용하여 특정 결제 거래의 상태를 조회
  braintree.transaction.find(transactionId, function (err, transactionResult) {
    if (err) {
      console.error(err);
      return;
    }

    var transactionStatus = transactionResult.transaction.status;
    console.log("Transaction Status: " + transactionStatus);
  });
}
```

위의 코드에서 `<YOUR_CLIENT_TOKEN>`은 Braintree 계정에서 생성한 클라이언트 토큰을 대체해야 합니다. 또한 `<TRANSACTION_ID>`는 조회하려는 특정 결제 거래의 ID로 대체해야 합니다.

이 코드를 사용하면 Braintree JavaScript SDK를 활용하여 특정 결제 거래의 상태를 조회할 수 있습니다.

더 자세한 내용은 Braintree의 공식 문서를 참조하세요.

- [Braintree JavaScript SDK 문서](https://developers.braintreepayments.com/start/hello-client/javascript/v3)
- [Braintree API 문서](https://developers.braintreepayments.com/reference/general/overview)