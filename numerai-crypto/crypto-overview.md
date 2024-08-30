
# 概要

Numerai Cryptoに関する概要を紹介します。

## はじめに

Numerai Signalsと同様に、Numerai Cryptoも独自のデータを持ち込むことを求めます。暗号市場のシグナル（「CryptoSignal」）とは、情報のフィードです。これは、暗号通貨のトレーダーが使用できるトークンに関する数値データです。これらの情報フィードは、暗号市場をモデル化し、Numerai Crypto Meta Modelを構築するために使用されます。これらは無料で提供されます。

暗号市場のシグナルの例として、以下のものがあります：

 - テクニカルシグナル（MACD、RSI、MFI）
 - 代替データシグナル（クレジットカード取引、衛星画像、ソーシャルメディアのセンチメント）
 - ブレンドシグナル（Barraリスクファクター、Fama Frenchファクター）

データ提供者の場合は、シグナルとして独自の特徴量を直接提出することができます。データサイエンティストの場合は、ユニークなデータをモデル化して予測をシグナルとして提出できます。シグナルは、我々のターゲットおよび他の提出されたシグナルと比較されてスコアリングされます。シグナルはNMR暗号通貨でステーキングすることができ、パフォーマンスに応じてNMRを獲得または失うことができます。

## データ

Numerai Data APIを使用して始めることができます：

```python
from numerapi import NumerAPI
import pandas as pd

napi = NumerAPI()
napi.download_dataset("crypto/v1.0/train_targets.parquet")
training_data = pd.read_parquet("crypto/v1.0/train_targets.parquet")
```

高品質なシグナルを生成するには、独自の暗号市場データを取得する必要があります。[Messari](https://messari.io/api)や[CoinMarketCap](https://coinmarketcap.com/api)などのデータプロバイダを利用して始めることができます。

もし暗号市場データを持っていなくても、Numeraiに興味がある場合は、[Numerai Tournament](https://numer.ai/home)で株式市場を予測してみてください。

## モデリング

データのモデリングをどこから始めるべきか分からない場合は、Numerai Tournamentで基本的なモデリング方法を学ぶことを強くお勧めします。モデリングスキルに自信がついたら、それをNumerai Cryptoに応用することができます。以下は、勾配ブースティングに基づくモデルの基本的な例です：

```python
import lightgbm as lgb
import pandas as pd
import random
from numerapi import NumerAPI
from typing import List

napi = NumerAPI()

def generate_training_features(df: pd.DataFrame) -> List[str]:
    # TODO: データを取得して特徴量を作成
    df['fake_feature_1'] = df.groupby(["symbol", "date"])['symbol'].transform(lambda x: random.uniform(0, 1))
    return ['fake_feature_1']

# 過去のターゲットファイルには["symbol", "date", "target"]の列が含まれています
napi.download_dataset("crypto/v1.0/train_targets.parquet")
train_df = pd.read_parquet("crypto/v1.0/train_targets.parquet")

# 各（symbol, date）に対してトレーニング特徴量を追加
feature_cols = generate_training_features(train_df)

model = lgb.LGBMRegressor(
    n_estimators=2000,
    learning_rate=0.01,
    max_depth=5,
    num_leaves=2 ** 5,
    colsample_bytree=0.1
)

model.fit(
    train_df[feature_cols],
    train_df["target"]
)
```

## 提出

Numerai Cryptoの提出はNumerai Signalsと非常に似ています。ただし、株式ティッカーの代わりにトークンシンボルを使用します。提出は、各シンボルにリターンを予測する数値を持つリストであるべきです。

提出するシンボルのリストは、Numerai Cryptoのトークンユニバースで定義されています。数値は0から1の間であるべきです。

以下は、Pythonでライブ予測を生成し、アップロードする方法の例です：

```python
def generate_features(df: pd.DataFrame):
    # TODO: ライブユニバース用にデータを取得し特徴量を作成
    df['fake_feature_1'] = df['symbol'].transform(lambda x: random.uniform(0, 1))

# APIキーを使用して認証
napi = NumerAPI("[your api public id]", "[your api secret key]")

# 最新のライブユニバースをダウンロード
napi.download_dataset("crypto/v1.0/live_universe.parquet")
live = pd.read_parquet("crypto/v1.0/live_universe.parquet")

# ライブユニバースの特徴量を生成
generate_features(live)

# ライブ予測を取得
live["signal"] = model.predict(live[feature_cols])

# 予測は0から1の間である必要があります
live["signal"] = live["signal"].rank(pct=True)

# 提出をフォーマットし保存
live[['symbol', 'signal']].to_parquet("submission.parquet")

# モデルIDを取得し、モデルを提出
models = napi.get_models(tournament=12)
for model_name, model_id in models.items():
    print(f'submitting {model_name}...')
    napi.upload_predictions("submission.parquet", model_id=model_id, tournament=12)

print('done!')
```

## スコアリング

スコアリングもまたNumerai Tournamentに非常に似ています。

Numerai Cryptoはトークンのリターンを予測するだけでなく、他のモデルが既に持っていない独自のシグナルを見つけることが目的です。

詳細は[スコアリングセクション](../numerai-crypto/submissions.md)をご覧ください。

## ステーキング

Numerai Tournamentと同様に、NMRを自分のモデルにステーキングすることで、パフォーマンスに基づいてNMRを獲得または失うことができます。詳細については[ステーキング](../numerai-crypto/staking.md)のドキュメントをお読みください。

{% hint style="info" %}
重要な点として、シグナルのステーキングの機会は、Numeraiからの投資契約、証券、金融資産のリターンに基づくスワップ、Numeraiのヘッジファンドへの関心、または我々が得る手数料への関心を提供するものではないことを理解してください。NumeraiのヘッジファンドはNumerai Cryptoとは全く関係なく、暗号通貨を取引せず、Numerai Crypto Meta Modelも使用しません。支払いは我々の裁量で行われ、ユーザーには開示されないブラックボックスターゲットに基づいて行われます。根本的に、Numerai CryptoはNumeraiが提供するサービスであり、ユーザーがNMRステーキングを通じて「本物の」シグナルを検証する方法を提供します。異なる期待を持つユーザーはステーキングしないでください。

詳しくは[利用規約](https://numer.ai/terms)をご確認ください。
{% endhint %}

## よくある質問

**トークンユニバースとは何ですか？**

取引可能な有名な暗号通貨トークンシンボルのセットです。Numeraiはこれらのシンボルのみの予測を求めています。詳細は[こちら](../numerai-crypto/submissions.md)をご覧ください。

**Numerai Tournament、Numerai Signals、およびNumerai Cryptoの違いは何ですか？**

Numerai TournamentとNumerai Signalsは、ユーザーが株式市場を予測するためのトーナメントです。Numerai Cryptoは暗号通貨市場を予測するためのものです。Numerai CryptoはSignalsに最も似ており、ユーザーは独自の特徴量を使用する必要があります。Numeraiはモデルを訓練し、検証データで評価するための過去のターゲットファイルを提供しますが、ユーザーは独自の特徴量を収集し、処理してモデルを訓練する必要があります。

**私のコード/データはNumeraiから保護されていますか？**

はい。Numeraiはあなたのデータや予測を構築するコードを閲覧しません。Numeraiが受け取るのは予測そのものだけです。コードをリバースエンジニアリングすることはほぼ不可能であり、Numeraiもそのようなことに関心を持っていません。

**参加するためにNMRをステーキングする必要がありますか？**

いいえ。予測ファイルを提出して、ステーキングせずにパフォーマンスを受け取ることができます。

**なぜ自分で取引しないのですか？**

あなたが自分で取引することは可能ですし、私たちはそれを止めることはできません。しかし、Numeraiはあなたのシグナルが既に知られており、他の誰もが使用しているかどうかを教えてくれます。すべての人が既に取引しているシグナルを取引しても、それほど価値がありません。[詳細はMediumの投稿をご覧ください](https://medium.com/numerai/building-the-last-hedge-fund-introducing-numerai-signals-12de26dfa69c)。

**参加するためにコーディングや金融の知識が必要ですか？**

基本的なモデルや探索的ノートブックは提供されており、初めての方でも参加できますが、コーディングや金融に不慣れな方はNumerai Tournamentに参加することをお勧めします。Numerai Cryptoは、成功するために高いレベルのコーディングと市場知識が必要です。

**Numeraiは暗号通貨を取引していますか？**

いいえ。Numeraiは暗号通貨を取引しておらず、Numeraiのヘッジファンドも取引していません。

**NumeraiはNumerai Crypto Meta Modelを使用していますか？**

いいえ。Numeraiの他の製品、資産、またはサービスは、Numerai Crypto Meta Modelを使用、消費、ブレンド、または影響されていません。

**Numerai Cryptoの予測やデータはNumeraiのヘッジファンドで使用されていますか？**

いいえ。NumeraiのヘッジファンドはNumerai Cryptoと完全に分離されており、Numerai Cryptoから何もヘッジファンドに影響を与えません。

## サポート

質問、サポート、フィードバックは[Discord](https://discord.gg/numerai)でご連絡ください！
