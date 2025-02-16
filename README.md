# 1. 環境構築

## 1.1 Raspberry Pi pico の KiCAD 用ライブラリのインストール

### 1.1.1 シンボルライブラリのインストール

ディレクトリにある`KiCAD\ Raspberry\ Pi\ Pico.zip`を解凍し, `RPi_Pico.lib`を以下の手順で KiCAD に追加します.

1. 回路図エディタを開きます.
2. 設定 -> シンボル ライブラリを管理 を選択します.
3. 左下のフォルダマークから`RPi_Pico.lib`を追加します.
4. 追加したら, OK を押して閉じます.
5. 確認としてシンボルを追加ボタンを押して, `Pico`と検索してみてください.

### 1.1.2 フットプリントライブラリ

`KiCAD\ Raspberry\ Pi\ Pico.zip`を解凍し, `RPi_Pico.pretty`を`C:\Program Files\KiCad\8.0\share\kicad\footprints`にコピーします.
