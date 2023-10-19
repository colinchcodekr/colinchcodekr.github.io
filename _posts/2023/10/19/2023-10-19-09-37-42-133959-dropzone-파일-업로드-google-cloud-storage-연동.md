---
layout: post
title: "[javascript] Dropzone 파일 업로드 Google Cloud Storage 연동"
description: " "
date: 2023-10-19
tags: [javascript]
comments: true
share: true
---

Dropzone은 웹 애플리케이션에서 사용자가 파일을 쉽게 업로드할 수 있도록 도와주는 JavaScript 라이브러리입니다. 이 블로그 포스트에서는 Dropzone을 사용하여 파일을 Google Cloud Storage에 업로드하는 방법에 대해 알아보겠습니다.

## 1. Google Cloud Storage 설정

먼저 Google Cloud Platform 콘솔에서 프로젝트를 생성하고, Cloud Storage 서비스를 활성화해야 합니다. [여기](https://console.cloud.google.com/)에서 Google Cloud Platform 콘솔로 이동하여 프로젝트를 생성하고 Cloud Storage 서비스를 활성화합니다.

그런 다음, Google Cloud Storage에 버킷을 생성하고 업로드 할 파일이 저장될 위치를 지정해야합니다.

## 2. Dropzone 설정

Dropzone을 사용하기 위해 먼저 Dropzone 라이브러리를 다운로드하고 프로젝트에 포함시킵니다. Dropzone의 최신 버전은 [여기](https://www.dropzonejs.com/)에서 다운로드할 수 있습니다. 다운로드 한 파일을 프로젝트의 적절한 위치에 추가합니다.

다음으로, Dropzone 설정을 구성해야합니다. HTML에서 Dropzone을 생성하고 필요한 구성 옵션을 지정해야합니다. 예를 들어, 아래는 Dropzone 컨테이너를 생성하는 HTML 코드입니다.

```html
<div id="my-dropzone" class="dropzone"></div>
```

Dropzone은 기본적으로 파일을 서버에 POST 요청으로 전송합니다. 그러나 이번 예제에서는 파일을 Google Cloud Storage에 직접 업로드하기 때문에 Dropzone의 `url` 구성 옵션을 지정하지 않아도 됩니다.

## 3. 파일 업로드 처리

Dropzone은 파일을 업로드하기 전에 `addedfile` 이벤트를 트리거합니다. 이 이벤트를 사용하여 업로드 될 파일을 Google Cloud Storage에 전송할 수 있습니다.

아래는 JavaScript 코드에서 Dropzone 이벤트 리스너를 정의하는 방법입니다.

```javascript
Dropzone.options.myDropzone = {
  init: function () {
    this.on("addedfile", function (file) {
      // 파일 업로드 로직 구현 Here
    });
  },
};
```

이제 `addedfile` 이벤트가 트리거될 때 업로드 될 파일을 처리하는 로직을 구현해야합니다. 구체적인 Google Cloud Storage에 파일을 업로드하는 방법에 대해서는 Google Cloud Storage 클라이언트 라이브러리를 사용해야합니다. 필요한 경우, 해당 라이브러리를 다운로드하고 사용방법에 대해 [문서](https://cloud.google.com/nodejs/docs/reference/storage/2.3.x)를 참조하십시오.

## 4. 파일 링크 생성

파일이 Google Cloud Storage에 성공적으로 업로드되면 해당 파일에 대한 다운로드 링크를 생성할 수 있습니다. 이를 위해 Google Cloud Storage의 버킷 및 파일의 URL 구조에 따라 링크를 생성하면 됩니다. 필요한 경우, 그에 따라 서명된 URL을 생성하여 파일에 대한 인증을 추가 할 수도 있습니다.

```javascript
var fileUrl = `https://storage.googleapis.com/${bucketName}/${fileName}`;
```

이제 Dropzone을 사용하여 파일을 Google Cloud Storage에 업로드하는 방법을 알게 되었습니다. 이를 통해 웹 애플리케이션에서 사용자가 파일을 손쉽게 업로드하고 Google Cloud Storage에서 관리하고 액세스 할 수 있습니다.

더 자세한 내용은 [Dropzone 문서](https://www.dropzonejs.com/)와 [Google Cloud Storage 문서](https://cloud.google.com/storage/docs/)를 참조하십시오.