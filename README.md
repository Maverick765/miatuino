# Miatuino ECU NA6 PNP
<img src="https://github.com/user-attachments/assets/3b163c0d-8062-4994-85b1-077876a0c4ef" width="400">

MiatuinoはSpeeduinoをベースとしたNA6ロードスター専用ECUプロジェクトです。

Speeduino MX-5 PNPモデルをベースとし、部品の入手性、組み立てやすさなどを改善しました。

基本的な技術情報については公式のWikiを参照してください。
https://wiki.speeduino.com

また、部品に関してはできる限り日本国内で入手しやすいものにしています。国内で入手できないものはAliexpressやLCSCで入手可能です。

---

## 対応車種

- 車種：ユーノス・ロードスター（NA6CE）
- 年式：1989年〜1995年
- エンジン：1.6L B6ZE(RS)

注意：NA8には対応していません。

---

## Speeduinoからの変更点

- Arduino Mega2560をMega2560 Proに変更
- SMD部品を減らし、手はんだで組み立てやすいように変更
- A/C制御回路の追加
- 電源回路をROHM製のDC-DCコンバータBP5293-50に変更
- MAPセンサをBOSCH製0 281 002 593に変更

---

## 注意事項

- 仕様はほぼSpeeduinoと同様です。詳細仕様は [Speeduino公式Wiki](https://wiki.speeduino.com/) を参照してください。
- 純正には**吸気温センサー（IAT）が存在しない**ため、追加設置が必須です。
- ノック制御、スピードセンサーなどには非対応です。

---

## ECUの組み立てと取付に必要なもの

- Miatuino基板  
リポジトリ内のGerberファイルを利用。
- 実装用部品  
リポジトリ内の部品表を参照。
- 吸気温センサー(IAT)  
品番：25036751  
エアフロメーターを外したカプラに接続します。  
Aliexpressなどで入手可能
- 吸気温センサー用カプラ  
Aliexpressで「7pin Automotive Connector」などと検索すれば見つかります。
- スロットルポジションセンサー(TPS)  
品番：0280122001  
カプラの形状と配線が純正と同じため、そのまま利用できます。  
Aliexpressなどで入手可能。
- スロットルポジションセンサー用マウントアダプター  
リポジトリ内の.stlファイルを利用。  
3Dプリンタで出力するか、3Dプリントサービスを利用してください。  
.stlファイルは以下のページからも入手可能です。  
[1.6 Miata Kia type tps adapter M5 nuts](https://www.thingiverse.com/thing:4611603)
- MAPセンサー  
0 281 002 593  
Aliexpressなどで入手可能。
- MAPセンサー用カプラー  
品番：1928403966  
Aliexpressなどで入手可能。
- 基板用ケース  
基板のサイズは100mm x 100mmです。適当なサイズのアルミケースに入れます。
- 基板用USB Type Cコネクタ  
ケース内のMega 2560 Proと接続するためのパネルマウントのType Cコネクタ。
- 内径4.5mmのホース   
3m程度。キジマのガソリンホースがおススメです。
- TunerStudio  
[公式ページ](https://www.efianalytics.com/TunerStudio/)から入手可能。
- SpeedyLoader  
[公式ページ](https://speeduino.com/home/support/downloads)から入手可能。


---


## 製作

基本的にはKiCADのプロジェクトや部品表を見ながらはんだ付けすればOKです。
MAPセンサーは基板の3ピンコネクタにカプラを介して取り付けます。

---


## ファームウェアの書き込み

SpeedyLoaderを利用してファームウェアを書き込みます。
[SpeedyLoaderの公式マニュアル](https://wiki.speeduino.com/en/Installing_Firmware)を参考にしてください。

また、書き込みが完了したらbase tuneをダウンロードしておきます。

---


## 取付手順

### スロットルポジションセンサーを交換する

純正のスロットルポジションセンサーを外し、新しいスロットルポジションセンサーをアダプターを利用して取り付けます。

なお、純正のセンサーを取り外すには、スロットルボディーを外す必要があります。
(純正のセンサーを破壊すればスロットルボディーを外さずに新しいセンサーを取り付けることも可能ですがおススメしません)

### エアフロメーターのカプラを外して吸気温センサーを取り付ける

エアフロメータにつながっている7ピンのカプラを外し、吸気温センサを取り付けます。

### ST-SIGのヒューズを外す

エンジンルーム内の運転席側のヒューズボックスを開け、ST-SIGのヒューズを外します。
なお、Miatuinoを利用する場合、このヒューズは常に外したままにしておく必要があります。

_ST-SIGのヒューズは、セルモーターを回している間、一時的に燃料ポンプを動かすための電源が来ているヒューズです。_
_純正状態のNA6では、燃料ポンプの電源ON/OFFをフラップ式のエアフロメータの中にある機械式の接点で行っています。つまり、エンジンが回って負圧が発生している状態でないと燃料ポンプは作動しません。_
_エンジン始動時は負圧が弱く、この接点が動かないため、一時的に燃料ポンプに電源を供給する必要があります。その電源が来ているのがST-SIGのヒューズです。_
_Miatuinoでは、エアフロメータの配線を流用して燃料ポンプの制御を行うことになりますが、この時、ST-SIGのヒューズを残したままにしていると、キーを回したときに基板のドライバICに電流が逆流し、基板が焼けます。_


### 純正ECUを取り外す

助手席側スカッフプレート、一部のトリムを外してカーペットをめくります。
スチールのカバーパネルを外すと、ステーで固定されたECUが見えるので取り外し、カプラーを外します。


### MAPセンサーへつなぐホースを通す

MiatuinoではDジェトロニック方式になるため、インテークマニホールドの負圧をホースでECUまで接続する必要があります。
純正のインテークマニホールドには、ゴムキャップが付いた使われていない負圧取り出しニップルがあるので、それを利用します。
また、ロードスターのエンジンルーム隔壁にはゴム栓でメクラされた穴があるので、その栓を外してホースを通します。

カーペットをめくっている間に、エンジンルーム側からホースを送り、室内側の足元まで届かせます。
室内と反対側のホースの先をインマニにあるニップルに取り付けます。


### Miatuinoを取り付ける

純正ECUを取り外したカプラと、先ほど通したホースをMiatuinoに繋ぎます。
ECUのセッティングやトラブルシューティングのためにも、ECUは元の場所に戻さず、助手席足元に転がすなりしておきます。
ECU底面に面ファスナーのテープを取り付け、内装に張り付けておくのもおすすめです。

---

## セットアップ手順

PCとMiatuinoをUSBケーブルで接続し、PCでTuner Studioを起動し、初期データの書き込みと各種センサーのキャリブレーションを行います。

#### 初期データの書き込み

SpeedyLoaderからダウンロードしたbase tuneを書き込みます。

[File] -> [Load Tune(MSQ)]を選択して、SpeedyLoaderでからダウンロードしたbase tuneを書き込みます。

#### TPSのキャリブレーション

[Tools] -> [Calibrate TPS]を選択します。

正しくTPSが接続されていれば、アクセルペダルを踏めば値が変化することを確認できます。

まずはアクセルを完全に戻した状態で[Closed throttle ADC Count]の右の[Get Current]をクリックして、スロットル全閉時の値を取得します。
次に、アクセルを完全に踏み込んだ状態で[Full throttle ADC Count]の右の[Get Current]をクリックして、スロットル前回時の値を取得します。
完了したら[Accept]をクリックします。

この際、センサーの極性(全開で0Vか、全閉で0Vか)で警告が出ることがありますが、そのまま進めればSpeeduino側で勝手に極性を変更してくれます。

#### 水温センサーのキャリブレーション

[Tools] -> [Calibrate Tempereture Sensor]を選択します。

[SensorTable]のプルダウンから[Coolant Tempereture Sensor]を選択します。

[Table Input Solution]が3 Point Therm Generatorになっていることを確認します。

[Common Sensor Values]のプルダウンから[RX7_CLT(S4&S5)]を選択します。

[Write to Controller]をクリックして完了したら[Close]をクリックします。


#### 吸気温センサーのキャリブレーション

[Tools] -> [Calibrate Tempereture Sensor]を選択します。

[SensorTable]のプルダウンから[Air Tempereture Sensor]を選択します。

[Table Input Solution]が3 Point Therm Generatorになっていることを確認します。

[Common Sensor Values]のプルダウンから[RX7_AFM(S5 in AFM)]を選択します。

[Write to Controller]をクリックして完了したら[Close]をクリックします。


#### O2センサーの設定

[Tuning] -> [AFR/O2]を選択します。

純正のO2センサーを利用する場合、[Sensor Type]に[Narrow Band]を指定します。

完了したら[Burn]をクリックして[Close]をクリックします。

純正のO2センサーを利用する場合はこれで完了ですが、社外のワイドバンドセンサーを付けている場合はキャリブレーションを行う必要があります。

[Tools] -> [Calibrate AFR Sensor]を選択します。

[EGO Sensor]のプルダウンメニューから、利用しているセンサーのメーカーを選択します。

[Write to Controller]をクリックして完了したら[Close]をクリックします。

---

## 関連リンク

- [Speeduino 公式サイト（英語）](https://speeduino.com/)
- [Speeduino Wiki（英語）](https://wiki.speeduino.com/en/boards/MX5_PNP)
- [TunerStudio ダウンロードページ](https://www.efianalytics.com/TunerStudio/)
- [Speedy Loader ダウンロードページ](https://speeduino.com/home/support/downloads)
- [1.6 Miata Kia type tps adapter M5 nuts](https://www.thingiverse.com/thing:4611603)
