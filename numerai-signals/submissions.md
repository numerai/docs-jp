# 提出

## シグナルの提出とは？

シグナル作成に使用される基礎データは非常に多様です（監査済み財務情報、ニュース記事、駐車場の画像など）。ただし、すべてのシグナル提出は同じ基本形式、つまり、株式ティッカーのリストと、それぞれに0から1の範囲の数値が関連付けられている必要があります。

![株式市場シグナルの例](/.gitbook/assets/signals_submission_example.png)

提出内の株式ティッカーのリストは、**Numerai Signalsの株式市場ユニバース**によって定義されます。このユニバースには、世界で最大規模の約5000銘柄が含まれており、毎日更新されます。一般的に、日ごとに流動性の低い銘柄がわずかに入れ替わります。

最新のユニバースは、[Numerai data](https://signals.numer.ai/data/)から確認してください。

シグナルを提出する際には、少なくとも以下の2つの列を含める必要があります：

* `cusip`、`sedol`、`bloomberg_ticker`、`composite_figi`、または `numerai_ticker` の列 - ヘッダーで指定したティッカータイプに対応する有効なティッカーである必要があります。
* `signal` 列 - 値は0から1の範囲（0と1は含まない）である必要があります。

さらに、`live`提出が有効であるためには、以下の条件も満たす必要があります：

* ユニバース内の少なくとも100銘柄に対して有効な値（0から1の範囲）が含まれていること。
* 現在の`live`期間内に同じティッカーが複数回含まれていないこと。

## 自動化方法

APIを使用して提出ワークフローを自動化できます。予測結果を含むCSVを生成した後、以下のように提出を行います：

```python
from numerapi import SignalsAPI

# 認証
sapi = SignalsAPI("[your api public id]", "[your api secret key]")
sapi.upload_predictions("[path to your submission].csv")
```

* 次のいずれかの方法を使用できます：
  * [Numerapi](https://github.com/uuazed/numerapi)（公式Pythonクライアント）
  * [RNumerai](https://github.com/OmniacsDAO/Rnumerai)（非公式Rクライアント）
  * 他の言語向けの生の[GraphQL API](https://api-tournament.numer.ai/)
