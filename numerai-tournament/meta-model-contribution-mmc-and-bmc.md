# メタモデル貢献度（MMC & BMC）

## MMC, BMC とは

メタモデル貢献度（MMC）は、モデルの予測がメタモデルに中立化された後のターゲットとの共分散です。同様に、ベンチマークモデル貢献度（BMC）は、モデルの予測がステーク加重の[ベンチマークモデル](https://numer.ai/~benchmark_models)に中立化された後のターゲットとの共分散です。

これらの指標は、モデルの独自の成分がメタモデルの相関（BMCの場合はベンチマークモデル）にどのように貢献するかを示しています。モデルの予測をメタモデルまたはベンチマークモデルで中立化することにより、残りの直交成分のターゲットとの共分散がそのモデルの貢献です。

2024年2月現在、Tournamentでは[CorrとMMCのみが使われています](https://forum.numer.ai/t/changing-scoring-payouts-again-to-mmc-only/6794)。

## 計算

特定のラウンドのユーザーのMMCを計算するためには、以下の手順を実行します：

- 提出物の予測値とメタモデルの値を正規化する
- 提出物の予測値をメタモデルに対して中立化する
- 中立化された予測値とターゲットの共分散を計算する

```python
# https://github.com/numerai/numerai-tools/blob/master/numerai_tools/scoring.py
import numpy as np
import pandas as pd
from scipy import stats

def contribution(predictions: pd.DataFrame, meta_model: pd.Series, live_targets: pd.Series) -> pd.Series:
    """与えられた予測に関する与えられたメタモデルとの貢献相関を計算します。

    その後、次の手順で貢献相関を計算します：
    1. 各予測とメタモデルを順位付けし、順位を保持します
    2. 各予測とメタモデルをガウス化します
    3. 各予測をメタモデルに関して直交化します
    4. 直交化された予測とターゲットを乗算します

    引数:
        predictions: pd.DataFrame - 評価する予測
        meta_model: pd.Series - 評価対象のメタモデル
        live_targets: pd.Series - 評価対象のライブターゲット

    戻り値:
        pd.Series - 予測の各列の結果の貢献相関スコア
    """
    def rank(df: pd.DataFrame, method: str = "average") -> pd.DataFrame:
        return df.apply(lambda series: (series.rank(method=method).values - 0.5) / series.count())

    def tie_kept_rank(df: pd.DataFrame) -> pd.DataFrame:
        # rank columns, but keep ties
        return rank(df, "average")

    def filter_sort_index(s1, s2, max_filtered_ratio=0.2):
        ids = s1.dropna().index.intersection(s2.dropna().index)
        # ensure we didn't filter too many ids
        assert len(ids) / len(s1) >= (1 - max_filtered_ratio)
        assert len(ids) / len(s2) >= (1 - max_filtered_ratio)
        return s1.loc[ids].sort_index(), s2.loc[ids].sort_index()

    def gaussian(df: pd.DataFrame) -> pd.DataFrame:
        assert np.array_equal(df.index.sort_values(), df.index)
        return df.apply(lambda series: stats.norm.ppf(series))

    def orthogonalize(v, u):
        return v - np.outer(u, (v.T @ u) / (u.T @ u))

    # 予測、メタモデル、ターゲットをお互いにフィルタリングして並び替える
    meta_model, predictions = filter_sort_index(meta_model, predictions)
    live_targets, predictions = filter_sort_index(live_targets, predictions)
    live_targets, meta_model = filter_sort_index(live_targets, meta_model)

    # メタモデルと予測を順位付けして正規化して平均=0、標準偏差=1にします
    p = gaussian(tie_kept_rank(predictions)).values
    m = gaussian(tie_kept_rank(meta_model.to_frame()))[meta_model.name].values

    # 予測をメタモデルに関して直交化します
    neutral_preds = orthogonalize(p, m)

    # ターゲットを中心化します
    live_targets -= live_targets.mean()

    # ターゲットと中立化された予測を乗算します
    # 平均=0なので、これは共分散に相当します
    mmc = (live_targets @ neutral_preds) / len(live_targets)

    return pd.Series(mmc, index=predictions.columns)
```

## DiagnosticにおけるBMC

Diagnosticでは、BMCはステーク加重のベンチマークモデルではなく、単一のモデルであるステークが最も高いベンチマークモデルに対して計算されます（[こちら](https://numer.ai/~benchmark_models)を参照）。LBとDiagnosticのBMCには違いがあります：

- リーダーボード（LB）は **Live**データのパフォーマンスを表示します - これは、ここで計算されるBMCがNumeraiとデータサイエンティストがその時点で知っていたことに基づいているため、その時点でのステーク加重のベンチマークモデルに対してモデルを評価するのが公平です。初期のラウンドでは、ステーク加重のベンチマークモデルは単にv2データセットからの例の予測です。
- Diagnosticは **Validation**データのパフォーマンスを表示します - これは、より良いモデリング技術、より良いデータ、より良いターゲットを使用している可能性があり、v2データセットからの例の予測に対して評価するのは誤解を招く可能性があるためです。代わりに、できるだけ最新で最高のモデルに対して評価する必要があります。

BMCがLBとDiagnosticでなぜ異なるのかまだわからない場合は、[ターゲットアンサンブルノートブック](https://github.com/numerai/example-scripts/blob/master/target_ensemble.ipynb)をご覧ください。

## 議論

MMC & BMC についてもっと詳しく読みたい方は[こちら](https://forum.numer.ai/t/mmc-staking-starts-jan-2-2024/6827)をご参照ください。
