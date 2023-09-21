---
title: Google Apps Script でスプレッドシートにカスタムメニューを追加する話
tags:
  - GoogleAppsScript
  - spreadsheet
private: false
updated_at: '2022-10-29T09:10:13+09:00'
id: 9cb2cf989d5da750a4b1
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Google Apps Script（GAS）のトリガーを使って、スプレッドシートにカスタムメニューを追加することができます。

> Apps Script リファレンス

[onOpen(e)](https://developers.google.com/apps-script/guides/triggers#onopene)

## トリガーを使用

GAS のトリガー `onOpen(e)` はユーザーが Google ドキュメント、スプレッドシート、スライド、フォームのファイルを開いたときに自動的に実行されます。
この関数を使用して独自のメニューを追加します。

```
function onRefresh() {
  // do something
}

/* ファイルを開いたときのイベントハンドラ */
function onOpen() {
  var ui = SpreadsheetApp.getUi();
  var menu = ui.createMenu("ワークフロー");
  menu.addItem("データを更新", "onRefresh");
  menu.addToUi();
}
```
