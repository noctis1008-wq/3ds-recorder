# r3d2video — 録画を PC で高画質な動画に

本体が作る MP4 はスマホ向け（400 × 480、強めの圧縮）です。`r3d2video` は録画ファイル
（SD の `/3ds/recorder/recordings/` にある `.r3d`）を、YouTube 用・編集用・完全保存用の動画にします。

## Windows

1. ffmpeg を一度だけ入れます：`winget install --id Gyan.FFmpeg -e`
   （または `ffmpeg.exe` を `r3d2video.exe` と同じフォルダに置く）
2. `r3d2video-windows.zip` を好きな場所に展開します。
3. `.r3d`（複数可・フォルダも可）を **r3d2video.exe** にドラッグし、用途と画面の並べ方を選びます。
   動画は録画ファイルと同じフォルダにできます。

## 用途（プリセット）

| 用途 | ファイル | 映像 | 音声 | サイズ（上下2画面） |
|---|---|---|---|---|
| **youtube** | `.mp4` | H.264（CRF 16） | AAC 192 kb/s・48 kHz | 1200 × 1440（3倍） |
| **resolve** | `.mov` | DNxHR HQ（DaVinci Resolve 無料版でも読める） | PCM・48 kHz | 800 × 960（2倍、1080p に収まる） |
| **lossless** | `.mkv` | FFV1 RGB（全ピクセルそのまま） | FLAC（そのまま） | 400 × 480（等倍） |

拡大は整数倍・ニアレストネイバーなので、ドットがぼけません。しかも色を間引く（4:2:0 / 4:2:2）
**前に**拡大するので、細い色の線や文字がにじみません（等倍の 4:2:0 MP4 は、3DS の 2 × 2 ピクセルごとに
色が1つになります）。YouTube は 1440p 以上の動画に高いビットレートを割り当てるので、その点でも有利です。

## 画面の並べ方

`both` 上下（録画のまま）・`top` 上だけ・`bottom` 下だけ（320 × 240）・`side` 横並び・
`split` 画面ごとに別ファイル・`auto` 録画に入っている画面のまま（既定）

## オプション

    --preset youtube|resolve|lossless
    --layout auto|both|top|bottom|side|split
    --scale N        拡大倍率（整数）を指定
    --fps N          出力のフレームレート（既定は録画のもの）
    --no-eq          本体スピーカー風の高音カットをせず、DSP の音のまま
    --out DIR        出力先フォルダ
    --ffmpeg PATH    使う ffmpeg を指定
