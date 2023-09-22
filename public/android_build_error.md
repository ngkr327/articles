---
title: Android でビルドエラーになった話
tags:
  - Android
  - gradle
  - AndroidStudio
private: false
updated_at: '2023-09-23T08:01:16+09:00'
id: 70b8a8314c08660cd611
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Android Studio でビルドができない問題について個人的メモとしてまとめました。

## 環境

macOS Ventura 13.1
Android Studio Dolphin | 2021.3.1 Patch 1

## エラー #1

`Could not find tools.jar.` となりビルドができない

```
> Could not find tools.jar. Please check that /Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home contains a valid JDK installation.
```

### 解決方法

メッセージにあるように `tool.jar` を所定の位置に配置すると解決します。
私の環境ですと `/Users/<ユーザー名>/Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home/lib` にありましたのでコピーしました。

```
$ cd //Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin/Contents/Home/lib/

# フォルダ内に tool.jar が存在しないことを確認
$ ls -alF

# コピー
$ sudo cp <コピー元のパス>/tools.jar ./
```

### 注意点

- ユーザーのライブラリフォルダー（ `/Users/<ユーザー名>/Library` ）ではないので注意が必要です。

## エラー #2

`Unable to load class 'javax.xml.bind.JAXBException'.` となりビルドができない

```
Unable to load class 'javax.xml.bind.JAXBException'.

This is an unexpected error. Please file a bug containing the idea.log file.
```

### 解決方法

AGP のバージョンを更新すると解決します。

```build.gradle
dependencies {
    classpath 'com.android.tools.build:gradle:7.3.1'
}
```

```gradle-wrapper.properties
distributionUrl=https\://services.gradle.org/distributions/gradle-7.4-bin.zip
```
