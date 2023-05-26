---
title: "adb コマンドでファイルを端末に転送する話"
tags: ["Android", "adb"]
private: false
url: "https://qiita.com/ngkr327/items/aa2afe4e0ed4f928a22d"
---

## はじめに

マシンにあるファイルを Android 端末に adb コマンドで送る際に使い方を備忘録としてまとめます。

## 環境

macOS Ventura 13.1

## デバイスにファイルをコピーする

```
$adb push <pc> <dvice>
```

- ダウンロードフォルダにコピーする

```
$ adb push <file> /sdcard/Download/
```
