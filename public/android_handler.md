---
title: Android で指定した時間後に処理を行う方法についての話
tags:
  - Android
  - Handler
private: false
updated_at: '2023-09-01T22:43:28+09:00'
id: e21dfb12d39f48f4b08f
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Android で指定された時間後に処理を実行する方法についての備忘録まとめとなります。
「10 秒後に処理を実行したい！」「1 分間隔で繰り返し実行したい。」などの時に実装します。

> Android Developers Reference

- [Handler](https://developer.android.com/reference/android/os/Handler)

## 10 秒後に処理を実行する

```Java
// Java
Handler handler = new Handler();
handler.postDelayed(new Runnable() {
    @Override
    public void run() {
        // do something
    }
}, 10 * 1000);
```

```Kotlin
// Kotlin
val handler = Handler(Looper.getMainLooper())
handler.postDelayed({
    // do something
}, 10 * 1000)
```

## 1 分間隔で処理を繰り返し実行する

```Java
// Java
final int delayMillis = 1 * 60 * 1000;
final Handler handler = new Handler();
handler.postDelayed(new Runnable() {
    @Override
    public void run() {
        // do something

        handler.postDelayed(this, delayMillis);
    }
}, delayMillis);
```

```Kotlin
// Kotlin
val delayMillis: Long = 1 * 60 * 1000
val handler = Handler(Looper.getMainLooper())
val runnable = object : Runnable{
    override fun run() {
        // do something

        handler.postDelayed(this, delayMillis)
    }
}
handler.postDelayed(runnable, delayMillis)
```
