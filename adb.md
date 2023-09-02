---
title: "adb コマンド一覧"
tags: ["Android", "adb"]
private: false
url: "https://qiita.com/ngkr327/items/1d371de69f7851971a1c"
---

## はじめに

今更ながらせっかくなので個人的によく使う adb のコマンドをまとめました。

> 参考：Android Debug Bridge (adb) とは？

Android デバイスと通信するための多用途のコマンドラインツールになります。
adb コマンドを使用すると、アプリのインストールやデバッグなど、さまざまなデバイス操作を実行できます。（公式より）

> 公式ページ

[Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb)

> サンプルソース

- GitHub
[adbtool-for-mac](https://github.com/ngkr327/adbtool-for-mac)

## 環境

macOS Ventura 13.1

## コマンド一覧

### IP アドレスを使用してデバイスに接続する

```
$ adb connect <device_ip_address>
```

### 接続済みデバイスのリストを取得する

```
$ adb devices
```

### エミュレータまたは接続されたデバイスに apk をインストールする

```
$ adb install -r <path_to_apk>
```

### デバイスからトレース情報を取得する

Android では、ANR が発生するとトレース情報が保存されます。

```
$ adb pull /data/anr/traces.txt ./
```

### デバイスにファイルをコピーする

```
$ adb push <pc> <dvice>

// ダウンロードフォルダにコピー
$ adb push <file> /sdcard/Download/
```

### 指定したパッケージをデバイスオーナー設定する

アクティブな管理者として設定し、そのパッケージをデバイスオーナーとして設定します。
パッケージ名/デバイスアドミンを実装したクラス名を component に指定します。

```
$ adb shell dpm set-device-owner <component>
```

### デバイスにインストールされているパッケージの一覧を取得する

```
$ adb shell pm list package
```
