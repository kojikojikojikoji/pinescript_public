# **BB+Volume Strategy** (Pine Script v6)

このリポジトリでは、TradingViewのPine Script (v6) を用いて作成した「BB+Volume Strategy」を公開しています。本ストラテジーは、Bollinger Bandsを活用したロングエントリーと、ネガティブ・ボリューム比率による売り圧力検知を組み合わせて、短期売買の精度向上を狙うサンプル実装となっています。

## **概要**

1. **Bollinger Bands** (狭め設定: 0.8σ, デフォルト10～14期間)  
   - 価格が下限バンドを下抜け後に再度クロスアップしたタイミングでロングエントリー

2. **RSI フィルター** (デフォルト5期間 / 上限50～60あたり)  
   - 相場が「買われすぎ」状態でのエントリーを回避し、ダマシを減らす目的

3. **損切り & 利確**  
   - 損切り: デフォルト0.5%  
   - 利確: デフォルト1～3%  
   - バックテストや銘柄に合わせて調整してください

4. **ネガティブ・ボリューム比率**  
   - 過去数バー(volLookback, デフォルト14)で「陰線バーの出来高 / 総出来高」の割合が`volumeExitLimit`(例: 50%)を超えた場合、急激な売り圧力と判断してポジションをクローズ

## **特徴**

- **ta.sum() 非使用**  
  - `for`ループで手動合計する仕組みにより、古いバージョンや特殊環境でも動作可能  
- **ロングエントリー専用**  
  - シンプルに「押し目買い」を狙う実装  
- **短期ボリンジャー＆狭いσ**  
  - エントリー頻度を増やすため、標準的な 2σ ではなく 0.8σ などを採用  

## **使用方法**

1. **TradingView Pine Editorで新規スクリプトを作成**
   1. TradingViewのチャート画面を開く  
   2. 下部または右側のPine Editorを表示し、本リポジトリ内のスクリプトをコピー＆ペースト  

2. **チャートに適用**
   1. Pine Editor上でスクリプトを保存  
   2. 「Add to chart（チャートに追加）」ボタンを押すと、チャートにストラテジーが反映されます  
   3. 画面下部の「Strategy Tester」タブでバックテスト結果を確認できます

3. **パラメータを調整**
   - **BB 長期 (`bbLength`)**  
     ボリンジャーバンドの期間 (デフォルト14)  
   - **BB乗数 (`bbMult`)**  
     標準偏差の乗数 (デフォルト0.8)  
   - **RSI期間 (`rsiPeriod`)**, **RSI下限 (`rsiLimit`)**  
     エントリーのRSIフィルター (デフォルト5, 50)  
   - **損切り (`stopLossPerc`)**, **利確 (`takeProfitPerc`)**  
     ％指定で損切り/利確の閾値  
   - **出来高計算期間 (`volLookback`)**  
     過去何バーの出来高を合計するか (最大100推奨)  
   - **売り圧力閾値 (`volumeExitLimit`)**  
     過去 volLookback バーでの陰線バー出来高が全出来高の何％に達したら決済するか (デフォルト50%)

## **バックテスト・検証**

- **Strategy Tester** で勝率、プロフィットファクター、ドローダウンなどを確認し、パラメータを微調整してください。  
- 銘柄や時間足によって特性が大きく異なるため、複数の相場条件で試すことをおすすめします。

## **留意事項**

- 本ストラテジーは学習・検証用のサンプルです。実際のトレードでの使用にあたっては、必ずご自身でリスク管理やバックテストの徹底をお願いします。  
- 金融商品取引はリスクを伴い、場合によっては損失が発生する可能性があります。本ストラテジーにより生じたいかなる結果についても、作成者および本リポジトリは責任を負いません。  
- **投資判断は自己責任**で行ってください。

## **ライセンス**

- このコードはMITライセンス等で公開してもよいですし、利用者の方針に合わせて自由に拡張・変更してください。  

