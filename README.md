# WS2812B_PIC16F18313
NeoPixel WS2812BをPIC16F18313で制御するプログラムです  
開発環境はMPLAB X IDE v5.15およびXC8 v2.05です

# 対応マイコン
基本:PIC16F18313  
  
PIC16F18313およびPIC16F18326で実機確認済み  
PIC16F183xxシリーズでコンパイル通りますが実機での確認はしておりません  
(8ピンのマイコン向けに記述しているため、14ピン、20ピンのマイコンの場合はGPIOの設定(ポートB,C)を追加してください)  
HEXファイルはPIC16F18313のもののみ用意しております
  
なお、PIC16F18313に比べPIC16F18326はメモリが何倍も多いので、複雑な光らせ方をする場合はPIC16F18326を使用することをおすすめします

# 使い方
## 回路図
PIC16F18313(8ピン)の場合  
![8ピン回路図](https://github.com/yuzuhara0597/WS2812B_PIC16F18313/blob/master/PIC16F18313.png)  
  
  
PIC16F18326(14ピン)の場合  
![14ピン回路図](https://github.com/yuzuhara0597/WS2812B_PIC16F18313/blob/master/PIC16F18326.png)  

マイコンにはPICkit等を通してプログラムを書き込んでください。 CファイルとHEXファイルを用意しています  
## ※注意
NeoPixel点灯時はかなりの電流が流れます。点灯動作させる際はPICkitからの電流供給ではなく外部に電源をつないでください

# 関数について
## ws2812b_init関数
WS2812Bを点灯させるための初期設定の関数です。main関数内で最初に使います。  
なお、ピン設定もこの関数内で設定しているため、機能拡張の際は適宜書き換えてください  
```
void ws2812b_init(void)
```
## ws2812b_reset関数
WS2812Bを明るさ0で初期化する関数です。電源投入時に意図しないLEDが光るのを防ぐことができます  
```
void ws2812b_reset(unsigned int led_number)
```
この関数の引数に繋げてあるWS2812Bの個数を記述します  
例えば、100個のWS2812Bが繋がっている回路の場合は、
```
ws2812b_reset(100);
```
とします  
## ws2812b_flash関数
WS2812Bを指定の色、明るさで点灯させるための関数です  
```
void ws2812b_flash(unsigned char r,unsigned char g,unsigned char b)
```
この関数の引数r,g,bにそれぞれ赤、緑、青の明るさを0~255の範囲で代入します  
また、複数のWS2812Bを制御する場合はこの関数を続けて使用してください  
例えば、1つ目のWS2812Bを最大輝度で赤く、2つ目のWS2812Bを少し暗くした青で、3つ目のWS2812Bを最大輝度で白く光らせる場合、
```
ws2812b_flash(255,0,0);
ws2812b_flash(0,0,100);
ws2812b_flash(255,255,255);
ws2812b_end();  //この関数は後述
```
と記述します
## ws2812b_end関数
WS2812Bをws2812b_flash関数を使い指定個数制御した後に使用する関数です
```
ws2812b_end();
```
使い方はws2812b_flash関数での例を参考にしてください

## ws2812b_demo関数
デモ動作の関数です。7個のWS2812Bがゆっくり明るくなっていきます
```
ws2812b_demo();
```

# ライセンス
MITライセンスです
