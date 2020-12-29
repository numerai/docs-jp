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

To calculate a user's \(U\) `mmc` for a given round we

* select a random 67% of all staking users \(with replacement\)
* calculate the stake weighted predictions of these users
* transform both the stake weighted predictions, and U's model to be uniformly distributed
* neutralize U's model with respect to the uniform stake weighted predictions
* calculate the covariance between U's model and the targets
* divide this value by 0.0841 \(this step is to bring the expected score up to the same magnitude as correlation\)
* the resultant value is an MMC score
* repeat this whole process 20 times and keep the average MMC score

## Design Considerations <a id="design-considerations"></a>

* Stake weight is necessary to make the system unattackable
* Sampling a random 67% each time is important to incentivize some redundancy.

  A very large staker submitting similar predictions to yours would penalize you too much if we didn't do this.

## Discussion <a id="discussion"></a>

Read more about the MMC calculation [here](https://forum.numer.ai/t/mmc2-announcement/93). Read more about MMC and profitability [here](https://forum.numer.ai/t/mmc-staking-change-corr-mmc/698). Read [this Medium post about MMC](https://medium.com/numerai/a-new-data-science-competition-where-being-different-pays-251c2aecc40a) and the value of originality.[  
](https://app.gitbook.com/@numerai/s/numerai-tournament/tournament/tools)

