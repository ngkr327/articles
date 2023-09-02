---
title: "M2 Mac に開発環境をセットアップした話"
tags: ["Mac", "M2", "Git", "VSCode", "Android"]
private: false
url: "https://qiita.com/ngkr327/items/cc5b199abddaa6739ca7"
---

## はじめに

M2 MacBook Pro に開発環境を構築したので個人的メモとしてまとめました。

## 環境

MacBook Pro M2 2022
macOS Ventura 13.1

## 初期設定

- Wi-Fi の設定

- Dock サイズの調整

- バッテリー割合の表示
  - [システム設定] > [コントロールセンター] > [バッテリー] と遷移し、[割合（%）を表示] を `ON` にします。

- Apple Music アプリの自動起動を停止する

  ```
  % launchctl unload -w /System/Library/LaunchAgents/com.apple.rcd.plist
  ```

## 環境構築

### **Homebrew**

> 公式ページ

[Homebrew](https://brew.sh/index_ja)

- インストール

a. 下記のコマンドを実行します。

```
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

b. 記載の通り環境変数を設定します。

```
% echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/<ユーザー名>/.zprofile
% eval "$(/opt/homebrew/bin/brew shellenv)"
```

c. バージョンを確認します。

```
% brew -v
Homebrew 3.6.17
Homebrew/homebrew-core (git revision b7861bb27c5; last commit 2023-01-04)

% which brew
/opt/homebrew/bin/brew
```

### **Git**

a. デフォルトでインストールされているバージョンを確認します。

```
% git --version
git version 2.37.1 (Apple Git-137.1)
```

- SSH を使用した GitHub への接続

b. SSH キーを .ssh 配下に配置します。

```
% cp id_rsa .ssh/
% chmod 600 .ssh/id_rsa
```

c. SSH キーを ssh-agent に追加します。

```
% ssh-add -K ~/.ssh/id_rsa
```

d. 登録されている SSH キーを確認します。

```
% ssh-add -l
```

e. `.ssh/config` に Host の設定を追加します。

```
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa
```

### **VSCode**

> 公式ページ

[Visual Studio Code](https://azure.microsoft.com/ja-jp/products/visual-studio-code/)

- ダウンロードとインストール

a. [ダウンロードサイト](https://code.visualstudio.com/Download) にアクセスし、Apple silicon 版をダウンロードします。

b. アプリケーションフォルダに Visual Studio Code.app をドラッグ＆ドロップします。

#### **Extensions**

- [Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server)
  - Web ページをプレビューするプラグイン

- [PlantUML](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml)
  - UML 図を記述できるプラグイン
    - 以下のコマンドで Graphviz をインストールします。

    ```
    % brew install graphviz
    ```

- [vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)
  - フォルダやファイルの種類をアイコンで表示するプラグイン

#### **Settings**

- Insert Final Newline: true
  - ファイルの末尾に改行を追加する

- Trim Final Newlines: true
  - ファイルの末尾の改行は１つだけにする

- Trim Trailing Whitespace: true
  - 行末の余分なスペースを削除する

- Word Wrap: on
  - テキストをエディターの幅で折り返して表示する

### **Android Studio**

> 公式ページ

[Android Developers](https://developer.android.com/)

- ダウンロードとインストール

a. [ダウンロードサイト](https://developer.android.com/studio) にアクセスし、Apple silicon 版をダウンロードします。

b. アプリケーションフォルダに Android Studio.app をドラッグ＆ドロップします。

- セットアップウィザード

c. アプリを起動し、セットアップウィザードを完了します。

- Android Debug Bridge（adb）の設定

d. 環境変数を設定します。

```
% echo 'export ANDROID_HOME=$HOME/Library/Android/sdk' >> .zprofile
% echo 'export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools' >> .zprofile
% source .zprofile
```

e. バージョンを確認します。

```
% adb version
Android Debug Bridge version 1.0.41
Version 33.0.3-8952118
Installed as /Users/<ユーザー名>/Library/Android/sdk/platform-tools/adb
```

### **Docker Desktop**

> 公式ページ

[Docker](https://www.docker.com/)

- Rosetta 2 のインストール

a. 以下のコマンドで、Rosetta 2 をインストールします。

```
% softwareupdate --install-rosetta
```

- ダウンロードとインストール

b. [ダウンロードサイト](https://docs.docker.com/desktop/install/mac-install/) にアクセスし、Apple silicon 版をダウンロードします。

c. アプリケーションフォルダに Docker.app をドラッグ＆ドロップします。

d. アプリを起動します。

### **Python**

a. デフォルトでインストールされているバージョンを確認します。

```
% python3 -V
Python 3.9.6

% which python3
/usr/bin/python3
```

- 仮想環境の構築

b. 仮想環境を作成します。

```
# 任意のディレクトリを作成し移動
% cd python-study

# 仮想環境の作成
% python3 -m venv ./venv
```

c. 作成した仮想環境を起動します。

```
% source ./venv/bin/activate
```

d. 仮想環境にパッケージをインストールします。

```
% pip3 install -r requirements.txt
```

e. 仮想環境を修了するには以下を実行します。

```
% deactivate
```

### **Ruby on Rails**

a. デフォルトでインストールされているバージョンを確認します。

```
% ruby -v
ruby 2.6.10p210 (2022-04-12 revision 67958) [universal.arm64e-darwin22]

% which ruby
/usr/bin/ruby
```

- rbenv のインストール

b. ruby-build と rbenv をインストールします。

```
% brew install ruby-build rbenv
```

c. 環境変数を設定します。

```
% echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> .zshrc
% echo 'eval "$(rbenv init -)"' >> .zshrc
% source .zshrc
```

d. バージョンを確認します。

```
% rbenv -v
rbenv 1.2.0
```

- Ruby のインストール

e. インストールできる Ruby のバージョンを確認します。

```
% rbenv install -l
```

f. ruby をインストールします。

```
% rbenv install 3.0.5

# 切り替え
% rbenv global 3.0.5
```

g. バージョンを確認します。

```
# バージョン一覧を確認
% rbenv versions
system
* 3.0.5 (set by /Users/<ユーザー名>/.rbenv/version)

# rbenv を更新
% rbenv rehash

# バージョンを確認
% ruby -v
ruby 3.0.5p211 (2022-11-24 revision ba5cf0f7c5) [arm64-darwin22]

% which ruby
/Users/<ユーザー名>/.rbenv/shims/ruby
```

h. gem コマンドの確認をします。

```
% gem -v
3.2.33

% which gem
/Users/<ユーザー名>/.rbenv/shims/gem
```

- rails のインストール

i. rails をインストールします。

```
% gem install rails
```

j. バージョンを確認します。

```
# rbenv を更新
% rbenv rehash

# バージョンを確認
% rails -v
Rails 7.0.4

% which rails
/Users/<ユーザー名>/.rbenv/shims/rails

% bundle -v
Bundler version 2.2.33

% which bundle
/Users/<ユーザー名>/.rbenv/shims/bundle
```

- 動作確認

k. rails でプロジェクトを作成します。

```
# 任意のディレクトリを作成し移動
% cd ruby-study

# rails プロジェクトの作成
% rails new helloworld
```

l. VSCode で上記プロジェクトを開いて実行します。

```
#  ARM アーキテクチャの確認
% uname -m
arm64

# ローカルサーバーを起動
% rails server
```

m. ブラウザで [http://127.0.0.1:3000](http://127.0.0.1:3000) にアクセスし、Rails アプリが表示されることを確認します。

### **Java**

- ダウンロードとインストール

a. [Azul](https://www.azul.com/downloads/?os=macos&architecture=arm-64-bit&package=jdk) にアクセスし、Apple silicon 版（Java8）をダウンロード、インストールします。

b. バージョンを確認します。

```
% java -version
openjdk version "1.8.0_352"
OpenJDK Runtime Environment (Zulu 8.66.0.15-CA-macos-aarch64) (build 1.8.0_352-b08)
OpenJDK 64-Bit Server VM (Zulu 8.66.0.15-CA-macos-aarch64) (build 25.352-b08, mixed mode)
```

### **Circle CI**

- ローカル CLI のインストール

a. 以下のコマンドで CLI をインストールします。

```
% brew install --ignore-dependencies circleci
```

### **AWS**

- AWS CLI のダウンロードとインストール

a. [インストーラー](https://awscli.amazonaws.com/AWSCLIV2.pkg) をダウンロードします。

b. ダウンロードしたファイルを実行し、インストール手順に従ってインストールします。

c. バージョンを確認します。

```
% aws --version
aws-cli/2.9.17 Python/3.9.11 Darwin/22.2.0 exe/x86_64 prompt/off

% which aws
/usr/local/bin/aws
```

- EB CLI のインストール

d. 以下のコマンドで EB CLI をインストールします。

```
% brew install awsebcli
```

e. バージョンを確認します。

```
% eb --version
EB CLI 3.20.3 (Python 3.11.)
```

### **Node.js**

> 公式ページ

[Node.js](https://nodejs.org/en/)

- Node.js のインストール

a. [インストーラー](https://nodejs.org/ja/download/) をダウンロードします。

b. ダウンロードしたファイルを実行し、インストール手順に従ってインストールします。

c. バージョンを確認します。

```
% node --version
v18.14.0

% which node
/usr/local/bin/node

% npm --version
9.3.1

% which npm
/usr/local/bin/npm
```

## その他のアプリケーション

- [AppCleaner](https://freemacsoft.net/appcleaner/)

- [Biscuit](https://eatbiscuit.com/)

- Google Chrome

- [IntelliJ IDEA](https://www.jetbrains.com/idea/)

- Slack

- [Sourcetree](https://www.sourcetreeapp.com/)

- Zoom Desktop Client
