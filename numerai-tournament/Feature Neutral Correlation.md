# Feature Neutral Correlation \(FNC\)

## Motivation <a id="motivation"></a>
Feature Neutral Correlation（FNC）とは、モデルの予測値と、Numeraiがもつすべての特徴量を中和した後の、ターゲットとの相関のことです。 
少数の特徴量に依存しているモデルは、FNCが低くなりますが、短期的には高いパフォーマンスを持つかもしれません。
たとえば、dex7を予測値とした[このモデル](https://numer.ai/uki_monitor1/submissions)は、高いパフォーマンスを示す時期があります。

しかし、このようなモデルでは長期的なパフォーマンスが低い可能性があります。
様々な特徴量を使用し、なおかつターゲットとの相関性が高いモデルは、FNCが高く、長期的に安定したパフォーマンスを発揮する可能性が高いです。


# FNCの計算方法
・あるラウンドにおけるユーザのFNCを計算するために、提出された予測値を正規化します。 
・Numeraiがもつ特徴量に対して中和をします。 
・中和された予測値とターゲットとのスピアマン順位相関を計算します。

```python
def calculate_fnc(sub, targets, features):
    """    
    Args:
        sub (pd.Series)
        targets (pd.Series)
        features (pd.DataFrame)
    """
    
    # Normalize submission
    sub = (sub.rank(method="first").values - 0.5) / len(sub)

    # Neutralize submission to features
    f = features.values
    sub -= f.dot(np.linalg.pinv(f).dot(sub))
    sub /= sub.std()
    
    sub = pd.Series(np.squeeze(sub)) # Convert np.ndarray to pd.Series

    # FNC: Spearman rank-order correlation of neutralized submission to target
    fnc = np.corrcoef(sub.rank(pct=True, method="first"), targets)[0, 1]

    return fnc
```    
## Discussion <a id="discussion"></a>

より詳しいFNCの計算については[こちら](https://forum.numer.ai/t/model-diagnostics-feature-exposure/899)をご覧ください。
