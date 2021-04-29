# 評価

## モデルの評価方法について

提出した予測ファイルが高いCorr,MMCを示すかはトーナメント開始時点ではわかりません。
NMRのペイアウトは1回のラウンドでのパフォーマンスに左右されますが、リーダーボードに掲載される評価や順位は20ラウンド分の評価の平均値を用います。

## 評価の計算方法

ラウンド`n`でのあなたの評価は、現在解決中のラウンドを含む過去20ラウンドの相関関係の加重平均です。

各ラウンドの重さは、ラウンドが進むにつれて変化します。新しいラウンドは低めにスタートし、解決に近づくにつれてwieght が増えていきます。解決されたラウンドは、最大加重１を持っていますが、それが完全にドロップされるまで、それが古くなるにつれてweight が減少します。

```python
# delta is the difference between the current and target round number
def round_weight(delta, day):
  if delta <= 4:
      return (5 * delta + day) / 20
  elif delta >= 16:
      return (5 * (20 - delta) - day) / 20
  else:
      return 1
```

例えば、ラウンド204の3日目のラウンドweight はこんな感じです。

![](../.gitbook/assets/image%20%2817%29.png)

## Missing scores

20ラウンドのウィンドウでの提出遅れや提出しなかったsubmission は、評判がモデル間で比較できるようにするためにペナルティが課せられます。

最初の提出が遅れた、または失敗した場合、`example_predictions`と同等のスコアが与えられます。それ以降の遅刻やミスした投稿には`-0.1`という非常に低いスコアが与えられます。

このペナルティを回避するために、[Numerai Compute](https://jp.docs.numer.ai/numerai-tournament/numerai-compute)を使って毎週の提出ワークフローを自動化しましょう。

