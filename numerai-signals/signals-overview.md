# Numerai Signals Overview

[Numerai Signals](https://signals.numer.ai/tournament) では、株式市場のシグナルをアップロードして、Numerai の他のシグナルと比較してどれだけオリジナルであるかを確認することができます。シグナルは、暗号通貨NMRを使ってstake し、報酬を得ることができます。最もオリジナリティの高いシグナルは、Numeraiのヘッジファンドで使用されています。

Numerai Signals は、世界最後のヘッジファンドを構築するためのNumerai マスタープランの一部です。[Medium Post](https://medium.com/numerai/building-the-last-hedge-fund-introducing-numerai-signals-12de26dfa69c) を読んで、[short film](https://www.youtube.com/watch?v=GWeC2PK4yXQ&feature=youtu.be) を見て、それがどのようにしてすべてを統合しているのかを詳しく知りましょう。



## Summary

1. [Numerai Signals](https://signals.numer.ai/tournament)にサインアップするか、既存のNumerai Tournament アカウントでサインインしてください。
2. Numerai のstock universe のシグナルをアップロードして、シグナルの過去の部分のパフォーマンス、リスク、収益性の診断を受け取ることができます。
3. シグナルのライブ部分にNMRをstake して、Numeraiのカスタムターゲットとの相対的なパフォーマンスに基づいてNMRを獲得したり、失うことができます。
4. 当社のAPIに直接接続することで、毎週のシグナルのアップロードを自動化し、時間の経過とともにstake の価値を高めます。

## What are stock market signals?

株式市場のシグナルは、Numeraiのような定量的なヘッジファンドがポートフォリオを構築するために使用する、株式に関する数値データの供給です。

![An example stock market signal](../.gitbook/assets/image%20%284%29.png)

株式市場のシグナルの例としては、次のようなものがあります。

* [ファンダメンタルシグナル](https://www.investopedia.com/terms/f/fundamentalanalysis.asp) \([P/E ratio](https://www.investopedia.com/terms/p/price-earningsratio.asp), [dividend yield](https://www.investopedia.com/terms/d/dividendyield.asp), [analyst ratings](https://www.investopedia.com/terms/r/rating.asp#:~:text=A%20rating%20is%20conducted%20by,this%20action%20for%20the%20stock.)\)
* [テクニカルシグナル](https://www.investopedia.com/terms/t/technicalindicator.asp) \([MACD](https://www.investopedia.com/terms/m/macd.asp), [RSI](https://www.investopedia.com/terms/r/rsi.asp), [MFI](https://www.investopedia.com/terms/m/mfi.asp)\)
* [オルタナティヴデータシグナル](https://en.wikipedia.org/wiki/Alternative_data_%28finance%29) \([クレジットカード取引](https://secondmeasure.com/), [衛生画像](https://www.theatlantic.com/magazine/archive/2019/05/stock-value-satellite-images-investing/586009/), [ソーシャルメディアの感情](https://www.swaggystocks.com/dashboard/wallstreetbets/realtime)\)
* [ブレンドシグナル](https://www.investopedia.com/terms/m/multifactor-model.asp) \([Barra risk factors](https://www.investopedia.com/terms/b/barra-risk-factor-analysis.asp#:~:text=The%20Barra%20Risk%20Factor%20Analysis%20is%20a%20multi%2Dfactor%20model,turnover%20and%20senior%20debt%20rating.), [Fama French factors](https://www.investopedia.com/terms/f/famaandfrenchthreefactormodel.asp)\)

これらのシグナルを生成するために使用される、基礎となるデータは、非常に異なる場合がありますが（監査済みの財務報告書と駐車場の画像）、シグナル自体はすべて同じ基本的な形式で提供されます - それぞれに関連する数値を持つ株式相場表示\(stock ticker\)のリストです。

## Signal Creation

### Data and Tools

独自のシグナルを作成するためには、まず、いくつかの株式市場のデータを取得する必要があります。

{% hint style="info" %}
株式市場のデータがないデータサイエンティストですか？代わりに[Numerai Tournament](https://numer.ai/)に参加してください。 
{% endhint %}

まだ株式市場のデータにアクセスできていない場合は、 [Yahoo Finance](https://finance.yahoo.com/)、[Quandl](https://www.quandl.com/)、 [Koyfin](https://www.koyfin.com/) など、インターネット上に無料または格安のデータプロバイダーが多数存在します。 

また、 [Quantopian](https://www.quantopian.com/)、[QuantConnect](https://www.quantconnect.com/)、[Alpaca](https://alpaca.markets/) などのシグナルを簡単に作成できるプラットフォームもあります。特に、[Risk Model](https://www.quantopian.com/risk-model) と[AlphaLens Tearsheets](https://www.quantopian.com/tutorials/alphalens#lesson1) は、シグナルの品質を分析するのに最適な方法です。 私たちのコミュニティで使用されている人気のあるデータソース、プラットフォーム、ツールのリストについては、この[forum thread](https://forum.numer.ai/t/free-or-cheap-data-for-erasure-numerai-quant/350) をチェックしてください。

{% hint style="success" %}
ユニークで差別化されたデータセットを見つけることが、オリジナルのシグナルを生み出す鍵となります。
{% endhint %}

### Universe

ヌメライシグナルの株式市場ユニバースは、世界の上位5000の大型株をカバーしています。 

universe は毎週更新されていますが、一般的には、ある週に動き出すのは数銘柄の出来高の少ない銘柄のみです。 

[latest universe file](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/universe/latest.csv) をダウンロードすると、最新のuniverse を見ることができます。

universe の履歴は、 [historical targets file](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/signals_train_val_bbg.csv) をダウンロードしてご覧いただけます。

### Submissions

シグナルをNumerai Signals に提出する際には、少なくとも2つの列を含める必要があります。

* `cusip`、`sedol`、または`bloomberg_ticker` 列 - 値はヘッダーのticker タイプに関連付けられた有効なティッカーでなければなりません。
* `signal` 列- 値は0から1の間でなければなりません（排他的）。

2列のみの予測結果は、現在の`live`時間帯に対応していると仮定していますが、これはティッカーの値が一意でなければならないことを意味します。

また、過去の検証期間にわたってシグナルをアップロードして、パフォーマンス、リスク、潜在的な収益に関する診断指標を受け取ることもできます。検証期間は`20130104`から`20200228`までの374週間です。

検証期間を含む予測結果には、2つの余分な列を含める必要があります。

* `friday_date` 列 -  Numerai Signals では、週の期間が金曜日に始まるので、値は金曜日でなければなりません。
* `data_type`  列 - 値は`live`または`validation`のみを取り得ます。`data_type`が`live`の行には、直近の金曜日の日付が含まれていなければなりません。

![](../.gitbook/assets/image%20%288%29.png)

最新の予測結果の例は[こちら](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/example_signal/latest.csv)からダウンロードできます。

### Diagnostics

予測結果が受理されると、診断のために時間がかかります。これは通常、提出物に含まれている週数やティッカー数に応じて10～15分程度かかります。

![An example diagnostics report](../.gitbook/assets/image%20%2810%29.png)

これらの診断は、あなたのシグナルがstake する価値があるほど良いものかどうかを評価するための指針となります。過去の検証期間中に強い診断結果が出たシグナルは、現在または将来のライブ期間では良いスコアが得られない可能性があることに注意することが重要です。

{% hint style="danger" %}
このヒストリカル評価ツールを繰り返し使用すると、すぐにオーバーフィッティングにつながります。診断は、シグナル作成プロセスの最終チェックとしてのみ扱うようにしてください。
{% endhint %}

診断の計算に使用した過去のターゲットはすべて[ここ](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/signals_train_val_bbg.csv)にあります。

### API and Automation

{% hint style="info" %}
最新のシグナルを毎週Numeraiに提出する必要があります。
{% endhint %}

[GraphQL API ](https://api-tournament.numer.ai/)に直接接続するか、公式 python クライアントを使用することで、投稿ワークフローを自動化することができます。

{% embed url="https://github.com/uuazed/numerapi\#usage-example---numerai-signals" %}

## Signal Evaluation

### Neutralization

Numerai には様々な既存のシグナルがあります。当社の既存のシグナルには、Barra ファクター（サイズ、バリュー、モメンタムなどのようなもの）、国やセクターのリスクファクター、株式でよく使われている特徴量\(custom stock features\) などが含まれています。

{% hint style="info" %}
定義: シグナルまたはターゲットは、Barra ファクター、国やセクターのファクター、その他のcustom stock features など、Numeraiの既存のシグナルとの相関関係が０になるように変換された後、"neutralized" されたとみなされます。
{% endhint %}

Numerai Signalsにアップロードされた全ての信号は、スコアリングされる前にneutralize されます。neutralization のポイントは、既知の信号に存在しない信号の独自成分あるいは直交成分を分離することです。

![A visualization of neutralization against a single known signal](../.gitbook/assets/image%20%289%29.png)

{% hint style="warning" %}
よく知られたいくつかの信号の単純な線形の組み合わせを提出すると、中和後に直交成分がほとんど残りません。
{% endhint %}

信号を評価するために使用されるターゲットも中和されます。ターゲットは、実質的にはNumeraiのカスタムの「特定のリターン」または「残留リターン」です。

中和を実行するために使用されるデータは提供されないため、このプロセスは「ブラックボックス」であることを意味します。ただし、過去の期間に強いスコアを持つシグナルは、現在のラウンドでも将来のラウンドでも良いスコアが得られない可能性があることに注意することが重要ですが、シグナルのヒストリカル診断を使用して、neutralization が将来のシグナルに与える影響を推定することができます。

The code that is used to implement neutralization is open source. You can learn more about the neutralization process in this example notebook:

{% embed url="https://github.com/numerai/example-scripts/blob/master/SignalsScoringExample.ipynb" %}

Or check out this forum post to understand broader implications of feature exposure and neutralization.  







###   <a id="spotify-music"></a>







