# Meta Model Contribution \(MMC\)

## Motivation <a id="motivation"></a>

各ユーザーは、個々の相関スコアを最大化するようにインセンティブを与えられています。しかし、Numeraiはメタモデルの相関スコアを最大化したいと考えています。ここで、メタモデルは、すべてのsubmission のstake 加重アンサンブルです。

メタモデル貢献度`mmc`は、このギャップを埋めるために設計されています。`correlation`が個人のパフォーマンスに報酬を与えるのに対し、`mmc`はメタモデルの`correlation`やグループパフォーマンスへの貢献に報酬を与えます。

{% hint style="info" %}
もしあなたがバスケットボールチームのマネージャーで、あなたのチームにすでに4人の[シャーク・オニール](https://ja.wikipedia.org/wiki/%E3%82%B7%E3%83%A3%E3%82%AD%E3%83%BC%E3%83%AB%E3%83%BB%E3%82%AA%E3%83%8B%E3%83%BC%E3%83%AB)がいるとしたら、あなたはもう1人のシャークを5人目としてドラフトしますか？それとも[コービー](https://ja.wikipedia.org/wiki/%E3%82%B3%E3%83%BC%E3%83%93%E3%83%BC%E3%83%BB%E3%83%96%E3%83%A9%E3%82%A4%E3%82%A2%E3%83%B3%E3%83%88)のようなガードを取りますか？
{% endhint %}

{% hint style="success" %}
2019年には、Integration\_testのようなツリーベースのモデルがよいパフォーマンスを出しており、非常に人気があります。これを知っていると、このグループのモデルとうまくアンサンブルするモデルをどのように設計するのでしょうか？
{% endhint %}

## Calculation <a id="calculation"></a>

特定のラウンドのユーザ（以下Uとする）の`mmc` を計算するには、以下の手順を踏みます。

* 全stake ユーザーの67％をランダムに選択します。（入れ替えあり）
* これらのユーザーのstake 重み付き予測を計算します。
* stake 重み付き予測とUのモデルの両方を一様分布に変換します。
* 一様なstake 重み付き予測に関してUのモデルをneutralize します。
* Uのモデルとtarget の間の共分散を計算します。
* この値を0.0841で割ります。 \(このステップは、期待されるスコアを相関と同じ大きさにするためです\)
* 結果として得られる値は、MMC のスコアです。
* この全体のプロセスを20回繰り返し、平均MMCのスコアを保持します。

## Design Considerations <a id="design-considerations"></a>

* システムが攻撃されないようにするにはstake weight が必要です。
* 毎回ランダムに67%の確率でサンプリングすることは、ある程度の冗長性を高めるために重要です。  あなたに似たような予測を提出した非常に大きなstake をした者は、我々がこれをしなかったら、あなたにペナルティを与えすぎてしまいます。

## Discussion <a id="discussion"></a>

より詳しいMMCの計算については[こちら](https://forum.numer.ai/t/mmc2-announcement/93)をご覧ください。MMCと収益性については[こちら](https://forum.numer.ai/t/mmc-staking-change-corr-mmc/698)をお読みください。MMCとオリジナリティの価値については、[このMediumの記事](https://medium.com/numerai/a-new-data-science-competition-where-being-different-pays-251c2aecc40a)をお読みください。

