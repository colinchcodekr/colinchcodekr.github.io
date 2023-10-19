---
layout: post
title: "[javascript] Dropzone 파일 업로드 Azure Blob Storage 연동"
description: " "
date: 2023-10-19
tags: [javascript]
comments: true
share: true
---

Azure Blob Storage는 Microsoft Azure의 객체 스토리지 서비스로서 파일 저장 및 관리를 위한 솔루션을 제공합니다. Dropzone은 웹 페이지에서 파일 업로드를 쉽게 처리할 수 있도록 도와주는 JavaScript 라이브러리입니다. 이번 포스트에서는 Dropzone을 사용하여 파일을 Azure Blob Storage에 업로드하는 방법을 알아보겠습니다.

## 1. Dropzone 설치 및 설정

먼저, Dropzone을 설치하고 기본 설정을 구성해야합니다. 아래의 스크립트를 웹 페이지에 추가하여 Dropzone을 로드합니다.

```html
<script src="path/to/dropzone.min.js"></script>
<link rel="stylesheet" href="path/to/dropzone.min.css">
```

다음으로, Dropzone 인스턴스를 생성하고 필요한 설정을 추가해야합니다. 아래 예시 코드를 참고하여 Dropzone을 초기화합니다.

```javascript
var dropzone = new Dropzone("#my-dropzone", {
  url: "upload.php",  // 파일 업로드를 처리할 서버 스크립트의 URL
  params: {},  // 추가적인 파라미터 (ex: 토큰, 폴더 경로 등)
  autoProcessQueue: true,  // 파일이 추가되면 자동으로 업로드할지 여부
  maxFilesize: 10,  // 업로드 가능한 최대 파일 크기 (MB)
  acceptedFiles: ".jpg,.png,.pdf",  // 허용되는 파일 형식
  // 이벤트 핸들러 등 추가적인 설정
});
```

위 코드에서 `url`은 파일 업로드를 처리할 서버 스크립트의 URL을 지정하는 부분입니다. Azure Blob Storage와의 연동을 위해 이 URL을 Azure Function 또는 Express.js와 같은 서버 프레임워크에서 처리할 수 있습니다.

## 2. 서버 스크립트 작성

Azure Blob Storage와 연동하기 위해 서버 스크립트를 작성해야합니다. 서버 스크립트는 업로드된 파일을 Azure Blob Storage에 저장하고 업로드된 파일의 URL을 클라이언트로 반환해야합니다.

아래는 Node.js 환경에서 Azure Blob Storage와 연동하는 예제 코드입니다.

```javascript
const { BlobServiceClient } = require('@azure/storage-blob');

// Blob 서비스에 연결
const connectionString = "<blob storage connection string>";
const containerName = "<container name>";
const blobServiceClient = BlobServiceClient.fromConnectionString(connectionString);
const containerClient = blobServiceClient.getContainerClient(containerName);

// 파일 업로드 및 URL 반환 처리 
async function uploadFileToBlobStorage(file) {
  const blobName = file.name;  // Blob에 저장될 파일 이름
  const blockBlobClient = containerClient.getBlockBlobClient(blobName);
  await blockBlobClient.uploadData(file.data);
  return blockBlobClient.url;
}

// 업로드 요청 처리
app.post("/upload", async function(req, res) {
  const file = req.files[0];  // Dropzone에서 업로드된 파일
  const fileUrl = await uploadFileToBlobStorage(file);
  res.send(fileUrl);
});
```

위 코드에서 `<blob storage connection string>`과 `<container name>`은 개별적으로 Azure Portal에서 확인하고 설정해야합니다.

## 3. 웹 페이지 구성

마지막으로, 웹 페이지를 구성하여 Dropzone을 표시하고 업로드된 파일을 Azure Blob Storage에 전송하도록 설정해야합니다. 예를 들어, 아래와 같이 HTML 코드를 작성할 수 있습니다.

```html
<!-- Dropzone 컨테이너 -->
<div id="my-dropzone" class="dropzone"></div>
```

위 코드에서 `#my-dropzone`는 Dropzone 인스턴스가 만들어질 DOM 요소의 ID입니다. CSS 클래스 `dropzone`는 Dropzone 스타일을 적용하기 위해 추가됩니다.

## 결론

이제, Dropzone을 사용하여 웹 페이지에서 파일 업로드를 Azure Blob Storage에 연동하는 방법을 알아보았습니다. Dropzone의 다양한 설정 및 이벤트 핸들러를 활용하여 UI/UX를 개선하고, Azure Blob Storage에서 제공하는 기능을 활용하여 파일 관리 용이성을 높일 수 있습니다.

---

**참고 자료:**

- Dropzone 공식 문서: [https://www.dropzonejs.com/](https://www.dropzonejs.com/)
- Azure Blob Storage JavaScript SDK 문서: [https://docs.microsoft.com/javascript/api/azure-storage-blob/](https://docs.microsoft.com/javascript/api/azure-storage-blob/)
- Azure Blob Storage 연동 예제 코드: [https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/storage/storage-blob/samples/javascript](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/storage/storage-blob/samples/javascript)