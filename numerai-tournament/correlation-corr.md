# 相関（CORR）
## CORRとは？

Numeraiの主なスコアリング指標は、モデルの予測とターゲットとの相関関係です。
Numeraiは「Numerai Corr」と呼ぶ相関の特別なバリエーションを使用します。この指標は、予測が実際の取引で使用された場合の実際のポートフォリオのリターンの優れた代理となるように設計されています。

## CORR はどのように計算されるのか？

[Numerai公式が公開](https://github.com/numerai/example-scripts/blob/master/utils.py)しているコードを以下に記載します。

```python
import numpy as np
from scipy import stats


def numerai_corr(preds, target):
    # rank (keeping ties) then Gaussianize predictions to standardize prediction distributions
    ranked_preds = (preds.rank(method="average").values - 0.5) / preds.count()
    gauss_ranked_preds = stats.norm.ppf(ranked_preds)

    # make targets centered around 0
    centered_target = target - target.mean()

    # raise both preds and target to the power of 1.5 to accentuate the tails
    preds_p15 = np.sign(gauss_ranked_preds) * np.abs(gauss_ranked_preds) ** 1.5
    target_p15 = np.sign(centered_target) * np.abs(centered_target) ** 1.5

    # finally return the Pearson correlation
    return np.corrcoef(preds_p15, target_p15)[0, 1]
```

手順的には以下の通り

 1. 予測のランク値化および平均値を0に変換

 2. 予測値とターゲット両方を1.5乗

... ヘッジファンドは予測リターンが最も高いか低い銘柄のみを取引する傾向があるため、テールを強調するためにこのような処理を行います。

 3. ピアソン相関係数を計算

1.でランク化を行っているため、スピアマン相関係数に近いものの、2.の1.5乗の処理により典型的な順位相関よりもテールに依存します。

### ウェブサイト上のCORR

ウェブサイトでは、CORR のさまざまなバリエーションを見ることができます。

CORR20V2 - メインターゲットの20日バージョンに対する最新の相関係数のスコア。

CORJ60 - Jeromeという補助ターゲットの60日バージョンに対する相関性
