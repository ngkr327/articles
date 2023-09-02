---
title: "Android で端末の充電状態を監視するようにした話"
tags: ["Android", "Kotlin", "battery"]
private: false
url: "https://qiita.com/ngkr327/items/112885cad9806e233b9d"
---

## はじめに

バッテリーの充電状況を取得するための備忘録メモとなります。
その他、BatteryManager では電池残量やバッテリーの状態などを得ることができます。

> Android Developers Reference

[BatteryManager](https://developer.android.com/reference/android/os/BatteryManager)

> サンプルソース

- GitHub
[simple-battery-android](https://github.com/ngkr327/simple-battery-android)

## BroadcastReceiver をマニフェストに登録

AndroidManifest.xml に以下を追加します。

```
<receiver android:name=".PowerConnectionReceiver"
    android:exported="false">
    <intent-filter>
        <action android:name="android.intent.action.ACTION_POWER_CONNECTED"/>
        <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED"/>
    </intent-filter>
</receiver>
```

## 充電状態の変化を監視する

```Kotlin
// Kotlin
class PowerConnectionReceiver : BroadcastReceiver() {

    override fun onReceive(context: Context?, intent: Intent?) {
        val status = when(intent?.getIntExtra(BatteryManager.EXTRA_STATUS, -1) ?: -1) {
            BatteryManager.BATTERY_STATUS_CHARGING -> "充電中"
            BatteryManager.BATTERY_STATUS_DISCHARGING -> "放電中"
            BatteryManager.BATTERY_STATUS_FULL -> "充電完了"
            BatteryManager.BATTERY_STATUS_NOT_CHARGING -> "未充電"
            BatteryManager.BATTERY_STATUS_UNKNOWN -> "UNKNOWN"
            else -> "不明"
        }
    }
}
```
