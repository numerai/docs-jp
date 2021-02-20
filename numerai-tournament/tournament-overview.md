---
description: 公式ルールと始め方ガイド
---

# Tournament Overview

## Data

Numeraiの中核をなすのは、データサイエンスの問題、つまり株式市場の予測の問題です。

提供されている`training_data`では、各`id`は難読化された`features`のセットを持つ株式に対応しています。`target`は将来のパフォーマンスを表します。行は、異なる時点を表す`eras`にグループ化されています。

あなたの目標は、新しい特徴を与えられたターゲットを予測するための機械学習モデルを学習させることです。

{% hint style="info" %}
[analysis and tips notebooks](https://github.com/numerai/example-scripts/blob/master/analysis_and_tips.ipynb) を読んで、データセットを深く掘り下げてみましょう。
{% endhint %}

![numerai\_training\_data.csv](../.gitbook/assets/image%20%287%29.png)

## Modeling

以下に、`training_data`上でモデルを訓練して、`tournament_data`上で予測を行う方法の例を示します。

{% hint style="info" %}
より高度な例については [example-scripts](https://github.com/numerai/example-scripts) のレポジトリをチェックしてください。
{% endhint %}

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

## Submissions

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

