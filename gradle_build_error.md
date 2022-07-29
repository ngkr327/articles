---
title: "Could not find tools.jar. でビルドエラーになった話"
tags: ["gradle", "macos"]
private: false
url: "https://qiita.com/ngkr327/items/ce4a56658f8c1d2be410"
---

## はじめに

`Could not find tools.jar.` となりビルドができない問題に何回か遭遇、ハマっているのでアウトプットとして個人的にまとめました。
ターゲットは mac になります。

## 問題

ビルド実行時に `Could not find tools.jar.` となりビルドに失敗します。

```
> Could not find tools.jar. Please check that /Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home contains a valid JDK installation.
```

## 解決方法

メッセージにあるように `tool.jar` を所定の位置に配置すると解決します。
自分の環境ですと `/Users/<ユーザー名>/Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home/lib` にありましたのでコピーします。

```
$ cd //Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin/Contents/Home/lib/

# フォルダ内に tool.jar が存在しないことを確認
$ ls -alF

# コピー
$ sudo cp <コピー元のパス>/tools.jar ./
```

### 注意点

- ユーザーのライブラリフォルダー（ `/Users/<ユーザー名>/Library` ）ではないので注意が必要です。
ビルドができなくて焦ってしまい、初手はここを見に行ってしまうミスを何回かやらかしました...
