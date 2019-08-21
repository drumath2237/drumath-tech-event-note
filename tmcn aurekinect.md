# TMCN Azure Kinect DK Meetupp

## Kinect の概要

Azure kinect はv4、Hololensがv3らしい
AzureKinectにHololensの顧客が興味を見ち始めた。
AzureはCUDAが必須→Nvidea縛りが発生
IRカメラで血管が見れるらしい(?)
壁がちゃんとまっすぐ出る
v2はレーザーが強かったのでノイズが出る、v3はパターンで操作するので粗い
ボディトラックの精度が向上

- センサーSDK
  - C,C++API、Unityで動作
  - ドキュメントが整備された
  - Linuxの正式サポート
  - SDKはGithubで公開
- ボディトラッキングSDK
  - Win32API
  - Linuxサポート予定(現状はまだ)

### システム要件

body tracking sdk→GTX1070以上！？！？
温度制限が厳しい→15~20度←夏場の東京ではまず無理

魚眼→DoF120度

横を向くと、鼻と目で前後の区別ができている

v2は6人までだったが、一応無制限らしい

高齢者のベッド落下などの介護ニーズに対応
寝っ転がってもトラッキングできる

Depthセンサー

4パターン
binnedとunbinnedがある

Colorカメラ
4Kまでいける
縦長の3:2になる？

モーションセンサー(IMU)

ジャイロセンサー加速度センサー温度センサー

マイクアレイ
４つ→７つに

### 外部同期

複数台の連携

IMU→1台でSLAMするため？
据え置きスキャンと1台でSLAMに対応か？

同期処理


## Azure Kinect DK C++開発概要

SDK1.2のお話

センサーSDKとBodyTラッキングSDKの二つに分かれている
センサーはオープンソースになっている

C++APIとC#のラッパー

ビルド済みのSDKがある

BodyTrackingSDKはOSSじゃないのでインストーラから
ONNIX　Runtime　CUDA　backend

depthイメージ→PointCloudの変換も可能

ファイルからの再生はK4Aプレイバックでファイルをオープン

Body Tracking SDK はC++のラッパーもない

v4ではまだJointの信頼度が取得できない

真上からのトラッキングは公式ではサポートしていないが割ととれる
