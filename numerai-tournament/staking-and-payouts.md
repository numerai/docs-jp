# Staking and Payouts

## Motivation

[シビル攻撃](https://en.wikipedia.org/wiki/Sybil_attack)に対抗するためには、どのようにしてインセンティブを付与してペイアウトシステムを設計すればよいのでしょうか？

その答えはstaking です。

ヌメライは正確な予測を望んでおり、それに報いることを望んでいます。あなたがどれだけ稼ぐことができるか/燃やすことができるかは、あなたのパフォーマンスと賭け金の関数です。これは、[ゲームにスキン](https://www.amazon.com/dp/B075HYVP7C/)を持っていることとしても知られています。

ステイクはまた、Numeraiにペイアウトを配分するためのシビル耐性のある方法を提供します。ペイアウトはステーク値のパーセンテージであるため、単に重複したアカウントを作成するだけではペイアウトシステムをゲーム化することはできません。

stakeせずにNumeraiに参加することで、トーナメントの詳細や自分のモデルの性能を知ることができます。自分のモデルに自信が持てるようになったら、そのモデルにstakeすることができます。stakeの最小値は0.01NMRです。

## Managing your stake

Numeraiのウェブサイトでは、「Manage Stake」をクリックしてstake を管理することができます。このモーダルを使用して、ステークの金額を増減したり、`MMC`に参加したり、参加しないことを選択したりすることができます。

![](../.gitbook/assets/image%20%2817%29.png)

stake を増やすと、あなたのwallet からNMRを取り出し、stake に入れます。stake を減らすと、stake からNMRを取り出してwalletに戻します。

あなたのステークへの変更はすぐに適用されるのではなく、代わりに、右図のような`effective_date`に適用されます。

* `mmc`のオプトインまたはオプトアウトは、来週の`Thursday`に適用されます
* 増加は来週の`Thursday`に適用されます 
* 減少は来週の木曜日の`stake amount`に影響しますが、資金は来週の`Thursday + 4 weeks`後にのみリリースされます
* Decreases impact your `stake amount`next Thursday,  but the funds are only released after next `Thursday + 4 weeks`

## Payouts

各ラウンドのペイアウトは、提出期限後の最初の木曜日の`stake_value`に基づいています。ペイアウトは、木曜日の次のラウンドの開始時にステーク値にロールバックされます。

例えば、ラウンドNの`stake_value`が100で、`correlation = 0.05`の場合、ペイアウトは+5NMRとなり、これはラウンドN+4のstake valueに適用されます。

mmcをオプトインしている場合は、`correlation`と`mmc`の両方の料金が支払われます。`correlation`は常に 1 倍率ですが、mmc は 0.0x、0.5x、1.0x、2.0x のいずれかになります。

 例えば、`mmc+corr` が選択されていて、ラウンドスコアが `correlation = 0.05`、`mmc = 0.01` の場合、ペイアウトは `0.06 * stake_value NMR` _となります。_

代わりに、corr + 2xmmc を選択した場合、同じラウンドでは、ペイアウトは `0.07 *  stake_value NMR` となります。 

2x MMC はリスクが高いことに注意してください。 このオプションを選択する前に、モデルのライブMMCパフォーマンスを確認してください。 

ペイアウトの上限は、1 ラウンドあたりプラスまたはマイナス 25%です。

{% hint style="warning" %}
stake を減らすと、すぐに次のラウンドで`stake_value`が下がりますが、それは4週間後にしか起こりません。
{% endhint %}

{% hint style="info" %}
減少リクエストをキャンセルすると、すぐに次のラウンドでステーク値が元の値に戻ってしまいます。
{% endhint %}

コミュニティで構築された[Numerai Payouts](https://docs.numer.ai/help/payouts-app)アプリでペイアウトを追跡しましょう。

## Compounding

毎週新しいラウンドがあり、各ラウンドが4週間続くので、4週間遅れでstake valueが複合します。

例えば、6週目のstake value は、5週目の前回のstake value（110NMR）＋2週目のペイアウト（-5NMR）＝105NMRを基準にしています。

![stake compounding](https://documents.app.lucidchart.com/documents/2cb7265f-6e5b-454a-a84d-6f32b6058f34/pages/0_0?a=466&x=249&y=136&w=1112&h=486&store=1&accept=image%2F*&auth=LCA%20a086c3be9ef17d9fa2cd22ee9808e742d1a2d888-ts%3D1590449860)

## Abuse

当社は、お客様が積極的にペイアウトルールを悪用している、または悪用していると当社が判断した場合には、お客様の賭け金を払い戻し、すべてのearning とburning を無効にする権利を留保します。

当社の支払いシステムは攻撃に強いように設計されており、ユーザーに罰を恐れずに新しいアイデアを試してもらいたいため、この権利を行使することはめったにありません。 ‌

悪用を発見した場合には、そのことをコミュニティに伝え、悪用に対してどのような行動をとるのかを説明します。ここではその [one example](https://forum.numer.ai/t/leaderboard-bonus-exploit-uncovered/200/8) を紹介します。

