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

## 2. 部品の選定

| 部品名称       | 選定部品          | 概要                                                         |
| -------------- | ----------------- | ------------------------------------------------------------ |
| マイコン       | Raspberry Pi Pico | RP2040 マイコン。左島、右島、中央島にそれぞれ搭載            |
| キースイッチ   | Cherry MX         | メカニカルスイッチ（リニア、タクタイル、クリッキーから選択） |
| ダイオード     | 1N4148W           | キーマトリクスに使用（キーゴースト防止）                     |
| TRRS ジャック  | MJ-4PP-9          | 左右の島を接続するために使用                                 |
| TRRS ケーブル  | TRRS 4 極 3.5mm   | 左右の島を接続するためのケーブル                             |
| LED            | SK6812MINI-E      | CapsLock などの状態を表示するために使用                      |
| スタビライザー | PCB マウント      | 2u 以上のキーの安定化に使用                                  |

# 3. 回路図の作成

## 3.1 キーサイズと top legend の対応

| キーサイズ | 標準的な番号の範囲 | 番号のスキップルール                       |
| ---------- | ------------------ | ------------------------------------------ |
| **1u**     | 1~100              | 通常通り 1 つずつ増加                      |
| **1.25u**  | 101~120            | 1 つスキップ（1.25u = 1.25 倍のスペース）  |
| **1.5u**   | 121~140            | 2 つスキップ（1.5u = 1.5 倍のスペース）    |
| **1.75u**  | 141~160            | 3 つスキップ（1.75u = 1.75 倍のスペース）  |
| **2u**     | 161~180            | 4 つスキップ（2u = 2 倍のスペース）        |
| **2.25u**  | 181~200            | 5 つスキップ（2.25u = 2.25 倍のスペース）  |
| **6.25u**  | 201~250            | 16 つスキップ（6.25u = 6.25 倍のスペース） |

## 3.2 キーマトリクスと master-slave 接続

master は左右のマイコンを slave として通信するので, UART1 が左のマイコンに接続され, UART0 が右のマイコンに接続されます.

### 3.2.1 master

### 3.2.1 master GPIO 配置

| 機能     | GPIO ピン |
| -------- | --------- |
| UART1_TX | GPIO4     |
| UART1_RX | GPIO5     |
| row0     | GPIO6     |
| row1     | GPIO7     |
| row2     | GPIO8     |
| row3     | GPIO9     |
| row4     | GPIO10    |
| row5     | GPIO11    |
| row6     | GPIO12    |
| col0     | GPIO13    |
| col1     | GPIO14    |
| col2     | GPIO15    |
| col3     | GPIO18    |
| UART0_TX | GPIO16    |
| UART0_RX | GPIO17    |

## 4. 疑問点

- 真ん中の島の 5 つの LED をボタンを押されたときに独立して光らせる
- 左右の電源はどうやって供給するのか
  - 左右は独立した電源供給にする
  - 電池
