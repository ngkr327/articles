---
title: Google Apps Script でスプレッドシートの最終行に値をコピーする話
tags:
  - GoogleAppsScript
  - spreadsheet
private: false
updated_at: '2022-09-24T08:42:43+09:00'
id: ab43e4bc51a408389664
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Google Apps Script (GAS) の `copyTo()` 関数を使ってスプレッドシートのセルをコピー＆ペーストします。

> Apps Script リファレンス

[copyTo(destination)](https://developers.google.com/apps-script/reference/spreadsheet/range#copytodestination)

## サンプルコード

```
function onCopy() {
  const spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
  const source = spreadsheet.getSheetByName("<コピー元のシート名>").getRange("<セルの範囲>");
  const row = source.getLastRow();
  const column = source.getLastColumn();

  // コピー
  const sheet = spreadsheet.getSheetByName("<コピー先のシート名>");
  const insert = sheet.getLastRow() + 1;
  const destination = sheet.getRange(insert, 1, row, column);
  source.copyTo(destination);
}
```
