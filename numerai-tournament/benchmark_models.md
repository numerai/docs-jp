
# ベンチマークモデル

## 概要

ベンチマークモデルは、Numeraiチームが構築した一連の標準モデルです。その予測は、毎ラウンド配布されるため、誰でも簡単にそれらを提出し、望むならステークすることができます。

モデルのリストとその最近のパフォーマンスはこちらです：

[NUMERAI BENCHMARK MODELS](https://numer.ai/~benchmark_models)

## 予測のダウンロード

検証およびライブの予測は[Numerai API](https://github.com/uuazed/numerapi)を介して利用できます。

```python
!pip install numerapi
from numerapi import NumerAPI
napi = NumerAPI()
napi.download_dataset("v5.0/train_benchmark_models.parquet", "train_benchmark_models.parquet")
napi.download_dataset("v5.0/validation_benchmark_models.parquet", "validation_benchmark_models.parquet")
napi.download_dataset("v5.0/live_benchmark_models.parquet", "live_benchmark_models.parquet")
```

## ベンチマークモデルの作成方法

### ウォークフォワード交差検証

すべての予測はウォークフォワードフレームワークを使用して行われます。これは、すべての予測が、予測が行われる日付より前に利用可能なデータのみを使用してトレーニングされたモデルを使用して行われることを意味します。

具体的には、データは156Eraのチャンクに分割されます。それから、各Eraチャンクごとに、最初のEraチャンクからパージEraまでトレーニングされたモデルによって予測が行われます。パージEraの数は、20Dターゲットの場合は8であり、60Dターゲットの場合は16です。

したがって、モデルはEra1〜148でトレーニング、Era149〜156がパージ、Era157〜312で評価します。
次のモデルはEra1〜304でトレーニング、Era305〜312がパージ、Era313〜468で評価します。
ウォークフォワード交差検証のウィンドウは以下のようになります。

| ウィンドウ | 学習開始Era | 学習終了Era | 評価開始Era | 評価終了Era |
|------------|----------|----------|----------|----------|
| 1          | 1        | 148      | 157      | 312      |
| 2          | 1        | 304      | 313      | 468      |
| 3          | 1        | 460      | 469      | 624      |
| 4          | 1        | 616      | 625      | 780      |
| ...        | ...      | ...      | ...      | ...      |


### 標準的な大規模なLGBMパラメータ

すべてのモデルは、以下のLGBMパラメータを使用します：

```python
standard_large_lgbm_params = {
    "n_estimators": 20000,
    "learning_rate": 0.001,
    "max_depth": 6,
    "num_leaves": 2**6,
    "colsample_bytree": 0.1,
}
```

より多くの木を持つことが役立つことがわかりましたし、より深い木を持つことでより少ない木でも同様の結果が得られることもわかりました。詳細はこちらをご覧ください：[https://forum.numer.ai/t/super-massive-lgbm-grid-search/6463](https://forum.numer.ai/t/super-massive-lgbm-grid-search/6463)

### アンサンブル

すべてのアンサンブルは、以下の手順を使用します：

1. 各Eraごとに予測をガウス化する
2. 標準偏差が1になるように標準化する
3. 予測を、各モデルごとに望ましい重みを表す重みベクトルとドット積する
4. 結果の予測ベクトルをガウス化し、中和する特徴がある場合は中和する

ステップ1、2、および3は次のようになります：

```python
# https://forum.numer.ai/t/benchmark-models/6754/9を元に少し改変
def rank_gauss_pow1(s: pd.Series) -> pd.Series:
    # 順位を正規化
    s_rank = (s.rank(method="average") - 0.5) / s.count()

    # ガウス化
    s_rank_norm = pd.Series(stats.norm.ppf(s_rank), index=s_rank.index)

    # 標準偏差1に標準化
    result_series = s_rank_norm / s_rank_norm.std()
    return result_series


ensemble_cols = ["V4_LGBM_NOMI20", "V42_RAIN_ENSEMBLE"]
weight_vector = [0.1, 0.9]
for col in X[ensemble_cols]:
    if "era" in X.columns:
        X[col] = X.groupby("era", group_keys=False)[col].transform(lambda s1: rank_gauss_pow1(s1))
    else:
        # Xが単一のEraのみを含むことを確認します
        assert 1800 < X.shape[0] < 6000
        X[col] = rank_gauss_pow1(X[col])
return X[ensemble_cols].dot(weight_vector)
```

### 中和

一部のモデルには中和（neutralize）が含まれています。これは、各特徴への予測の露出度を求めるために回帰を行い、その露出度を予測ベクトルから差し引いて、その結果がすべてのその特徴に直交するベクトルになるようにすることです。

以下は、いくつかの予測列（columns）をいくつかの特徴（ニュートラライザー）で中和するコードです。

```python
def neutralize(df, columns, neutralizers=None, proportion=1.0, era_col="era"):
    if neutralizers is None:
        neutralizers = []
    unique_eras = df[era_col].unique()
    computed = []
    for u in unique_eras:
        df_era = df[df[era_col] == u]
        scores = df_era[columns].values
        scores2 = []
        for x in scores.T:
            x = pd.Series(x)
            x = (x.rank(method="first") - 0.5) / len(x.dropna())
            x = stats.norm.ppf(x)
            scores2.append(x)
        scores = np.array(scores2).T
        exposures = (
            df_era[neutralizers]
            .fillna(df_era[neutralizers].median())
            .fillna(0.5)
            .values
        )
        scores -= proportion * exposures.dot(
            np.linalg.pinv(exposures.astype(np.float32), rcond=1e-6).dot(
                scores.astype(np.float32)
            )
        )

        scores /= pd.DataFrame(scores).std(ddof=0, axis=0, skipna=True).values

        computed.append(scores)

    return pd.DataFrame(np.concatenate(computed), columns=columns, index=df.index)
```

## ベンチマークモデルの命名規則

**{data\_version}\_LGBM\_{target}**

これらは、データバージョン（V2、V3、V4、V41、V42、V43、V5）とターゲットの組み合わせを持つ多くのモデルがあります。

これらは、標準のウォークフォワード方法でトレーニングされたモデルであり、標準的なLGBMパラメータを使用し、指定されたデータバージョンとターゲットを使用しています。それだけです！

[https://numer.ai/~benchmark_models](https://numer.ai/~benchmark_models)から最新のデータバージョンのモデルを確認することができます。

