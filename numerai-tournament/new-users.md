## はじめに

2015年に設立された[Numerai](https://numer.ai)は、毎週データサイエンスのトーナメントを開催しています。世界中のデータサイエンティストが、難読化されたデータを無料でダウンロードし、株式市場の予測モデルを構築することでトーナメントに参加できます。ダウンロードできるデータは難読化されたいるため、金融の知識がなくても参加することができます。

参加者は、自分の予測に賭け金をかけることでトーナメントに参加できます。良い予測を提出すると、より多くの仮想通貨（[NMR](https://vimeo.com/205032211)）を得ることができ、悪い予測を提出すると、NMRを没収されます。

Numeraiは、[メタモデル](https://www.youtube.com/watch?v=dhJnt0N497c)と呼ばれる参加者のモデルを統合したモデルを構築し、得られたデータを自社のグローバル・エクイティ・ヘッジファンドの取引に反映させています。

参加者は、賭け金の有無にかかわらずトーナメントに参加することができますが、NumeraiはNMRがステークされたモデルのみを使用します。参加者は自分でデータを用意する必要はありませんが、チームから与えられたデータを最適化し、自分の予測を提出することが求められます。

## 目次 

1. Numeraiのホームページと用語集の読み方

2. Numeraiに予測を提出する方法

3. モデル診断の読み方

4. Numeraiとコミュニティに関連する便利なリンク

## 1. Numeraiのホームページと用語集の読み方 

NumeraiのホームページのURLは、[https://numer.ai/tournament](https://numer.ai/tournament) です。

**Numeraire（NMR）トークン:** Numeraireは[ERC-20ベースのトークン](https://www.coinbase.com/price/numeraire)で、Numeraiへのステーキングに使用されます。

NMRは、Numeraiのトーナメントに参加したり、Numeraiに技術的な貢献をすることで獲得できます。NMRトークンは、Numeraiが構築されている[Erasure Protocol](https://erasure.world/)で使用することができます。現在、Erasureプロトコル上のアプリは、Numerai、Numerai Signals、Erasure Bayですが、プロトコルは誰でも構築できるようになっています。

**Corr：** 提出された予測データとターゲットとの相関係数を表します。

**TC：** 真の貢献度（TC）は、モデルの予測がNumeraiのメタモデルにとってどれだけ価値があるかを示します。

**FNC:** Feature neutral correlation （FNC）は、提出した予測データをNumeraiのすべての特徴量に対して中和した後の、ターゲットとの相関係数を表します。

**Corr / TC / FNC Rep:** Rep（評判）は、過去20ラウンドにおけるその指標の加重平均であり、リーダーボードでユーザーをランク付けするために使用されるものです。Repについての詳細は[こちら](https://docs.numer.ai/tournament/reputation)

**ステーク** 自分のモデルの予測にどれだけ自信があるかを示すために、NMRをステーク（預入れ＋ロック）をします。良い予測を提出した場合、NMRを得ることができます。一方、悪い予測を提出した場合はNMRが没収されます。賭け金の最小値は3NMRです。ステークせずに参加して、自分のモデルがどのようなパフォーマンスを示すかを知ってから、ステークするかどうかを決めることができます。

**ペイアウト** 賭けたNMRに応じて受け取る報酬。毎週（1ラウンドは4週間）、賭け金の最大25％を獲得または没収されます。ステーキングとペイアウトについての詳細は[こちら](https://docs.numer.ai/tournament/staking-and-payouts)をご覧ください。

### ホームページ上部

![image](https://user-images.githubusercontent.com/78800304/120104122-eca94d80-c18d-11eb-8f06-d0128a2d7bb4.png)

**DOCS:** ルール、FAQ、新規ユーザーセクションを含むNumeraiの[ドキュメント](https://docs.numer.ai/)へのリンクです。

**CHAT:** 告知、一般的な議論、データサイエンスなどのチャンネルを含むチャットスペースです。NumeraiチームはRocketChatに積極的に参加しており、プロフィールには`team`タグが付いています。チームメンバーは主に太平洋時間で活動しています。参加は[こちら](http://community.numer.ai/)から。

**FORUM:** Numerai、データサイエンス、ステイク戦略などに関連する議論のためのスペースです。主にコミュニティ内での情報共有を目的としています。リンクは[こちら](https://forum.numer.ai/)です。

**LEADERBOARD：** Numeraiに投稿された予測結果のランキングです。ステーク量、Rep、TCなどでソート可能です。

**アカウント:** 「ウォレット」「モデル」「設定」「ログアウト」の4つのリンクがあります。

・ウォレット：NMRトークンの入金と出金が行えます。

入金(deposit):ウォレットに登録されているアドレスにNMRトークンを送ることで入金できます。このアドレスに他のトークンを送ることはできません。

出金(withdraw):NMRトークンを自分のNumeraiウォレット以外のアドレスに出金することができます。出金を依頼する前に、出金先の外部アドレスがNMR受け取りに適していることを確認してください。間違ったアドレスに送ったNMRは回収できません。

![image](https://user-images.githubusercontent.com/78800304/120104136-fd59c380-c18d-11eb-9986-e510285a0b4b.png)

**モデル** このページでは、Numeraiに投稿するモデルを追加／削除できます。モデルの追加／削除をするには、「新しいモデルの追加」／「既存のアカウントの吸収」を押してください。
複数モデルのアカウントやアカウントの吸収については[こちら](https://forum.numer.ai/t/announcing-general-availability-of-multi-model-account-support-for-all-users/399)をご覧ください。

![image](https://user-images.githubusercontent.com/78800304/120104142-08145880-c18e-11eb-8874-aa5533355ef5.png)

**設定：** Eメール、パスワード、2段階認証（2FA）、APIキーの設定を行います。

アカウントがNMRを保持しているため、2FAによるセキュリティ強化を推奨します。2FAを使用する場合は、リカバリーコードを保存する必要があります。2FAのデバイスにアクセスできなくなっても、Numeraiはアカウントをリセットしません。

![image](https://user-images.githubusercontent.com/78800304/120104152-119dc080-c18e-11eb-88ed-ada0e1b5f6d1.png)

### ホームページ下部

**モデル情報：** モデルのランキングやCorr・TCのRepなどの情報を掲載しています。ˇのボタンでモデルを切り替えることができます。

**データ情報:** 最新ラウンドのデータダウンロードリンクと、予測結果のアップロードリンクです。

**ステーク:** NMRのステーク量を調整できます。ステーク方法には、CorrやTCがあります。Corrではターゲットとの相関関係のみにNMRを賭けることができ、TCでは真の貢献にNMRを賭けることができます。

## 2. Numeraiに予測を提出する方法

すぐにでもNumeraiに投稿したいという方は、大会参加者の[katsu1110さん](https://www.kaggle.com/code1110/numerai-tournament)や[Carlo Lepelaarsさん](https://www.kaggle.com/carlolepelaars/how-to-get-started-with-numerai)のKaggle Notebooks、および公式が発表している[Example script](https://github.com/numerai/example-scripts)がとても参考になります。

今回の記事では、上記の記事や公式のサンプルモデルから一歩踏み込んだ説明（コードでどこを改善するかなど）をします。本説明により提出プロセスがわかりやすくなり、大会の出場者数が増えることを願っています。

今回紹介したコードは、基本的にGoogle Colab上で実行できます。Runボタンを押すと投稿ファイルが作成されますので、ぜひ使ってみてください。

[Colabへのリンク](https://colab.research.google.com/drive/1b1Eik4skZUaR0Znx7je_OloqwKIlcbEl)

### コードを説明する前の基礎知識

#### i) Numeraiデータセットの構造

[データセットはNumeraiのAPIを通じてダウンロードできます](https://numer.ai/data/)。

train_int8.parquetはトレーニングデータを格納したcsvファイル、validation_int8.parquetは検証用データを格納したcsvファイルです。

![image](https://user-images.githubusercontent.com/78800304/120104183-31cd7f80-c18e-11eb-8ebc-1c03fcc095b4.png)

**id:** 暗号化された株のラベル

**era:** データが収集された期間のことです。eraが同じであれば、同じ期間にデータが収集されたことを意味します。

**feature:** ビン化した特徴量。特徴量は5段階にビン化されています。

**target:** ビン化された教師データ。また、ターゲットも5段階にビン化されています。

#### ii）データ提出までの流れ

1. データ読み込み

2. 特徴量エンジニアリング

3. 機械学習

4. モデルの強さについて

5. 予測結果が書き込まれたcsvファイルの作成

6. 中和の方法

### 2A.データ読み込み

`pd.read_parquet("train.parquet")` で読み込むことができます。

```python
!pip install -Uqq numerapi

import json
import numerapi
import pandas as pd
from contextlib import redirect_stderr

napi = numerapi.NumerAPI()
# Notebook実行時に大量に出力がでてしまうため抑制
with redirect_stderr(open(os.devnull, 'w')):
    napi.download_dataset("v4.2/train_int8.parquet", "train.parquet")
    napi.download_dataset("v4.2/live_int8.parquet", "live.parquet")
    napi.download_dataset("v4.2/features.json", "features.json")

# 特徴量の選択（今回はmedium特徴量を選択）
feature_set_name = "medium"
feature_metadata = json.load(open("features.json"))
feature_cols = feature_metadata["feature_sets"][feature_set_name]
targets = ["target"]

# データの読み込み
train = pd.read_parquet("train.parquet", columns=feature_cols+targets).dropna()

```

## 2B.特徴量エンジニアリング

Numeraiデータセットの特徴量は互いに相関が低く、特徴量エンジニアリングを行わなくてもある程度の結果が得られます。

まず、訓練データを見てみると、大まかにいくつかの種類の特徴量があることがわかります。

これらの特徴の平均値、偏差値、歪度などは有用な特徴です。

```python
# v4.2のデータで確認
# small 42
# medium 583
# all 2132
# v2_equivalent_features 304
# v3_equivalent_features 1000
# fncv3_features 400
# intelligence 35
# charisma 290
# strength 135
# dexterity 51
# constitution 335
# wisdom 140
# agility 145
# serenity 95
# sunshine 325
# rain 666
feature_metadata = json.load(open("features.json"))
for k, v in feature_metadata["feature_sets"].items():
    print(k, len(v))

def get_group_stats() -> pd.DataFrame:
    df_out = pd.DataFrame()
    for group in ["intelligence", "wisdom", "charisma", "dexterity", "strength", "constitution"]:
        print(group)
        cols = feature_metadata["feature_sets"][group]
        train_cols = pd.read_parquet("train.parquet", columns=cols).dropna()
        print(train_cols.shape)
        train_cols[f"feature_{group}_mean"] = train_cols[cols].mean(axis=1)
        train_cols[f"feature_{group}_std"] = train_cols[cols].std(axis=1)
        train_cols[f"feature_{group}_skew"] = train_cols[cols].skew(axis=1)
        train_cols.drop(cols, axis=1, inplace=True)
        df_out = pd.concat([df_out, train_cols], axis=1)
    return df_out
train_stats = get_group_stats()
```

メモリに余裕のあるPCであれば、特徴量の差分データや多項式特徴量などを含めると、良い結果が得られます。Google Colabで実行するとクラッシュしてしまうので、コードのみ掲載します。

```python
from sklearn import preprocessing

# interaction計算する変数
cols = [
    feature_metadata["feature_sets"]["dexterity"][6],
    feature_metadata["feature_sets"]["charisma"][17],
    feature_metadata["feature_sets"]["charisma"][62],
    feature_metadata["feature_sets"]["dexterity"][13]   
]
targets = ["target"]

# データ読み込み
train = pd.read_parquet("train.parquet", columns=cols+targets).dropna()

# interactionを計算する
interactions = preprocessing.PolynomialFeatures(degree=2, interaction_only=True, include_bias=False)
interactions.fit(train[cols], train["target"])
train_interact = pd.DataFrame(interactions.transform(train[cols]), index=train.index).astype(np.int8)
train = pd.concat([train, train_interact],axis=1)
```

Kaggleで使われているような特徴量エンジニアリングがNumeraiでもそのまま使えるので、train、val、testのデータを加工ことで、良いCorrやSharpe ratioが得られると思います。Numeraiで良い結果を得るために必要な作業の一つが特徴量エンジニアリングであることに間違いはありません。

## 2C.機械学習 

Numeraiデータセットに機械学習を適用する際に考慮しなければならないのは

i) どのような機械学習手法を使用するか（LightGBM、XGBoost、ニューラルネットワークなど)

ii) どのようなハイパーパラメータを使用するか

iii) 予測結果をスタックするかどうか などです。

今回は、計算時間を考慮してLightGBMを使用します。訓練データ以外のid、era、data_typeは機械学習には必要ありません。残ったfeature_ ○○を説明変数として、targetを教師データとして学習します。学習したデータを用いて、valに含まれるValidationデータとLiveデータについても予測データを作成します。

i)～iii)を考慮すれば、Corr等の値が改善されるので、この部分もやりこみ要素の要素の一つです。


```python
import pickle
import pandas as pd
import lightgbm as lgb
from sklearn.model_selection import KFold

# データの読み込み
train = pd.read_parquet("train.parquet", columns=feature_cols+targets).dropna()

# 学習
cv = KFold(n_splits=3)
for fold, (trn_idx, val_idx) in enumerate(cv.split(train), start=1):
    trn_x = train.iloc[trn_idx, :][feature_cols].values
    trn_y = train.iloc[trn_idx, :][target].values
    val_x = train.iloc[val_idx, :][feature_cols].values
    val_y = train.iloc[val_idx, :][target].values
    model = lgb.LGBMRegressor(**params)
    model.fit(
        trn_x, trn_y,
        eval_set=[(val_x, val_y)],
        callbacks=[lgb.early_stopping(stopping_rounds=100, verbose=True)],
    )
    pickle.dump(model, open(f"model.lgb.fold_{fold}.pkl", 'wb'))
```

## 2D.モデルの強さについて 

spearman（numerai_corr）, numerai_sharpe, max_drawdownを計算して、Validationデータのモデルの強さを推定することができます。

spearman（numerai_corr）, numerai_sharpeは大きいほど良いです。

この中でも特にspearmanの値が大きい（0.025以上が目安）と良いモデルであるとみなせます。

(※Corrだけに注目すると、いろいろな問題が発生する可能性があります。Numeraiに詳しい方とは意見が分かれるところだと思いますが、初めて予測結果を提出する方向けの記事なので、このように表現させてください)

なお、用語の説明は以下の通りです。

**spearman（numerai_corr）：** Correlationの平均値。高ければ高いほど良い(参考は0.022～0.04)

**numerai_sharpe：** 平均リターンを標準偏差で割った比率。高ければ高いほど良い（目安は1以上）

**max_drawdown：** 最大資産から落ち込む最大値

## 2E.予測結果の準備 

中和用のファイルをsubmission_file.csvに書き込みます。このファイルにはidとpredictionのカラムが必要です。

```py
models = []

# 上で作成したpklを読み込む
for path in glob.glob(f"model.*.pkl"):
    models.append(pickle.load(open(path, "rb")))

# Live dataでテストを行う
live = pd.read_parquet("live.parquet")
preds_live = np.zeros(len(live))
    for model in models:
        preds_live += model.predict(live[feature_cols]) / len(models)
    live_features["prediction"] = preds_live
```

## 2F.中和の方法 

学習用データに含まれる特徴量やExample_model（Numeraiが公式に配布しているサンプルモデル）と自分のモデルを線形回帰させることで、それぞれの特徴量と予測結果の相関を下げつつ、シャープ比を向上させることができます。ただし、やりすぎるとCorrが大きく下がってしまうので、0.3～0.5くらいがいいと思います。どのようなモデルをどれだけ中和するかも一つの検討要素となります。（＊中和をしない、というのも選択肢の一つです）

以下では、学習用データに含まれる特徴量に対して中和を行います。得られたファイルをcsvとして出力し、NumeraiのホームページのUpload predictionsから提出すれば完了です。

```python
def predict(live_features: pd.DataFrame) -> pd.DataFrame:
    def neutralize(df, columns, neutralizers=[], proportion=1.0, normalize=True, era_col="era"):
        unique_eras = df[era_col].unique()
        computed = []
        for u in unique_eras:
            df_era = df[df[era_col] == u]
            scores = df_era[columns].values
            if normalize:
                scores2 = []
                for x in scores.T:
                    x = (st.rankdata(x, method='ordinal') - .5) / len(x)
                    x = st.norm.ppf(x)
                    scores2.append(x)
                scores = np.array(scores2).T
            exposures = df_era[neutralizers].values

            scores -= proportion * exposures.dot(
                np.linalg.pinv(exposures.astype(np.float32)).dot(scores.astype(np.float32)))
            scores /= scores.std(ddof=0)
            computed.append(scores)
        return pd.DataFrame(np.concatenate(computed),
                            columns=columns,
                            index=df.index)
    
    # main:    
    preds_live = np.zeros(len(live_features))
    for model in models:
        preds_live += model.predict(live_features[feature_cols]) / len(models)
    live_features["prediction"] = preds_live
    
    # Feature Neutralization
    # Ref: https://qiita.com/NT1123/items/6c0123e960ab43148eb1
    live_predictions = neutralize(
        live_features,
        columns=["prediction"], 
        neutralizers=feature_cols, 
        proportion=1.0,
        normalize=True,
        era_col='era'
    ).rank(pct=True, method="first")
    return live_predictions
models = []
for path in glob.glob(f"model.*.pkl"):
    models.append(pickle.load(open(path, "rb")))

# Live dataでテストを行う
live = pd.read_parquet("live.parquet")
live_sub = predict(live)
live_sub.to_csv("submission.csv")
```

## 3.モデル診断の読み方 

**以下に示す目安はあくまでも一例です。参考程度にとどめてください。事実、以下の指標が悪いものでも上位にランクされるモデルも存在します。**

**Sharpe Ratio：** Validationデータのシャープレシオは1以上が良い結果を得やすいです。

**CORR20v2:** ValidationデータのCorr平均値が0.025～程度であると良いです。

**FNCv3:** v3データの特徴量で中和した場合のCorr平均値（あまり参考になりません）

**Std. Dev.：** 各Eraの予測値とValidationデータの相関の標準偏差（あまり参考になりません）

**Feat. Exposure：** 特徴量の露出度。特徴量と予測結果のバランスの良さを示す指標です。小さければ小さいほど良いです。

**Max Drawdown：** -0.05以下を目安としましょう。

**Ex. Preds Corr：** サンプルモデルとの相関性；値はあまり気にする必要はないです。

---

# 4.新規参加者向けのTips

## Numeraiとコミュニティに関連する便利なリンク

* [RocketChat \#newUsers チャンネル](https://community.numer.ai/channel/newusers)に参加することでさらなるヒントやサポートを得られます！
* [Slack](https://t.co/a9i06PrSsN?amp=1) に参加することで、日本人参加者とコミュニケーションがとれます！
* データ分析、ヒント、チュートリアルに関する投稿は、[Numeraiフォーラム](https://forum.numer.ai/)をチェックしてください。

【初心者向け】

[@tit_BTCQASH](https://twitter.com/tit_BTCQASH):[NumeraiのHPの見方＋サブミット＋便利リンク集](https://qiita.com/tit_BTCQASH/items/366a2d1c273507dd4b8c)

【Numeraiに関する説明・HPの見方等】

[Numerai公式](https://numer.ai/tournament):[Numerai 日本語ドキュメント](https://jp.docs.numer.ai/)

[@blog_UKI](https://twitter.com/blog_uki):[機械学習による株価予測　はじめようNumerai](https://qiita.com/blog_UKI/items/fb401725288e58c92bd6)

[@blog_UKI](https://qiita.com/blog_UKI/items/469143fe6940f3148880):[Numeraiトーナメント　－伝統的クオンツと機械学習の融合－](https://qiita.com/blog_UKI/items/fb401725288e58c92bd6)

[@blog_UKI](https://twitter.com/blog_uki):[機械学習による株価予測　さがそうNumerai Signals](https://qiita.com/blog_UKI/items/adba89950c4f70c2167d)

[@blog_UKI](https://twitter.com/blog_uki):[機械学習による株価予測　さがそう 真のNumerai Signals](https://qiita.com/blog_UKI/items/6f044b41819f1f003426)

[@katsu1110](https://twitter.com/kk1110tt):[KagglerへのNumeraiのススメ](https://zenn.dev/katsu1110/articles/bb2b5cba9b04c9e30bfe)

[@developer_quant](https://twitter.com/developer_quant):[【ファイナンス機械学習】著者によるNumerai解説スライドを日本語でまとめてみる](https://quantcollege.net/financial-machine-learning-numerai)

[@Y_oHr_N](https://twitter.com/y_ohr_n):[Numeraiはいいぞ](https://speakerdeck.com/yohrn/an-encouragement-of-numerai)


【計算モデル関連】

[@katsu1110](https://twitter.com/kk1110tt):[Numerai tournamentベースライン](https://www.kaggle.com/code1110/numerai-tournament)

[@katsu1110](https://twitter.com/kk1110tt):[[numerai] MLP with KerasTuner Starter](https://www.kaggle.com/code1110/numerai-mlp-with-kerastuner-starter/notebook)

[@tit_BTCQASH](https://twitter.com/tit_BTCQASH):[Numeraiに上位20%以上のスコアがでる予測値を提出する方法](https://qiita.com/tit_BTCQASH/items/4b321f06f7fea9709e05)

[@habakan_f](https://twitter.com/habakan_f):[Numeraiトーナメントのデータを構築過程から分析してみる](https://zenn.dev/habakan/articles/how-to-generate-numerai-dataset)

【Corr,MMC関連】

[@blog_UKI](https://twitter.com/blog_uki):[NumeariトーナメントのValid Corrをちょびっとだけ上げる小技](https://qiita.com/blog_UKI/private/c71ec4d34624afaf1a2d)

[@kunigaku](https://twitter.com/kunigaku):[Numerai で Random Seed Average](https://zenn.dev/kunigaku/articles/914efe9855ad2d8f487b)

[@blog_UKI](https://twitter.com/blog_uki):[Numeraiトーナメント：直交化に関するテクニック
](https://qiita.com/blog_UKI/private/fbf4520278569db8b880)

[@katsu1110さん](https://twitter.com/kk1110tt):[[Numerai] 成功が約束された特徴量を試してみる](https://zenn.dev/katsu1110/articles/0d96b293b547e0)

【Era selection】

[@katsu1110](https://twitter.com/kk1110tt):[Metric learningでlive eraに近いeraを見つける](https://www.kaggle.com/code1110/numerai-metric-learning-and-live-era/notebook)

【feature neutralization】

[@yaaku](https://twitter.com/yaaku123):[[Numerai] 成功が約束された特徴量を試してみる](https://yaakublog.com/numerai-feature-neutralization)

【Era boost】

[@pegion_hole](https://twitter.com/pegion_hole):[Era Boost について](https://zenn.dev/ageonsen/articles/aab408111bf952)

【Numerai compute/Numerai api関連】

[@murenoha](https://twitter.com/murenoha):[Numerai APIとnumerapiライブラリのraw_queryメソッド
](https://qiita.com/murenoha/items/a64f4c6e473066b0ce22)

[@reo3313](https://twitter.com/reo3313):[Numerai-Computeのエラー対応
](https://reon777.com/2020/07/06/numerai-compute/)

[@tit_BTCQASH](https://twitter.com/tit_BTCQASH):[Numerai-cliを使って予測ファイルの提出を自動化する方法
](https://qiita.com/tit_BTCQASH/items/fbcc9271c0a8977ff216)

[@habakan_f](https://twitter.com/habakan_f):[Payoutの一定割合を各モデルにStakeするスクリプト](https://gist.github.com/habakan/943ec48cf4e6b27043e5f4c4562a7e2e)

【fireside chat】

[@katsu1110](https://twitter.com/kk1110tt):[Numerai 2021Q1炉端会議メモ](https://zenn.dev/katsu1110/articles/7cdf98af5d3b57)

[@katsu1110](https://twitter.com/kk1110tt):[Numerai 2020Q4炉端会議メモ](https://zenn.dev/katsu1110/articles/3fc47534cdc8c1807102)

[@katsu1110](https://twitter.com/kk1110tt):[Numerai Numerai 2021Q2炉端会議メモ](https://zenn.dev/katsu1110/articles/7ce69ccd5212fb)

[@katsu1110](https://twitter.com/kk1110tt):[Numerai Numerai 2021Q3炉端会議メモ](https://zenn.dev/katsu1110/articles/bba27e6f8ff8c0)

[@katsu1110](https://twitter.com/kk1110tt):[Numerai Numerai 2021Q4炉端会議メモ](https://zenn.dev/katsu1110/articles/d804efecba6a49)

[@katsu1110](https://twitter.com/kk1110tt):[Numerai Numerai 2022Q1炉端会議メモ](https://zenn.dev/katsu1110/articles/d461c8dea4024b)

【掲示板】

[【日本語】Numeaiについて雑談・質問](https://forum.numer.ai/t/numeai/1473/11)

[【日本語】Numeai　Slack](https://t.co/05yh6pPy4T?amp=1)


【Advent Calendar】

[@kunigaku](https://twitter.com/kunigaku):[Numerai Advent Calendar 2020](https://adventar.org/calendars/5031)

[@kunigaku](https://twitter.com/kunigaku):[Numerai Advent Calendar 2021](https://adventar.org/calendars/6226)

## Numeraiに関するチュートリアル \(＊英語版\)

[@SurajP](https://numer.ai/surajp):[Google Colabを使った簡単なガイド](https://medium.com/@parmarsuraj99/a-guide-to-the-hardest-data-science-tournament-on-the-planet-748f46e83690)

[@perfect\_fit](https://numer.ai/perfect_fit):[Kaggleカーネルを使ったチュートリアル](https://app.wandb.ai/carlolepelaars/numerai\_tutorial/reports/Build-the-World-s-Open-Hedge-Fund-by-Modeling-the-Stock-Market--VmlldzoxODU0NTQ)

[@perfect\_fit](https://numer.ai/perfect_fit):[Kaggleカーネルを使ったチュートリアル②](https://www.kaggle.com/carlolepelaars/how-to-get-started-with-numerai)

[@MesozoicMetallurgist](https://numer.ai/mesozoicmetallurgist):[MesozoicMetallurgist Numerai Model List
](https://docs.google.com/document/d/19P_e8ahJUr6HbaOfFAmJSLXcXZWgzSj3lf_zyecBatM/edit)


