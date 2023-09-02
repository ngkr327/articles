---
title: "Android の Wi-Fi 関連の実装についての話"
tags: ["Android", "Kotlin", "WiFi"]
private: false
url: "https://qiita.com/ngkr327/items/dabd90aebe7caaf5b743"
---

## はじめに

今更ながら Android で Wi-Fi まわりの実装を行う機会があったので個人的にまとめました。
いくつかのメソッドは `This method was deprecated in API level 29.` なので注意が必要です。

> Android Developers Reference

- [WifiManager](https://developer.android.com/reference/android/net/wifi/WifiManager)

- [WifiInfo](https://developer.android.com/reference/android/net/wifi/WifiInfo)

## パーミッション

AndroidManifest.xml に以下を追加します。

```
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
```

## Wi-Fi が有効かどうか取得する

Wi-Fi が有効か無効かを取得します。

```Java
// Java
WifiManager manager = (WifiManager) getSystemService(WIFI_SERVICE);
boolean enabled = manager.isWifiEnabled();
```

```Kotlin
// Kotlin
val manager = applicationContext.getSystemService(WIFI_SERVICE) as WifiManager
val enabled = manager.isWifiEnabled
```

## Wi-Fi の情報を取得する

- SSID

```Java
// Java
WifiManager manager = (WifiManager) getSystemService(WIFI_SERVICE);
WifiInfo info = manager.getConnectionInfo();
String ssid = info.getSSID();
```

## Wi-Fi に接続する

登録済みの Wi-Fi に接続します。

```Java
// Java
WifiManager manager = (WifiManager) getSystemService(WIFI_SERVICE);
WifiConfiguration config = null;
for (WifiConfiguration network : manager.getConfiguredNetworks()) {
    if (network.SSID.equals('"' + `ssid` + '"')) {
        config = network;
        break;
    }
}
if (config != null) {
    wm.enableNetwork(config.networkId, true);
}
```

## Wi-Fi を切断する

Wi-Fi を無効にします。

```Java
// Java
WifiManager manager = (WifiManager) getSystemService(WIFI_SERVICE);
WifiInfo info = manager.getConnectionInfo();
manager.disableNetwork(info.getNetworkId());
```
