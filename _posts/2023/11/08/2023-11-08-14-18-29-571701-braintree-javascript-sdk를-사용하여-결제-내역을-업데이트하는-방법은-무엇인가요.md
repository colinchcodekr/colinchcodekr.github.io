---
layout: post
title: "[javascript] Braintree JavaScript SDK를 사용하여 결제 내역을 업데이트하는 방법은 무엇인가요?"
description: " "
date: 2023-11-08
tags: [javascript]
comments: true
share: true
---

먼저, Braintree JavaScript SDK를 프로젝트에 추가해야 합니다. CDN을 통해 스크립트를 로드하거나 npm을 통해 패키지를 설치할 수 있습니다. 다음은 CDN을 사용하는 예시입니다:

```html
<script src="https://js.braintreegateway.com/web/3.90.1/js/client.min.js"></script>
<script src="https://js.braintreegateway.com/web/3.90.1/js/hosted-fields.min.js"></script>
```

이제 결제 내역을 업데이트하는 코드를 작성해보겠습니다. Braintree JavaScript SDK는 클라이언트 사이드에서 실행되므로 신용 카드 정보 등 민감한 데이터를 안전하게 처리할 수 있습니다.

```javascript
var clientToken = 'YOUR_CLIENT_TOKEN'; // Braintree 클라이언트 토큰
var gateway = braintree.client.create({
  authorization: clientToken
}, function (err, clientInstance) {
  if (err) {
    console.error(err);
    return;
  }

  braintree.hostedFields.create({
    client: clientInstance,
    styles: {
      'input': {
        'font-size': '16px',
        'font-family': 'courier, monospace',
        'font-weight': 'lighter',
        'color': '#ccc'
      }
    },
    fields: {
      number: {
        selector: '#card-number'
      },
      cvv: {
        selector: '#cvv'
      },
      expirationDate: {
        selector: '#expiration-date'
      }
    }
  }, function (err, hostedFieldsInstance) {
    if (err) {
      console.error(err);
      return;
    }

    // 결제 내역 업데이트 로직을 작성합니다.
    // 예시: hostedFieldsInstance.on('blur', updatePayment);

    // 결제 정보를 서버로 전송하는 함수
    function updatePayment(event) {
      hostedFieldsInstance.tokenize(function (err, payload) {
        if (err) {
          console.error(err);
          return;
        }

        // payload를 서버로 전송하여 결제 내역을 업데이트합니다.
        // 예시: fetch('/update-payment', {
        //          method: 'POST',
        //          body: JSON.stringify({ paymentMethodNonce: payload.nonce })
        //        }).then(function(response) {
        //          // 결제 내역이 업데이트된 후의 로직
        //        });
      });
    }
  });
});
```

위 코드에서 `YOUR_CLIENT_TOKEN`을 Braintree에서 발급한 클라이언트 토큰으로 대체해야 합니다. 또한, `hostedFieldsInstance.on('blur', updatePayment)`를 사용하여 결제 입력 필드(`#card-number`, `#cvv`, `#expiration-date`) 중 하나에서 블러(blur) 이벤트가 발생했을 때 `updatePayment` 함수가 호출되도록 설정할 수 있습니다.

`updatePayment` 함수는 `hostedFieldsInstance.tokenize` 메소드를 사용하여 결제 정보를 토큰화한 후, 해당 토큰을 서버로 전송하여 결제 내역을 업데이트하는 로직을 작성해야 합니다. 예시 코드에는 `fetch` 함수를 사용하여 POST 요청을 보내고, 응답을 처리하는 코드도 포함되어 있습니다.

이제 Braintree JavaScript SDK를 사용하여 결제 내역을 업데이트하는 방법에 대해 알게 되었습니다. Braintree의 공식 문서와 개발 가이드를 참조하여 보다 자세한 내용을 확인할 수 있습니다.