# IRC_Monitor
IR Remote Controller signal monitor PIC16F18313

赤外線リモコンの信号をシリアルテキスト(9600bps)に変換します。

ChaNさまの[「赤外線リモコン制御モジュール」](http://elm-chan.org/fsw/irctrl/00index.html)を利用しています。 

NECフォーマット、家製協(AEHA)フォーマット、SONYフォーマット三種類の送受信に対応。

***
## 受信フォーマット
9600bps 8N
### NECフォーマット
32bitの固定長
- N 0x11 0x22 0x33 0x44 

### 家製協(AEHA)フォーマット
可変長(128bitまで受信可能)
- N 0x11 0x22 0x33 0x44 .. 0xNN

### SONYフォーマット
12bit、15bit、20bitの3種類の固定長

- S12 0x11 0x22
- S15 0x11 0x22
- S20 0x11 0x22 0x33
- SE 0x00 エラー

## 送信フォーマット
デバッグ中..

***
## 回路図
[![IRC_monitor by kane4d 4a457c9002343800 - Upverter](https://upverter.com/kane4d/4a457c9002343800/IRC_monitor/embed_img/15365775480000/)](https://upverter.com/kane4d/4a457c9002343800/IRC_monitor/#/)


## PCB例
Machikania Type M拡張基板の実装例
X
 - Vdd
 - Gnd

Y
    - RA4 - C14/RX
 - RA3 - C13/TX
 - RA2 - B2(Reserved)
 - RA1 - B3(Reserved)

![PCB](/images/pcb.PNG)
黄色はジャンパー接続をイメージしてます。

![Machikaniaに装着](/images/e_kiban.jpeg)
 
***
## ご注意
### ソースについて
PIC16F18313の2kWord内に収めるため、ソースコード可読性を犠牲にしてます。
#### XC8のバージョン
XC8 1.45とXC8 2.0のメモリー使用量を比較して2.0を選びました。
#### 3種類のシリアル出力でメモリー使用量
putch < puts < printf
#### 乗除算
シフト演算を利用しています。
#### 関数に展開
マクロと関数化どちらが小メモリーになる方を使用します。
