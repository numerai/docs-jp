
# データ

## データ構造

Numerai Cryptoのデータセットは、トークンのユニバースとそのリターンを時系列で表した表形式のデータセットです。

概要として、各行は特定の時点でのトークンを表し、その時点はシンボルと日付で識別されます。日付は「マーケットクローズ」（特定の日の23:59 UTC）データが特徴量を生成するために使用された日を示しています。ラウンドとライブデータの文脈では、これはラウンドが始まる前の日を意味します。ターゲットは、その日付に対する将来のリターン（例：30日後）を測るものです。

## ターゲット

Numerai Cryptoには1つのターゲットがあり、それは30日後のトークンのリターンです。各ラウンドごとに、ユニバース内の各トークンの30日間のリターンはランク付けされ、ガウス化された後、5つのビンに分けられます。

## データAPI

Numerai Cryptoのデータセットにアクセスする最良の方法はデータAPIを使用することです：

```python
from numerapi import NumerAPI
napi = NumerAPI()

[f for f in napi.list_datasets() if f.startswith("crypto/v1.0")]

[
 'crypto/v1.0/live_universe.parquet',
 'crypto/v1.0/train_targets.parquet',
]

# トレーニングデータをダウンロード
napi.download_dataset("crypto/v1.0/train_targets.parquet")
```

 - `train_targets.parquet` には過去のシンボルとターゲットが含まれています。

 - `live_universe.parquet` には現在のラウンドのターゲットがない最新のトークンユニバースが含まれています。
