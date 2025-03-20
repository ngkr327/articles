---
title: ffmpeg を使って画像に動画を合成する話
tags:
  - ffmpeg
private: false
updated_at: '2025-03-20T21:03:35+09:00'
id: b3d7bc5c762a9ec6f74e
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

FFmpeg を使って画像に動画を合成する、画像を背景にして動画を重ねる方法を個人的にまとめました。

## 動画を画像の上に重ねる

### 基本的な方法

```
$ ./ffmpeg -i image.png -i video.mp4 -filter_complex "[0][1]overlay=0:0" output.mp4
```

`image.png`: 背景にする画像ファイル
`video.mp4`: 重ねたい動画ファイル
`overlay`: 画像上の座標（動画の表示位置）
`output.mp4`: 出力ファイル名

### 動画のサイズを変更して重ねる

```
$ ./ffmpeg -i image.png -i video.mp4 -filter_complex "[1]scale=680:512[v];[0][v]overlay=62:38" output.mp4
```

`[1]scale=680:512[v]`: 動画のサイズを 680:512 にリサイズ
`[0][v]overlay=62:38`: 画像の (62, 38) の位置に動画を配置

## 素材提供
いらすとや様
https://www.irasutoya.com/

Pexels 様
https://www.pexels.com/
