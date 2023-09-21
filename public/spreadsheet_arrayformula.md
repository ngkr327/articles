---
title: ARRAYFOMULA 関数で複数行のそれぞれの合計を計算する話
tags:
  - spreadsheet
  - ARRAYFORMULA
private: false
updated_at: '2022-06-25T08:05:36+09:00'
id: 018971759f6099400e72
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

スプレッドシートにある ARRAYFOMULA 関数の備忘録まとめとなります。

> 公式ページ

[ARRAYFORMULA](https://support.google.com/docs/answer/3093275)

> サンプルソース

- スプレッドシート
[arrayformula](https://docs.google.com/spreadsheets/d/1VbyiFZ5z9NT_UmhChrGKRm3qPIBSW8bR4SKw02KZGMA/edit?usp=sharing)

## SUM 関数を使う方法

ARRAYFORMULA(SUMIF(IF(COLUMN(1行目の範囲),ROW(1列目の範囲)),ROW(1列目の範囲),全体の範囲))

```
=ARRAYFORMULA(SUMIF(IF(COLUMN(B2:D2),ROW(B2:B6)),ROW(B2:B6),B2:D6))
```
