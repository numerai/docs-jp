# データについて
## データ構造
Numerai Signalsデータセットは、時間の経過に伴う世界株式市場を記述した表形式のデータセットです。

概略として、各行は特定の時点での株式を表し、numerai_tickerまたはcomposite_figiと日付によって識別されます。日付は、マーケットクローズのデータが特徴量生成に使用された日を示し、ラウンドやライブデータのコンテキストではラウンドが始まる前日を指します。ターゲットは、その日付からの将来のリターン（例：20日後）の指標です。

## 特徴量
Signalsデータセットには以下が含まれます：

1. ファクター: ターゲットが中立であるファクターに類似したもので、モデルの独自性の判断、予測の中立化、またはデータセットの追加特徴量として使用できます。
2. スタータ特徴量: 比較的単純なクラシックなクオンツ指標で、リターン系列から構成されています。

### V2データセットの特徴量

データセットの特徴量は以下のとおりです:

```
feature_adv_20d_factor
feature_beta_factor
feature_book_to_price_factor
feature_country
feature_dividend_yield_factor
feature_earnings_yield_factor
feature_growth_factor
feature_impact_cost_factor
feature_market_cap_factor
feature_momentum_12w_factor
feature_momentum_26w_factor
feature_momentum_52w_factor
feature_momentum_52w_less_4w_factor
feature_ppo_60d_130d_country_ranknorm
feature_ppo_60d_90d_country_ranknorm
feature_price_factor
feature_rsi_130d_country_ranknorm
feature_rsi_60d_country_ranknorm
feature_rsi_90d_country_ranknorm
feature_trix_130d_country_ranknorm
feature_trix_60d_country_ranknorm
feature_value_factor
feature_volatility_factor
```

名前に{n}(d|w)が含まれる特徴量（例：feature_adv_20d_factor）は、n日またはn週間の期間で計算される時系列の特徴量です。
名前にcountry_ranknormが含まれる特徴量は、国ごとにグループ化された後、ランク付けされ、正規化されています。
factorを含む特徴量は、多くのターゲットが中立であるリスクファクターを指します。価格ファクターは国ごとにグループ化され、ランク付けされています。
PPOは、短期と長期の移動平均を比較するパーセンテージ価格オシレーターです。
RSIは、買われ過ぎ・売られ過ぎの指標として使用される相対力指数です。
TRIXは、モメンタムまたは反転指標として使用されるトリプル指数移動平均インジケーターです。
momentum_52w_less_4wは、直近4週間を除いた1年間の株式のリターンを指します。

## ターゲット
データセットのターゲットはヘッジファンドの戦略に適合するように設計されています。

私たちのヘッジファンドは、市場/国/セクターおよびファクターに中立であるため、ターゲットは市場/国/セクターや一般的なファクターでは説明されない株式特有のリターンとして解釈できます。簡単に言えば、私たちが求めているのは「アルファ」です。


### 主なターゲット
Signalsには、モデル性能の調整に役立つ3種類のターゲットがあります。

 - target_raw_return

公開データからリターンを自分で計算する場合、株式分割や配当などの要因で難しくなるため、正確なリターン列を構築するのが難しいことがあります。このターゲットはこれらの要因をすべて処理し、リターンをNumeraiの標準分布にビン分けします。このターゲットはICv2のスコアリングに使用されます。

 - target_factor_neutral
国、セクター、ベータ、モメンタム、サイズなどの標準ファクターに中立化されたターゲットです。このターゲットはRICおよびMMCの計算に使用されます。

 - target_factor_feat_neutral
多くのファクターおよびNumerai v4データセットのすべての特徴量に中立化されたターゲットです。これはSignalsデータセットの主要ターゲットで、CORRv4およびFNCv4のスコアリングに使用されます。

 - 補助ターゲット
主要ターゲットに加えて、異なるタイプの株式特有リターンを示す多くの補助ターゲットも提供しています。これらも株式特有リターンに基づいていますが、残差化される要素や期間が異なります（例：市場/国vsセクター/ファクター、20日 vs 60日）。補助ターゲットで学習したモデルが主要ターゲットのモデルを上回ることもあります。

注意：補助ターゲットの一部にはNaN値が含まれる場合がありますが、主要ターゲットにはNaNが含まれません。

## データAPI
Signalsデータセットへの最適なアクセス方法はデータAPIです。

## ファイル

Numeraiデータセットは複数のファイルで構成されています。

データAPIを使用して、利用可能なファイルを確認し、ファイルをダウンロードする方法は以下の通りです。

```python
from numerapi import NumerAPI
napi = NumerAPI()

[f for f in napi.list_datasets() if f.startswith("signals/v2.0")] 

['signals/v2.0/train.parquet',
 'signals/v2.0/validation.parquet',
 'signals/v2.0/validation_example_preds.csv',
 'signals/v2.0/validation_example_preds.parquet']
 
# トレーニングデータをダウンロード
napi.download_dataset("signals/v1.0/train.parquet")
```

 - `train.parquet` はティッカー、特徴量、およびターゲットを含む履歴データです。
 - `validation.parquet` はさらに多くの履歴データを含みます。
 - `validation_example_preds.parquet` は、例示モデルの検証予測を含みます。
