---
title: FFmpeg コマンド一覧
tags:
  - ffmpeg
private: false
updated_at: '2023-09-01T22:23:36+09:00'
id: 073725350c3cf43364e0
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

FFmpeg を用いて動画を編集する機会があり、せっかくなので個人的によく使うコマンドをまとめました。

> 参考：FFmpeg とは？

動画ファイルの切り取り、リサイズ、静止画に切り出す、フレーム補間などの様々な処理を行えるツールとなります。

> 公式ページ

[FFmpeg HP](http://ffmpeg.org/)

## コマンド一覧

### ラウドネス値を調べる

```
$ ./ffmpeg -i input.mp4 -vn -filter_complex ebur128 -f null -
```

### フレームレート（fps）を変更する

`-r` オプションでフレームレートが指定できます。

```
$ ./ffmpeg -i input.mp4 -r 30 output.mp4
```

### 動画から音を削除する

`-an` オプションで音声データを削除することができます。

```
$ ./ffmpeg -i input.mp4 -vcodec copy -an output.mp4
```

### .mov から .mp4 に動画を変換する

QuickTime Player で再生させるためには `-pix_fmt yuv420p` オプションが必要です。


```
$ ./ffmpeg -i input.mp4 -pix_fmt yuv420p output.mp4
```
