---
title: "clasp を導入した話"
tags: ["GoogleAppsScript", "clasp"]
private: false
url: "https://qiita.com/ngkr327/items/31ff70142860eb4f9ec6"
---

## はじめに

既存の Google Apps Scirpt プロジェクトをコード管理するため、google/clasp を導入したのでその手順などを個人的メモとしてまとめました。

> 参考：clasp とは？

Google Apps Scirpt の CLI ツールとなります。Apps Script プロジェクトをローカルで開発できるようになります。

> 公式ページ

[clasp](https://github.com/google/clasp)

## 環境

Node.js `18.14.0`
npm `9.3.1`
clasp `2.4.2`

## 導入

### 準備

- clasp のインストールには `Node.js` がインストールされている必要があります。

  - `Node.js` のインストールは [こちらの記事](https://qiita.com/ngkr327/items/cc5b199abddaa6739ca7) を参照してください。

- [Google Apps Script API](https://script.google.com/home/usersettings) を有効にします。

### インストール

- `npm` コマンドを使用して clasp をインストールします。

```
% sudo npm install -g @google/clasp
```

- バージョンを確認します。

```
% clasp --version
2.4.2
```

## 開発

- 以下の流れで開発していきます。

1. ログイン
1. 【初回のみ】プロジェクトを新規作成 or 既存のプロジェクトをクローン
1. 【必要あれば】最新の状態をローカル環境に反映
1. コードの修正
    1. *.js として改修します。
1. アップロード
    1. *.gs ファイルに変換されて push されます。
1. ログアウト

### ログイン

- 以下のコマンドを使用して、Google アカウントの Apps Script プロジェクトにログインします。

  - ブラウザが起動するので承認します。

```
% clasp login
```

### 既存のプロジェクトのクローンを作成

- 以下のコマンドで、現在のディレクトリに既存のプロジェクトのクローンを作成します。

```
% cd <開発環境のフォルダ>
% clasp clone <Script ID>
```

> **NOTE:** クローンできない場合は、`.clasp.json` を削除して再度試してください。

### スクリプトのアップロード

- 以下のコマンドで、ファイルをすべてアップロードします。

```
% clasp push
```

### ログアウト

- 以下のコマンドでログアウトします。

```
% clasp logout
```

## その他のコマンド

### 新規 Apps Script プロジェクトの作成

- 新しいスクリプトを作成します。

```
% clasp create <Script Title>
```

### Apps Script プロジェクトの表示

- Apps Script エディタでプロジェクトを開きます。

```
% clasp open
```

### スクリプトのダウンロード

- ローカル環境に Apps Script プロジェクトをダウンロードします。

  - Apps Script エディタで修正した場合は、以下のコマンドを使用してローカル環境を更新します。

```
% clasp pull
```
