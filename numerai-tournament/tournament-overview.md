---
description: 公式ルールと始め方ガイド
---

# トーナメント概要

#### 前書き
Numeraiトーナメントでは、難読化されたデータを使用して機械学習モデルを構築することで株式市場の動向を予測します。<br>
提出した予測ファイルにNMRと呼ばれる暗号通貨を賭けると、パフォーマンスに基づいてNMRを獲得できます。
Numeraiに提出された予測ファイルは、Numeraiが保有するヘッジファンドのモデル（メタモデル）を設計するために使用されます。下に示すyoutubeを見ることで、どのようにデータが使用されるか学べます。

[![](https://img.youtube.com/vi/dhJnt0N497c/0.jpg)](https://www.youtube.com/watch?v=dhJnt0N497c)

#### 概要
1.Numeraiに[登録](https://numer.ai/)する。
2.トレーニングデータとサンプルスクリプトを含むデータセットをダウンロードする。
3.モデルを作成し、予測をNumeraiに送信する。
4.モデルにNMRを賭けて、パフォーマンスに基づいてNMRを貰う/払う
6.毎週の提出物を自動化する。

## データ
Numeraiトーナメントの中核は無料のデータセットが使用できることです。データセットはクリーンアップ・正規化・難読化された高品質の財務データで構成されています。
![numerai\_training\_data.csv](../.gitbook/assets/image%20%287%29.png)

提供されている`training_data`では、各`id`は難読化された`features`のセットを持つ株式に対応しています。`target`は将来のパフォーマンスを表します。行は、異なる時点を表す`eras`にグループ化されています。
詳細は[本記事](https://qiita.com/tit_BTCQASH/items/366a2d1c273507dd4b8c)に詳しく記述されています。

## モデリング
Numeraiトーナメントでは、過去のデータを用いて予測モデルを作成し、そのモデルを用いて将来の株式市場を予測することが目的です。
PythonでXGBoostを使用した基本的な例を次に示します。過去のトレーニングデータを使用してモデルをトレーニングし、ライブトーナメントデータで予測を行います。（＊本プログラムのみでは予測ファイルの提出ができません。より実践的な例は[本記事](https://qiita.com/tit_BTCQASH/items/366a2d1c273507dd4b8c)をチェックしてください。

```python
import pandas as pd
from xgboost import XGBRegressor

# training data contains features and targets
training_data = pd.read_csv("numerai_training_data.csv").set_index("id")

# tournament data contains features only
tournament_data = pd.read_csv("numerai_tournament_data.csv").set_index("id")
feature_names = [f for f in training_data.columns if "feature" in f]

# train a model to make predictions on tournament data
model = XGBRegressor(max_depth=5, learning_rate=0.01, \
                     n_estimators=2000, colsample_bytree=0.1)
model.fit(training_data[feature_names], training_data["target"])

# submit predictions to numer.ai
predictions = model.predict(tournament_data[feature_names])
predictions.to_csv("predictions.csv")
```

## 予測ファイルの提出

毎週土曜日の`18:00 UTC`\(日本時間では日曜日`03:00 JST`\) に新しい`round`が始まり、新しい`tournament_data`が公開されます。あなたの予想をNumeraiに提出して、トーナメントに参加しましょう。

締め切りは月曜日`14:30 UTC` \(日本時間では月曜日`23:30 JST`\) です。提出が遅れた場合、ペイアウトの対象外となります。

{% hint style="info" %}
[tool や library](https://docs.numer.ai/tournament/tools) を使用して、GraphQL [API](https://api-tournament.numer.ai/)に接続しましょう。
{% endhint %}

![prediction.csv](../.gitbook/assets/image.png)

## Scoring

あなたが提出した予測結果は、あなたの予測と真のターゲットの `correlation` \(ここではspearmanの順位相関\)でスコアリングされます。相関性が高いほど良いです。

{% tabs %}
{% tab title="scoring\_function.py" %}
```python
# method='first' breaks ties based on order in array
ranked_predictions = predictions.rank(pct=True, method="first")
correlation = np.corrcoef(labels, ranked_predictions)[0, 1]
```
{% endtab %}
{% endtabs %}

あなたの予測結果は、あなたのメタモデルへの貢献度、つまり`mmc`でも採点されます。

詳しくは、[metamodel contribution](https://jp.docs.numer.ai/numerai-tournament/meta-model-contribution-mmc) のセクションを参照してください

## Staking and Payouts

あなたの予測結果に `stake` することで `payouts` を得ることができます。`corr` のみ、または `corr + mmc` にstake することができます。

stake せずにNumeraiに参加することで、トーナメントの詳細や自分のモデルの性能を知ることができます。自分のモデルに自信が持てるようになったら、そのモデルにstake することができます。stake の最小値は0.01NMRです。

{% hint style="info" %}
ステイキングを行うには、[Erasure](https://erasure.world/) smart contract agreement で [NMR](https://coinmarketcap.com/currencies/numeraire/) をロックする必要があります。これにより、モデルのパフォーマンスが低下した場合、Numerai はあなたのstake を燃やすことができます。
{% endhint %}

あなたがstake しているスコアに基づいて、あなたのstake のパーセンテージを `earn` \(獲得\)したり、 `burn` \(燃やし\)たりします。例えば、`correlation` に `100NMR` をstake して、スコアが+0.05だった場合、100NMRの5%=5NMRを獲得できます。稼ぐか燃やすかの上限は、1ラウンドごとにstake の `25％` となります。

```python
corr_payout = stake * clip(corr, -0.25, 0.25)

mmc_payout = stake * clip(corr + mmc, -0.25, 0.25)
```

詳しくは [Staking and Payouts](https://jp.docs.numer.ai/numerai-tournament/staking-and-payouts) のセクションを見てください。

## Daily Updates

提出した予測結果はそれぞれ、投稿締め切り後の最初の木曜日から4週間後の水曜日まで、毎日更新されたスコアを受け取ることができます。例えば、`7日（日）`に青の投稿をした場合、最初のスコアは`11日（木）`、最終スコアは翌月の`7日（水）`に届きます。

提出した予測結果にstake した場合、ペイアウトも毎日更新されます。しかし、最終的なスコアと最終的なペイアウトだけがカウントされます。

![submission and scoring calender](../.gitbook/assets/image%20%282%29.png)

## Reputation and Leaderboard

リーダーボードでのあなたの `rank` は、過去20ラウンドの `correlation` スコアの加重平均である `reputation` に基づいています。

詳しくは、 [Reputation](https://jp.docs.numer.ai/numerai-tournament/reputation) のセクションを参照してください。

![](../.gitbook/assets/image%20%285%29.png)

## Support

助けが必要ですか？

質問、サポート、フィードバックのために [RocketChat](https://community.numer.ai/home) で私たちを見つけてください!

