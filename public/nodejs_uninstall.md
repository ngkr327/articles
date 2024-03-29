---
title: Mac 環境から Node.js を アンインストールする話
tags:
  - Node.js
  - macOS
  - Uninstall
private: false
updated_at: '2023-04-29T08:04:42+09:00'
id: b02aa83d8eaff086385d
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

[Node.js](https://nodejs.org/ja/download) からパッケージ版でインストールした Node.js をアンインストールする個人的メモになります。

> 公式ページ

[Node.js HP](https://nodejs.org/)

## 環境

macOS Ventura 13.1

## アンインストール方法

### バージョンの確認

```
% node --version
v18.16.0

% which node
/usr/local/bin/node
```

### アンインストール

以下のコマンドを実行します。
パスワードを求められたらマシンのパスワードを入力します。

```
% sudo rm -rf /usr/local/{bin/{node,npm},lib/node_modules/npm,lib/node,share/man/*/node.*}

# アンインストールされたことの確認
% node --version
zsh: command not found: node
```
