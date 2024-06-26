# LineTraceCar_ver1_2023

ライントレースカーキットを作るにあたっての性能、設計、製作方法等をここに示す。

## Technical data

### CPU
AVRマイコン / ATMEGA328

### バッテリー
CPU,モータ共用
Lipo / 2セル / 7.4[v] / 240[mAh] / 

### モータ
- 走行用モータ DCモータ : 2[個] / マブチ RE-260RA
- モータドライバ : TB6643KQ

### センサ
- 赤外線センサ : 6[個] / / (ラインセンサ)
- 赤外線センサ : 2[個] / / (サイドセンサ))

### サイズ
- xx[mm]
- [g]

### 動輪
対向2輪 / ミニ四駆用タイヤ
(スキッドステアに変更も可)

### 速度(設計上最大)
- 速度 : 3[m/s]
- 加速度 : 2[m/s/s]


## 設計

### 機体サイズ・質量
- トレッド : 110[mm]
  - カーブ走っている際に、モータが逆回転しない幅にする必要がある.
- センサーバ : 適当
  - 長ければ安定して早く走れる.
- 質量 : 100[g] (目安)
  - 軽ければ軽いほどいいらしい

### タイヤ径・幅
- タイヤ径 : 24[mm] (ミニ四駆の小径ホイールを使用)
  - タイヤ径が大きいとトルクが大きい、小さいと回転数が大きい.
- タイヤ幅 : [mm] (ミニ四駆のタイヤ)
  - タイヤ幅が広いと直進安定性、加速性が高い、狭いとカーブに弱い.

### ギア比
- ギア比 : モータ:タイヤ = 1:3
  - トルクを増すためにギアを挟む.端数は互いに素であるようにする.

### 最高速度・最高加速度
走らせたい速度と加速度を決める(適当).
- 速度 : 3[m/s]
- 加速度 : 2[m/s/s]

### モータの選定
質量、タイヤ径、ギア比、速度・加速度からモータを選定します。
- 使用するモータ : [RE-260RA(マブチ)](https://www.mabuchi-motor.co.jp/motorize/branch/motor/pdf/re_260ra.pdf)  
- トルクの計算  
  運動方程式 : $ma = F$  
  タイヤのトルク : $T_t = Fr$ ( $r$ :タイヤの半径)  
  上式よりタイヤのトルクが導出できる.  
  $ma = T_t/r$  
  $T_t = mar$  
  このタイヤのトルクにギア比をかければモータのトルクが導出できる.  
  そうすると今回ほしいトルクが求められる.  
  $T = {1 \over 3} \cdot T_t = {1 \over 3} \cdot mar = {1 \over 3} \cdot 100 \times 10^-3 [kg] \cdot 2 [m/s/s] \cdot {24 \times 10^-3 [m] \over 2} = 0.0008 [Nm] = 0.8[mNm]$
- 回転数の計算  
  タイヤの回転数 : $rpm_r$ (rpm:"rotations per minute")  
  とすると、速度から  
  $v = 2 \pi r {rpm_r \over 60}$  
  $rpm_r = {v \over 2 \pi r} \cdot 60$  
  このタイヤの回転数にギア比をかければ、モータの回転数が導出できる.  
  そうすると今回ほしい回転数が求められる.  
  $rpm = 3 \cdot rpm_r = 3 \cdot {v \over 2 \pi r} \cdot 60 = 3 \cdot {2 \cdot 3 [m/s] \over 2 \pi 24 \times 10^-3 [m]} \cdot 60 \approx 7162[rpm]$  

このトルクと回転数を超えるモータを選べばOK

## 電子パーツ　

### CPU
- AVRマイコン / ATMEGA328  
  秋月電子で販売されている[AE-ATMEA328-MINI(Arduio Pro Mini上位互換)](https://akizukidenshi.com/catalog/g/gK-10347/)を使用.

### 電源
- DC\DCコンバータ 5[v] 1.5[A] [NJM7805FA](https://akizukidenshi.com/catalog/g/gI-08678/)

### モータドライバ
- TOSHIBA [TB6643KQ](https://akizukidenshi.com/catalog/g/gI-07688/)

### ラインセンサ
- 赤外線LED [OSI3CA5111A](https://akizukidenshi.com/catalog/g/gI-04779/)
- 照度センサ(フォトトランジスタ) [NJK7302L-F3](https://akizukidenshi.com/catalog/g/gI-08910/)

## ライセンス
- このソフトウェアパッケージは，3条項BSDライセンスの下，再頒布および使用が許可されます．
- © 2022 Yamaguchi Yuto
