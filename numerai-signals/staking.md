# ステーキング

あなたのシグナルが十分に低いチャーン率を持っている場合、モデルにNMRをステーキングして、`FNCV4`および`MMC`スコアに基づき報酬を得たり、焼却されたりすることができます。

ステーキングとは、Ethereumブロックチェーン上の[スマートコントラクト](https://github.com/numerai/tournament-contracts)にNMRをロックすることを指します。ステーキング期間中、NumeraiはロックされたNMRに対して報酬の追加や焼却を行う権限を持ちます。

ウェブサイト上でステーキングを管理することができます。ステーキングを増やす場合、NMRはウォレットからステーキングコントラクトに転送され、減らす場合は約4週間の遅延後にコントラクトからウォレットにNMRが戻されます。また、どのスコアに対してステーキングするかを選ぶステーキングタイプも変更可能です。

![](https://docs.numer.ai/\~gitbook/image?url=https:%2F%2Fgblobscdn.gitbook.com%2Fassets%252F-LmGruQ\_-ZYj9XMQUd5x%252F-MTwWeGztnW6NaH6Sd\_A%252F-MTxK8xvV36McXIClWAt%252Fimage.png%3Falt=media%26token=aea91c60-7079-439b-bbd6-f64e9d8c26d7\&width=768\&dpr=4\&quality=100\&sign=c26f0dc43daabd09b8834fe5fa0d22f7e105ca7c1b17f4fb0c4b1aa5c8ff0b2e)

{% hint style="info" %}
シグナルのステーキングの機会は、Numeraiが投資契約、証券、金融資産のリターンに基づくスワップ、Numeraiのヘッジファンドまたは当社の手数料の利益に対する権利、あるいはNumeraiそのものに対するものではないことを強調しておきます。報酬は非公開のブラックボックスターゲットに基づき、当社の裁量で行われます。Numerai Signalsは、NMRステーキングを使って「実際の」シグナルを検証する方法としてユーザーがシグナルの価値を評価できるサービスです。異なる期待を持つユーザーはステーキングを行うべきではありません。

**詳細については、[利用規約](https://numer.ai/terms)をご参照ください。**
{% endhint %}

## 報酬

報酬はステーク価値とスコアの関数で決まります。ステーク価値が高く、スコアが高いほど、より多くの報酬を得ることができます。スコアがマイナスの場合、ステークの一部が焼却されます。報酬は1ラウンドあたりステーク価値の±5％に制限されています。

```python
payout = stake_value * payout_factor * (fncv4 * 1 + mmc * 2)
```

`stake_value`はラウンドのclose時のステーク価値（保留中のリリースを除く）で、提出がない場合は0となります。

`payout_factor`は、総ステーキングNMRが`stake_cap_threshold`を超えると対数的に減少します。`stake_cap_threshold`の値については[こちら](../numerai-tournament/staking.md#the-payout-factor)をご参照ください。
