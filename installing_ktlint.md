---
title: "ktlint を導入した話"
tags: ["Android", "Kotlin", "Ktlint"]
private: false
url: "https://qiita.com/ngkr327/items/fcc2b3dc4e388abcfef3"
---

## はじめに

今更ながら ktlint を導入する機会があったので、その手順などをまとめました。

> 参考：ktlint とは？

ざっくり、[Kotlin Style Guide](https://developer.android.com/kotlin/style-guide) を元にコードスタイルのチェックをしてくれたり、lint で検出した部分にフォーマットをかけてくれたりしてくれる Kotlin 用の静的コード解析ツールになります。

> 公式ページ

[ktlint HP](https://ktlint.github.io/)

> サンプルソース

- GitHub
[simple-ktlint-android](https://github.com/ngkr327/simple-ktlint-android)

## 導入

### 1. やりたいこと

- ktlint でコードをフォーマットしたい
- さらに、ビルド時にフォーマットが走るようにしたい

### 2. 準備

Android Studio: `3.4.1`
ktlint: `0.4.0`

### 3. 導入

（ktlint の [README](https://github.com/pinterest/ktlint/blob/master/README.md) のとおり）Gradle へ依存関係の追加と、ktlint を実行するためのタスクを追加します。

```app/build.gradle

configurations {
    ktlint
}

dependencies {
    ktlint "com.pinterest:ktlint:0.40.0"
}

task ktlint(type: JavaExec, group: "verification") {
    description = "Check Kotlin code style."
    classpath = configurations.ktlint
    main = "com.pinterest.ktlint.Main"
    args "src/**/*.kt"
}
check.dependsOn ktlint

task ktlintFormat(type: JavaExec, group: "formatting") {
    description = "Fix Kotlin code style deviations."
    classpath = configurations.ktlint
    main = "com.pinterest.ktlint.Main"
    args "-F", "src/**/*.kt"
}
```

プロジェクトのルートディレクトリで

```
$ ./gradlew ktlint
```

を実行すると結果が出力されます。また、

```
$ ./gradlew ktlintFormat
```

を実行すると、lint で検出されたコードにフォーマットをかけてくれます。

### Option #1

チェックにひっかかっても途中で終了させないようにするために `ignoreExitValue true` を設定します。

```
task ktlint(type: JavaExec, group: "verification") {
    ignoreExitValue true
}

task ktlintFormat(type: JavaExec, group: "formatting") {
    ignoreExitValue true
}
```

### Option #2

ビルド時にフォーマットをしたいので以下も追加します。

```app/build.gradle

tasks.whenTaskAdded { task ->
    task.dependsOn ktlintFormat
}
```

これにより毎回コマンドを実行しなくても、ビルド時にフォーマットしてくれるようになります。コミット後のフォーマットの修正漏れの予防にもなります。

## ちょっとひとこと

お読みいただきありがとうございます。
今回は基本的な ktlint の導入と使い方をまとめました。
皆様の参考になれば幸いです。
