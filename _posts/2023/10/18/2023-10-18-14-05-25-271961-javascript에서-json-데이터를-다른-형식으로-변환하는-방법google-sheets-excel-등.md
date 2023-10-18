---
layout: post
title: "[javascript] JavaScript에서 JSON 데이터를 다른 형식으로 변환하는 방법(Google Sheets, Excel 등)"
description: " "
date: 2023-10-18
tags: [javascript]
comments: true
share: true
---

JSON(JavaScript Object Notation)은 데이터를 효율적으로 저장하고 전달하기 위해 사용되는 형식입니다. 하지만 JSON 데이터를 가독성이 높은 다른 형식으로 변환해야 할 때도 있습니다. 이번 블로그 포스트에서는 JavaScript를 사용하여 JSON 데이터를 Google Sheets, Excel 등의 다른 형식으로 변환하는 방법을 알아보겠습니다.

## 1. JSON 데이터를 Google Sheets로 변환하기

Google Sheets는 웹 기반 스프레드시트 애플리케이션으로, 데이터를 테이블 형식으로 표현할 수 있습니다. 다음은 JSON 데이터를 Google Sheets로 변환하는 방법입니다.

```javascript
// JSON 데이터
const jsonData = [
  {
    name: "John",
    age: 30,
    city: "New York"
  },
  {
    name: "Jane",
    age: 25,
    city: "London"
  }
];

// Google Sheets로 변환하는 함수
function convertToGoogleSheets(jsonData) {
  let sheetData = [];

  // 헤더 생성
  const headerRow = Object.keys(jsonData[0]);
  sheetData.push(headerRow);

  // 데이터 생성
  jsonData.forEach(data => {
    const rowData = Object.values(data);
    sheetData.push(rowData);
  });

  return sheetData;
}

// 변환된 데이터를 Google Sheets에 입력
const sheetData = convertToGoogleSheets(jsonData);
sheetData.forEach(rowData => {
  const row = rowData.join("\t");
  console.log(row);
  // Google Sheets에 입력하는 로직 추가
});
```

위의 코드에서 `jsonData`는 변환하고자 하는 JSON 데이터를 나타냅니다. `convertToGoogleSheets` 함수는 JSON 데이터를 Google Sheets 형식으로 변환하여 `sheetData` 배열에 저장합니다. 그리고 `sheetData`를 Google Sheets에 입력하는 로직을 추가하면 됩니다.

## 2. JSON 데이터를 Excel로 변환하기

Excel은 마이크로소프트에서 개발한 스프레드시트 애플리케이션으로, 다양한 데이터 가공 및 분석 작업을 지원합니다. 다음은 JSON 데이터를 Excel로 변환하는 방법입니다.

```javascript
// JSON 데이터
const jsonData = [
  {
    name: "John",
    age: 30,
    city: "New York"
  },
  {
    name: "Jane",
    age: 25,
    city: "London"
  }
];

// Excel로 변환하는 함수
function convertToExcel(jsonData) {
  let excelData = "Name\tAge\tCity\n"; // 헤더 생성

  // 데이터 생성
  jsonData.forEach(data => {
    const rowData = Object.values(data).join("\t");
    excelData += rowData + "\n";
  });

  return excelData;
}

// 변환된 데이터를 파일로 저장
const excelData = convertToExcel(jsonData);
console.log(excelData);
// 파일로 저장하는 로직 추가
```

위의 코드에서 `jsonData`는 변환하고자 하는 JSON 데이터를 나타냅니다. `convertToExcel` 함수는 JSON 데이터를 Excel 형식으로 변환하여 `excelData` 문자열에 저장합니다. 그리고 `excelData`를 파일로 저장하는 로직을 추가하면 됩니다.

## 결론

이번에는 JavaScript를 사용하여 JSON 데이터를 Google Sheets, Excel 등의 다른 형식으로 변환하는 방법을 알아보았습니다. 이러한 변환 기능을 활용하면 JSON 데이터를 다양한 형식으로 효율적으로 활용할 수 있습니다. 참고로, 실제 구현 시에는 해당 형식에 맞춰서 데이터를 변환하고 저장하는 로직을 추가해야 합니다.