# Numerai Signalsについての概要

[Numerai Signals](https://signals.numer.ai/tournament) は、全世界の株式市場を対象としたコンペティションです。<br>
収益の源泉となる指標を用いたデータを作成し、他の人のデータと比較してオリジナリティがどれだけ高いか比較することができます。<br>
より独創的で、優位な予測データを提出すると、ステーク量に比例したNMRトークンを得ることができます。<br>
また、Numeraiのヘッジファンドではオリジナリティが最も高いデータを使用しています。<br>

Numerai Signals は、Numeraiヘッジファンドを構築するために使用され、Numeraiのマスタープランの一部です。<br>
[Medium Post](https://medium.com/numerai/building-the-last-hedge-fund-introducing-numerai-signals-12de26dfa69c) や、[short film](https://www.youtube.com/watch?v=GWeC2PK4yXQ&feature=youtu.be) で詳細が述べられています。



## 概要

1. [Numerai Signals](https://signals.numer.ai/tournament)にサインアップするか、既存のNumerai Tournament アカウントでサインインしてください。
2. 対象となっている株式市場に対応したデータをアップロードすると、過去のパフォーマンス、リスク、収益性の診断ができます。
3. 現行のコンペティションにNMRをステーキングすると、性能（Corr,MMC)に基づいてNMRを得られます。ただし、品質の低いデータではNMRを失うこともあります。
4. NumeraiのAPIに直接接続することで、毎週のデータ提出を自動化することができます。

## 株式市場のシグナルとは?

株式市場のシグナルとは、Numeraiのようなクオンツ・ファンドがポートフォリオを構築するために使用するデータのことです。

![An example stock market signal](../.gitbook/assets/image%20%284%29%20%282%29.png)

株式市場のシグナルの例としては、次のようなものがあります。

* [ファンダメンタルシグナル](https://www.investopedia.com/terms/f/fundamentalanalysis.asp) \([P/E ratio](https://www.investopedia.com/terms/p/price-earningsratio.asp), [dividend yield](https://www.investopedia.com/terms/d/dividendyield.asp), [analyst ratings](https://www.investopedia.com/terms/r/rating.asp#:~:text=A%20rating%20is%20conducted%20by,this%20action%20for%20the%20stock.)\)
* [テクニカルシグナル](https://www.investopedia.com/terms/t/technicalindicator.asp) \([MACD](https://www.investopedia.com/terms/m/macd.asp), [RSI](https://www.investopedia.com/terms/r/rsi.asp), [MFI](https://www.investopedia.com/terms/m/mfi.asp)\)
* [オルタナティヴデータシグナル](https://en.wikipedia.org/wiki/Alternative_data_%28finance%29) \([クレジットカード取引](https://secondmeasure.com/), [衛生画像](https://www.theatlantic.com/magazine/archive/2019/05/stock-value-satellite-images-investing/586009/), [ソーシャルメディアの感情](https://www.swaggystocks.com/dashboard/wallstreetbets/realtime)\)
* [ブレンドシグナル](https://www.investopedia.com/terms/m/multifactor-model.asp) \([Barra risk factors](https://www.investopedia.com/terms/b/barra-risk-factor-analysis.asp#:~:text=The%20Barra%20Risk%20Factor%20Analysis%20is%20a%20multi%2Dfactor%20model,turnover%20and%20senior%20debt%20rating.), [Fama French factors](https://www.investopedia.com/terms/f/famaandfrenchthreefactormodel.asp)\)

これらのシグナルを生成するために使用される基礎データは、異なったフォーマットである可能性が高いです。<br>
例えば、監査済みの財務報告書と駐車場の画像は全く異なるデータですが、株式市場を予測する何かしらのデータが含まれているかもしれません。<br>
Numeraiがデータを利用するためには規格化された形式であることが必要なため、ティッカーとシグナルデータが一対一で対応するようにリスト化する必要があります。<br>

## シグナルの作り方

### データとツール

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

Numerai には様々な既存のシグナルがあります。当社の既存のシグナルには、Barra ファクター（サイズ、バリュー、モメンタムなどのようなもの）、国やセクターのリスクファクター、custom stock features などが含まれています。

{% hint style="info" %}
定義: シグナルまたはターゲットは、Barra ファクター、国やセクターのファクター、その他のcustom stock features など、Numeraiの既存のシグナルとの相関関係が０になるように変換された後、"neutralized" されたとみなされます。
{% endhint %}

Numerai Signalsにアップロードされた全てのシグナルは、スコアリングされる前にneutralize されます。neutralization のポイントは、既知のシグナルに存在しないシグナルの独自成分あるいは直交成分を分離することです。

![A visualization of neutralization against a single known signal](../.gitbook/assets/image%20%289%29.png)

{% hint style="warning" %}
よく知られたいくつかのシグナルの単純な線形和を提出すると、neutralization 後に直交成分がほとんど残りません。
{% endhint %}

シグナルを評価するために使用されるターゲットもneutralize されます。ターゲットは、実質的にはNumerai のカスタムの「特定のリターン」または「残留リターン」です。

neutralization を実行するために使用されるデータは提供されないため、このプロセスは「ブラックボックス」であることを意味します。ただし、過去の期間に強いスコアを持つシグナルは、現在のラウンドでも将来のラウンドでも良いスコアが得られない可能性があることに注意することが重要ですが、シグナルのヒストリカル診断を使用して、neutralization が将来のシグナルに与える影響を推定することができます。

neutralization を実装するために使用されているコードはオープンソースです。neutralization のプロセスについては、このexample notebook で詳しく知ることができます。

{% embed url="https://github.com/numerai/example-scripts/blob/master/SignalsScoringExample.ipynb" %}

あるいは、feature exposure とneutralization のより広い意味合いを理解するために、このフォーラムの投稿をチェックしてみてください。

{% embed url="https://forum.numer.ai/t/model-diagnostics-feature-exposure/899" %}

後続の株式リターンとの相関性が非常に高いシグナルは、Numerai Signalsのスコアが非常に悪く、後続の株式リターンとの相関性が弱いシグナルは、高いスコアを出すことができるかもしれません。

言い換えれば、強い予測値を持つ「良い」シグナルは、単独で考えた場合、Numerai Signals のスコアは低いかもしれません。これは、シグナルの重要なユニークな側面を強調しています。Numerai Signals は、株式のリターンを予測することではなく、Numerai にはない独自のシグナルを見つけることです。

### Six Day Neutralized Return Targets

シグナルは、Numerai によって作成されたカスタムブラックボックスターゲットに対して評価されます。このターゲットは、6日間のニュートラル化された後続リターンに基づいています（最初の2日間は無視します）。

シグナルが6日の地平線（最初の2日を除く）で評価される理由は、短い時間軸でしか機能しないシグナルは、大規模なヘッジファンドが実装することが不可能だからです。例えば、シグナルが株式の1時間後のリターンを正確に予測できたとしても、ヘッジファンドがそのポジションを完全に取引するのに24時間かかるのであれば、あまり有用ではありません。大規模なヘッジファンドにとって最も有用なシグナルは、「低アルファ減衰」とも呼ばれる長い時間軸での予測力を持っています。

後続のニュートラル化されたリターンの6日間を構成する正確な市場日についての詳細は、dates and deadlines についての後のセクションを参照してください。

### Scoring

スコアリングの前に、シグナルは最初に\[0, 1\]の間でランク付けされ、次に中和されます。最後に、neutralize されたシグナルとターゲットの間のスピアマン相関を取ることでスコアが計算されます。このスコアは、このドキュメントとウェブサイトでは、単に`corr`と呼ばれています。

スコアリングの前にシグナルをneutralize することで、Numeraiはシグナルをターゲットに合わせ、ターゲットに対するパフォーマンスを向上させます。ターゲットもneutralize されるため、neutralization ステップでは、neutralization に使用されたデータをNumeraiが提供することなく、シグナルを効果的に最適化して最高のパフォーマンスを得ることができます。

例えば、シグナルがcountry risks に対してneutralize されていない場合、Numerai Signalsはスコアリングの前にcountry risks に対してシグナルをneutralize するので、country risks のneutralization を気にすることなく独自のシグナルの作成に集中することができます。

universe の一部の銘柄（例：米国株のシグナルのみ）についてのみシグナルを保有している場合でも、シグナルに参加することができ、高いパフォーマンスを発揮することができます。シグナルがない銘柄については、シグナルがランク付けされた後、Numerai が自動的に中央値で埋めてくれます。

### Meta Model Contribution

`corr`があなたのシグナルがNumeraiが知っているすべてのシグナルとneutralize されたターゲットとどれだけ相関しているかを示す指標であるとすれば、Meta Model Contribution \(MMC\)は、あなたのシグナルが、Numeraiが知っているすべてのシグナルとneutralize されたターゲット、およびNumerai Signals 上の他のすべてのstake されたシグナルとどれだけ相関しているかを示す指標である。このスコアは、このドキュメントやウェブサイトでは、単に`mmc`と呼ばれています。

シグナルの`mmc`は、最初にSignals' Meta Modelと呼ばれる特別なシグナルを構築することによって計算されます。ここで、Signals' Meta Modelとは、与えられたラウンドに対してNumerai Signals上のすべての（ランク付けされ、neutralize された）シグナルのstake 加重平均として定義されたものです。シグナルの`mmc`は、Signals' Meta Modelに中和された後のターゲットに対するシグナルの相関関係です。

{% hint style="success" %}
シグナルの高い一貫性のあるMMCは、あなたのシグナルがNumeraiの全てのデータとNumerai Signalsの他の全てのシグナルの組み合わせよりも優位に立っていることを意味するので、二重に印象的です。
{% endhint %}

MMCはメインのNumerai Tournamentから取った概念であり、スコアリングシステムは非常に似ています。Numerai でのMMCの計算方法の詳細については、Numerai Tournament のドキュメントの[metamodel contribution](https://docs.numer.ai/tournament/metamodel-contribution) のセクションを参照してください。

Numerai SignalsのMMCの計算は、Numerai Tournamentのそれとは完全に分離されていることに注意してください。具体的には、Numerai Signalsへのsubmission のみがSignalsのメタモデルを構築するために使用されます。

## Staking and Payouts

`payouts` を獲得する機会が欲しい場合は、投稿を`stake` することができます。`corr` または `corr_plus_mmc` にstake することができます。

{% hint style="info" %}
ステイクを行うには、[NMR cryptocurrency](https://www.coinbase.com/price/numeraire) をロックアップ\(しばらく引き出せないようにする\)する必要があります。これにより、シグナルのパフォーマンスが悪くなった場合、Numeraiはあなたのステークを燃やすことができます。
{% endhint %}

一度stake すれば、提出したスコアに応じて、何％かを`earn` したり、`burn` したりすることができます。

```python
corr_payout = stake * clip(2 * corr, -0.25, 0.25)

corr_plus_mmc_payout = stake * clip(2 * corr + mmc, -0.25, 0.25)
```

例えば、`corr`に`100NMR`をstake して、あなたのスコアが`+0.05`であった場合、あなたは`100NMRの2 * 5% = 10NMR`を得ることができます。もしあなたが`corr_plus_mmc`にstake して、あなたの`mmc`が`+0.03`であれば、あなたは`100NMRの(2 * 5% + 3%) = 13NMR`を得ることになります。

あなたが稼ぐか、または燃やすことができる最大値は、各ラウンドであなたの賭け金の25％です。ペイアウトは自動的にあなたのstake に戻されます。

{% hint style="danger" %}
シグナルを賭ける機会は、Numeraiによる投資契約、証券、金融資産のリターンに基づくスワップ、Numeraiのヘッジファンドへの参加、またはNumerai自身への参加、またはNumeraiが獲得するフィーの提供**ではない**ことに注意することが重要です。支払いは、ユーザーには開示されないブラックボックスのターゲットに基づいて、当社の裁量で行われます。 基本的に、Numerai Signalsは、「本物の」シグナルを検証する方法としてNMR staking を使用して、ユーザーが自分のシグナルの価値を評価することを可能にするNumeraiが提供するサービスです。その見返りとして、Numeraiはstake されたシグナルと関連データをNumeraiヘッジファンドで使用します。異なる期待を持っているユーザーは、シグナルをstake するべきではありません。

詳細については、[利用規約](https://numer.ai/terms)をお読みください。
{% endhint %}

stake を作成するには、ウェブサイトの"manage stake"ボタンをクリックして、stake を"increase"するための"change request"を作成します。ここでは、`corr`と`corr_plus_mmc`のどちらにstake するかを選択することができます。いつでもstake を減らしたい場合は、"change request"を作成してステークを"decrease"することもできます。  

![](../.gitbook/assets/image%20%2812%29.png)

change requests をしたからといって、すぐに適用されるわけではありませんのでご注意ください。変更を適用する前に、必ずウェブサイトに表示されている"effective date"を再確認してください。

## Dates and Deadlines

### Data Date vs Effective Date

ヌメライシグナルには2種類の日付があります。

* `data_date` - 基礎となる株式市場データに対応する日付です。すべての`data_date`は、その日の市場の終値を参照しており、時刻は含まれていません。例えば、submissionsの`friday_date`列の値は`data_date`型です。
* `effective_date`- Numerai Signals で行われるアクションやイベントに対応する日付で、常にUTCで指定された時間を含む場合があります。時間帯や株式市場データの処理に時間がかかるため、`data_date`と`effective_date`の間には通常遅延が発生します。特に指定がない限り、本ウェブサイトおよび本文書に記載されている日付はすべて effective\_date 型です。

### Rounds

Submissions、stakes、scores、payoutsは、それらについて話しやすいように番号の付いた`rounds` にグループ化されています。

新しい`round`は毎週`土曜日の18:00 UTC`で行われます。提出とstake の締め切りは`月曜日の14:30 UTC`です。遅れたsubmissions は採点されず、payoutsにはカウントされません。締め切り後に行われたstake の変更は次のroundに適用されます。

オンタイムのsubmissionsは採点され、保留中のpayoutsは金曜日、土曜日、火曜日、水曜日に計算されます。stake 値は"stake selection"の間、金曜日までにロックされます。これは、前のround からのpayouts が次のroundsのためのあなたのstake 値に複合することを意味します。水曜日のスコアとペイアウトは、そのラウンドの最終スコアとペイアウトとなります。

![](../.gitbook/assets/image%20%2814%29.png)

`round`のuniverse は、前の金曜日の`data_date`で定義されています。4 日間のスコアリングとペイアウトは、`3 日目-2 日目`、`4 日目-2 日目`、`5 日目-2 日目`、`6 日目-2 日目`の中立リターンに基づいています。ある日のマーケットクローズからスコアリングのためにデータが利用可能になるまでには2日のラグがあります。例えば、`6日目-2日目`のneutralized returnsは月曜日のマーケットクローズまでですが、利用可能になるのは水曜日です。

![](../.gitbook/assets/image%20%2815%29.png)

## Reputation and Leaderboard <a id="reputation-and-leaderboard"></a>

あなたのシグナルの`reputation`は、過去20回のラウンドにおけるあなたのシグナルの`corr`の加重平均です。同様に、あなたのシグナルの`mmc_reputation`は、過去20ラウンドのあなたのシグナルの`mmc`の加重平均です。

![](../.gitbook/assets/image%20%2813%29.png)

## Support

助けが必要ですか？

質問、サポート、フィードバックのために [RocketChat](https://community.numer.ai/home) で私たちを見つけてください!

