---
title: "javax.xml.bind.JAXBException でビルドエラーになった話"
tags: ["Android", "gradle", "AndroidStudio"]
private: false
url: "https://qiita.com/ngkr327/items/ba09444e5d4dd85901b5"
---

## はじめに

Android Studio で `Unable to load class 'javax.xml.bind.JAXBException'.` となりビルドができない問題についてのアウトプットとして個人的メモとしてまとめました。

## 環境

macOS Ventura 13.1
Android Studio Dolphin | 2021.3.1 Patch 1

## 問題

ビルド実行時に `Unable to load class 'javax.xml.bind.JAXBException'.` となりビルドに失敗します。

```
Unable to load class 'javax.xml.bind.JAXBException'.

This is an unexpected error. Please file a bug containing the idea.log file.
```

## 解決方法

AGP のバージョンを更新すると解決します。

```build.gradle
dependencies {
    classpath 'com.android.tools.build:gradle:7.3.1'
}
```

```gradle-wrapper.properties
distributionUrl=https\://services.gradle.org/distributions/gradle-7.4-bin.zip
```
