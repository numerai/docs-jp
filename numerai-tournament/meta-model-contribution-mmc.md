# Meta Model Contribution \(MMC\)

## MMCを最大化するモチベーション <a id="motivation"></a>

多くのNMRを受け取るためには、`Corr(correlation)`の高い予測モデルを作成し、提出する必要があります。<br>
一方、Numeraiは参加者から提出された予測ファイルを変換し、Numeraiがで使用できる形にします。  <br>
この時、Numeraiは全参加者の予測値を各参加者のNMRステーク量でアンサンブルしたモデル（メタモデル）を使用します。 <br> 
Numeraiはメタモデルの`Corr`を高めることを目標としています。そのため、Numeraiは`mmc`という指標を用いて参加者に報酬/罰金を与える仕組みを作りました。<br>  
`Corr`が個人のパフォーマンスに報酬を与えるのに対し、`mmc`はメタモデルの`correlation`やグループパフォーマンスへの貢献に報酬を与えます。<br>  

{% hint style="info" %}
トーナメント参加者の大多数はexample_model.pyと似たようなモデルです。他の人と異なる独自のモデルを作れば高いMMCを得られます。
{% endhint %}

{% hint style="success" %}
2019年には、[Integration_test](https://numer.ai/integration_test) のようなツリーベースのモデルがよいパフォーマンスを出しており、非常に人気があります。<br>
一方、`Corr`を最大化しつつ、`mmc`を最大化したい場合、どのようにモデル設計をすればよいでしょう？　<br>
他の人が考えないような方法で予測ファイルを提出すれば`mmc`を高められると思います。<br>
試行錯誤しましょう！<br>
{% endhint %}

## mmcの計算方法 <a id="calculation"></a>

特定のラウンドのユーザ（以下Uとする）の`mmc` は、以下の手順で計算されます。

* NMRをステークしているユーザーの67％をランダムに選択します。（選択されるユーザーは入れ替えられることがあります）
* これらのユーザーのステークしているNMRの量を用い、加重した予測値を計算します。
* 加重した予測値とUのモデルの両方を一様分布に変換します。
* 上記の予測値とUのモデルを中和します。中和とは、加重した予測値とUのモデルを線形回帰しその差分を計算することです。
* [参考](https://qiita.com/blog_UKI/items/fb401725288e58c92bd6)
* Uのモデルとtarget の間の共分散を計算します。
* この値を0.0841で割ったものがMMCのスコアです。 \(このステップは、期待されるスコアを相関と同じ大きさにするためです\)
* この全体のプロセスを20回繰り返しすことでMMCの平均スコアが計算できます。
![MMCの図](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F562749%2F1dfde04d-9648-7c92-8da3-e23eac997161.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&w=1400&fit=max&s=3f4b1b65c4d915e845070ad5a345846d "MMCの図")

本図は[UKIさん](https://twitter.com/blog_uki)が[作成](https://qiita.com/blog_UKI/items/fb401725288e58c92bd6)したものを引用しています。

## MMCのデザインについて <a id="design-considerations"></a>

* MMCのシステムが攻撃されないようにするには各参加者がステークしたNMRを加重する操作が必要です。
* 冗長性を高めるために、毎回67%の参加者をランダムサンプリングします。もし、この操作がなかったら、自分と似たファイルを提出した人が多額のNMRをステークしていた場合、過剰なペナルティが課されてしまう可能性があります。
 
## 議論 <a id="discussion"></a>

より詳しいMMCの計算については[こちら](https://forum.numer.ai/t/mmc2-announcement/93)をお読みください。MMCと収益性については[こちら](https://forum.numer.ai/t/mmc-staking-change-corr-mmc/698)をお読みください。MMCとオリジナリティの価値については、[このMediumの記事](https://medium.com/numerai/a-new-data-science-competition-where-being-different-pays-251c2aecc40a)をお読みください。

