## はじめに
 2015年に設立された[Numerai](https://numer.ai)は、毎週データサイエンスのトーナメントを開催しています。世界中のデータサイエンティストが、難読化されたデータを無料でダウンロードし、株式市場の予測モデルを構築することでトーナメントに参加できます。ダウンロードできるデータは難読化されたいるため、金融の知識がなくても参加することができます。<br>
 <br>
 参加者は、自分の予測に賭け金をかけることでトーナメントに参加できます。良い予測を提出すると、より多くの仮想通貨（[NMR](https://vimeo.com/205032211)）を得ることができ、悪い予測を提出すると、NMRを没収されます。<br>
<br>
 Numeraiは、[メタモデル](https://www.youtube.com/watch?v=dhJnt0N497c)と呼ばれる参加者のモデルを統合したモデルを構築し、得られたデータを自社のグローバル・エクイティ・ヘッジファンドの取引に反映させています。<br>
 参加者は、賭け金の有無にかかわらずトーナメントに参加することができますが、NumeraiはNMRがステークされたモデルのみを使用します。参加者は自分でデータを用意する必要はありませんが、チームから与えられたデータを最適化し、自分の予測を提出することが求められます。<br>

## 目次 <br>
1. Numeraiのホームページと用語集の読み方<br>
2. Numeraiに予測を提出する方法<br>
3. モデル診断の読み方<br>
4. Numeraiとコミュニティに関連する便利なリンク<br>
<br>

## 1. Numeraiのホームページと用語集の読み方 <br>
NumeraiのホームページのURLは、https://numer.ai/tournament です。<br>
<br>
**Numeraire（NMR）トークン:** Numeraireは[ERC-20ベースのトークン](https://www.coinbase.com/price/numeraire)で、Numeraiへのステーキングに使用されます。<br>
NMRは、Numeraiのトーナメントに参加したり、Numeraiに技術的な貢献をすることで獲得できます。NMRトークンは、Numeraiが構築されている[Erasure Protocol](https://erasure.world/)で使用することができます。現在、Erasureプロトコル上のアプリは、Numerai、Numerai Signals、Erasure Bayですが、プロトコルは誰でも構築できるようになっています。<br>
<br>
**Corr：** 提出された予測データとターゲットとの相関係数を表します。<br>
<br>
**MMC：** メタモデル貢献度（MMC）は、モデルの予測がNumeraiのメタモデルにとってどれだけ価値があるかを示します。非常に独創的な予測は、独創的でない予測よりも高いMMCを持ちます。MMCに関する詳細は[こちら](https://medium.com/numerai/a-new-data-science-competition-where-being-different-pays-251c2aecc40a)<br>
<br>
**FNC:** Feature neutral correlation （FNC）は、提出した予測データをNumeraiのすべての特徴量に対して中和した後の、ターゲットとの相関係数を表します。<br>
<br>
**Corr / MMC / FNC Rep:** Rep（評判）は、過去20ラウンドにおけるその指標の加重平均であり、リーダーボードでユーザーをランク付けするために使用されるものです。Repについての詳細は[こちら](https://docs.numer.ai/tournament/reputation)<br>
<br>
**ステーク** 自分のモデルの予測にどれだけ自信があるかを示すために、NMRをステーク（預入れ＋ロック）をします。良い予測を提出した場合、NMRを得ることができます。一方、悪い予測を提出した場合はNMRが没収されます。賭け金の最小値は3NMRです。ステークせずに参加して、自分のモデルがどのようなパフォーマンスを示すかを知ってから、ステークするかどうかを決めることができます。
<br>
**ペイアウト** 賭けたNMRに応じて受け取る報酬。毎週（1ラウンドは4週間）、賭け金の最大25％を獲得または没収されます。ステーキングとペイアウトについての詳細は[こちら](https://docs.numer.ai/tournament/staking-and-payouts)をご覧ください。
<br>

# ホームページ上部
![image](https://user-images.githubusercontent.com/78800304/120104122-eca94d80-c18d-11eb-8f06-d0128a2d7bb4.png)
<br>
**DOCS:** ルール、FAQ、新規ユーザーセクションを含むNumeraiの[ドキュメント](https://docs.numer.ai/)へのリンクです。<br>
<br>
**CHAT:** 告知、一般的な議論、データサイエンスなどのチャンネルを含むチャットスペースです。NumeraiチームはRocketChatに積極的に参加しており、プロフィールには`team`タグが付いています。チームメンバーは主に太平洋時間で活動しています。参加は[こちら](http://community.numer.ai/)から。<br>
<br>
**FORUM:** Numerai、データサイエンス、ステイク戦略などに関連する議論のためのスペースです。主にコミュニティ内での情報共有を目的としています。リンクは[こちら](https://forum.numer.ai/)です。<br>
<br>
**LEADERBOARD：** Numeraiに投稿された予測結果のランキングです。ステーク量、Rep、MMCなどでソート可能です。<br>
<br>
**アカウント:** 「ウォレット」「モデル」「設定」「ログアウト」の4つのリンクがあります。<br>
・ウォレット：NMRトークンの入金と出金が行えます。<br>
入金(deposit):ウォレットに登録されているアドレスにNMRトークンを送ることで入金できます。このアドレスに他のトークンを送ることはできません。<br>
出金(withdraw):NMRトークンを自分のNumeraiウォレット以外のアドレスに出金することができます。出金を依頼する前に、出金先の外部アドレスがNMR受け取りに適していることを確認してください。間違ったアドレスに送ったNMRは回収できません。<br>
<br>
![image](https://user-images.githubusercontent.com/78800304/120104136-fd59c380-c18d-11eb-9986-e510285a0b4b.png)
<br>
**モデル** このページでは、Numeraiに投稿するモデルを追加／削除できます。モデルの追加／削除をするには、「新しいモデルの追加」／「既存のアカウントの吸収」を押してください。
複数モデルのアカウントやアカウントの吸収については[こちら](https://forum.numer.ai/t/announcing-general-availability-of-multi-model-account-support-for-all-users/399)をご覧ください。<br>
<br>
![image](https://user-images.githubusercontent.com/78800304/120104142-08145880-c18e-11eb-8874-aa5533355ef5.png)
**設定：** Eメール、パスワード、2段階認証（2FA）、APIキーの設定を行います。<br>
アカウントがNMRを保持しているため、2FAによるセキュリティ強化を推奨します。2FAを使用する場合は、リカバリーコードを保存する必要があります。2FAのデバイスにアクセスできなくなっても、Numeraiはアカウントをリセットしません。<br>
<br>
![image](https://user-images.githubusercontent.com/78800304/120104152-119dc080-c18e-11eb-88ed-ada0e1b5f6d1.png)
<br>
# ホームページ下部
**モデル情報：** モデル（今回はTIT_BTCQASH）のランキングやRep、MMC Repなどの情報を掲載しています。↓のボタンでモデルを切り替えることができます。<br>
<br>
**データ情報:** 最新ラウンドのデータダウンロードリンクと、予測結果のアップロードリンクです。<br>
<br>
**ステーク:** NMRのステーク量を調整できます。ステーク方法には、CorrやCorr＋MMCなどの種類があります。例えば、Corrではターゲットとの相関関係のみにNMRを賭けることができ、Corr + MMCではターゲットとの相関関係とMMCにNMRを賭けることができます。<br>
<br>
**Pending Payouts:** 各ラウンドの予想ペイアウト（払い出し）の表です。<br>
<br>
![image](https://user-images.githubusercontent.com/78800304/120104161-1d898280-c18e-11eb-9c4f-9dce9efe0cc2.png)
<br>
# 2. Numeraiに予測を提出する方法<br>
すぐにでもNumeraiに投稿したいという方は、大会参加者の[katsu1110さん](https://www.kaggle.com/code1110/numerai-tournament)と[Carlo Lepelaarsさん](https://www.kaggle.com/carlolepelaars/how-to-get-started-with-numerai)のKaggle Notebooksがとても参考になります。<br>
今回の記事では、上記の記事や公式のサンプルモデルから一歩踏み込んだ説明（コードでどこを改善するかなど）をします。本説明により提出プロセスがわかりやすくなり、大会の出場者数が増えることを願っています。<br>
<br>
今回紹介したコードは、Google Colab上で実行できます。Runボタンを押すと投稿ファイルが作成されますので、ぜひ使ってみてください。<br>
<br>
[Colabへのリンク](https://colab.research.google.com/drive/1u5Cc3NlJQZJwJNmOrPjjqBchk928gT4C?usp=sharing)<br>
<br>
## コードを説明する前の基礎知識<br>
## i) Numeraiデータセットの構造<br>
データセットはダウンロードリンクからダウンロードできます。ファイルを解凍すると、numerai_training_data.csv、numerai_tournament_data.csvなどのファイルがあることがわかります。numerai_training_data.csvはトレーニングデータを格納したcsvファイル、numerai_tournament_data.csvは検証用データを格納したcsvファイルです。<br>
<br>
![image](https://user-images.githubusercontent.com/78800304/120104183-31cd7f80-c18e-11eb-8ebc-1c03fcc095b4.png)
<br>
**id:** 暗号化された株のラベル<br>
**era:** データが収集された期間のことです。eraが同じであれば、同じ期間にデータが収集されたことを意味します。<br>
**data_type:** データの種類。trainはトレーニング用のデータ、validationは検証用のデータ、testはテスト用のデータ、liveは現在のラウンドのデータです。<br>
**feature:** ビン化した特徴量。特徴量は0,0.25,0.5,0.75,1の5段階にビン化されています。また、特徴量は、次のようなラベルの付いたグループに分かれています。<br>
"feature_intelligence"、"feature_wisdom"、"feature_charisma"、"feature_dexterity"、"feature_strength"、"feature_constitution"<br>
**target:** ビン化された教師データ。また、ターゲットも0,0.25,0.5,0.75,1の5段階にビン化されています。numerai_training_data.csvではターゲットデータが与えられていますが、numerai_tournament_data.csvのテストデータとライブデータではNaNとなっています。<br>
<br>
## ii）データ提出までの流れ<br>
1. データ読み込み<br>
2. 特徴量エンジニアリング<br>
3. 機械学習<br>
4. モデルの強さについて<br>
5. 予測結果が書き込まれたcsvファイルの作成<br>
6. 中和の方法<br>
<br>

## 2A.データ読み込み <br>
Carlo Lepelaars氏の記事から、データ読み込みの部分を引用（一部編集）します。<br>
download_current_data (DIR)を呼び出し、最新のデータをDIRで指定したディレクトリにダウンロード後、train, val, test = load_data (DIR, reduce_memory = True)を呼び出すと、train, val, testのデータを別々に保存できます。<br>
<br>
<br>
```
!pip install numerapi
import numerapi
NAPI = numerapi.NumerAPI(verbosity="info")
import numpy as np
import random as rn
import pandas as pd
import seaborn as sns
import lightgbm as lgb
import matplotlib.pyplot as plt
from scipy.stats import spearmanr, pearsonr
from sklearn.metrics import mean_absolute_error
import os

DIR = "/kaggle/working"
def download_current_data(directory: str):
        """
        Downloads the data for the current round
        :param directory: The path to the directory where the data needs to be saved
        """
        current_round = NAPI.get_current_round()
        if os.path.isdir(f'{directory}/numerai_dataset_{current_round}/'):
            print(f"You already have the newest data! Current round is: {current_round}")
        else:
            print(f"Downloading new data for round: {current_round}!")
            NAPI.download_current_dataset(dest_path=directory, unzip=True)

def load_data(directory: str, reduce_memory: bool=True) -> tuple:
        """
        Get data for current round
        :param directory: The path to the directory where the data needs to be saved
        :return: A tuple containing the datasets
        """
        print('Loading the data')
        full_path = f'{directory}/numerai_dataset_{NAPI.get_current_round()}/'
        train_path = full_path + 'numerai_training_data.csv'
        test_path = full_path + 'numerai_tournament_data.csv'
        train = pd.read_csv(train_path)
        test = pd.read_csv(test_path)
        # Reduce all features to 32-bit floats
        if reduce_memory:
            num_features = [f for f in train.columns if f.startswith("feature")]
            train[num_features] = train[num_features].astype(np.float32)
            test[num_features] = test[num_features].astype(np.float32)
        val = test[test['data_type'] == 'validation']
        test = test[test['data_type'] != 'validation']
        return train, val, test
    # Download, unzip and load data
download_current_data(DIR)
train, val, test = load_data(DIR, reduce_memory=True)
```
<br>

## 2B.特徴量エンジニアリング<br>
Numeraiデータセットの特徴量は互いに相関が低く、特徴量エンジニアリングを行わなくてもある程度の結果が得られます。<br>
まず、訓練データを見てみると、大まかに6種類に分かれていることがわかります。<br>
（"feature_intelligence"、"feature_wisdom"、"feature_charisma"、"feature_dexterity"、"feature_strength"、"feature_constitution "）
Carlo Lepelaars氏の論文からコードを引用しましたが、これらの特徴の平均値、偏差値、歪度などは有用な特徴です。<br>
したがって、train = get_group_stats (train)を呼び出して、これらの特徴をtrainデータに追加します。<br>
<br>
```
def get_group_stats(df: pd.DataFrame) -> pd.DataFrame:
        for group in ["intelligence", "wisdom", "charisma", "dexterity", "strength", "constitution"]:
            cols = [col for col in df.columns if group in col]
            df[f"feature_{group}_mean"] = df[cols].mean(axis=1)
            df[f"feature_{group}_std"] = df[cols].std(axis=1)
            df[f"feature_{group}_skew"] = df[cols].skew(axis=1)
        return df
train = get_group_stats(train)
val = get_group_stats(val)
test = get_group_stats(test)
```
<br>
メモリに余裕のあるPCであれば、特徴量の差分データや多項式特徴量などを含めると、良い結果が得られます。Google Colabで実行するとクラッシュしてしまうので、コードのみ掲載します。メモリ使用量を軽減する方法については、[フォーラム](https://forum.numer.ai/t/reducing-memory/313)で議論されています。<br>

```
from sklearn import preprocessing
ft_corr_list=['feature_dexterity7', 'feature_charisma18', 'feature_charisma63', 'feature_dexterity14']#Please try other features!
interactions = preprocessing.PolynomialFeatures(degree=2, interaction_only=True, include_bias=False)

interactions.fit(train[ft_corr_list], train["target"])

X_train_interact = pd.DataFrame(interactions.transform(train[ft_corr_list]))
X_best_val_inter =pd.DataFrame(interactions.transform(val[ft_corr_list]))
X_best_test_inter =pd.DataFrame(interactions.transform(test[ft_corr_list]))

train=pd.concat([train,X_train_interact],axis=1)

val=val.reset_index().drop(columns='index')
val=pd.concat([val,X_best_val_inter],axis=1)

test=test.reset_index().drop(columns='index')
test=pd.concat([test,X_best_test_inter],axis=1)
```
<br>
Kaggleで使われているような特徴量エンジニアリングがNumeraiでもそのまま使えるので、train、val、testのデータを加工ことで、良いCorrやSharpe ratioが得られると思います。Numeraiで良い結果を得るために必要な作業の一つが特徴量エンジニアリングであることに間違いはありません。<br>
<br>

## 2C.機械学習 <br>

Numeraiデータセットに機械学習を適用する際に考慮しなければならないのは<br>
i) どのような機械学習手法を使用するか（LightGBM、XGBoost、ニューラルネットワークなど)<br>
ii) どのようなハイパーパラメータを使用するか<br>
iii) 予測結果をスタックするかどうか などです。<br>
今回は、計算時間を考慮してLightGBMを使用します。訓練データ以外のid、era、data_typeは機械学習には必要ありません。残ったfeature_ ○○を説明変数として、targetを教師データとして学習します。学習したデータを用いて、valに含まれるValidationデータとLiveデータについても予測データを作成します。<br>
i)～iii)を考慮すれば、Corr等の値が改善されるので、この部分もやりこみ要素の要素の一つです。<br>
<br>
```
feature_list = train.columns.drop(['id','era','data_type','target'])
dtrain = lgb.Dataset(train[feature_list].fillna(0), label=train["target"])
dvalid = lgb.Dataset(val[feature_list].fillna(0), label=val["target"])

best_config ={"objective":"regression", "num_leaves":31,"learning_rate":0.01,"n_estimators":2000,"max_depth":5,"metric":"mse","verbosity": 10, "random_state": 0} 

model = lgb.train(best_config, dtrain)

train.loc[:, "prediction"] = model.predict(train[feature_list])

val.loc[:,"prediction"]=val["target"]
val.loc[:,"prediction"] = model.predict(val[feature_list])
```

## 2D.モデルの強さについて <br>

spearman, payout, numerai_sharpe, maeを計算して、Validationデータのモデルの強さを推定することができます。<br>spearman,payout,numerai_sharpeは大きいほど良いです。<br>
この中でも特にspearmanの値が大きい（0.025以上が目安）と良いモデルであるとみなせます。<br>
<br>
(※Corrだけに注目すると、いろいろな問題が発生する可能性があります。Numeraiに詳しい方とは意見が分かれるところだと思いますが、初めて予測結果を提出する方向けの記事なので、このように表現させてください)<br>
<br>
なお、用語の説明は以下の通りです。<br>
**spearman：** Correlationの平均値。高ければ高いほど良い(参考は0.022～0.04)<br>
**ペイアウト** 平均リターン<br>
**numerai_sharpe：** 平均リターンを標準偏差で割った比率。高ければ高いほど良い（目安は1以上）<br>
**mae：** 平均絶対誤差<br>
<br>

```
def sharpe_ratio(corrs: pd.Series) -> np.float32:
        """
        Calculate the Sharpe ratio for Numerai by using grouped per-era data

        :param corrs: A Pandas Series containing the Spearman correlations for each era
        :return: A float denoting the Sharpe ratio of your predictions.
        """
        return corrs.mean() / corrs.std()


def evaluate(df: pd.DataFrame) -> tuple:
        """
        Evaluate and display relevant metrics for Numerai 

        :param df: A Pandas DataFrame containing the columns "era", "target" and a column for predictions
        :param pred_col: The column where the predictions are stored
        :return: A tuple of float containing the metrics
        """
        def _score(sub_df: pd.DataFrame) -> np.float32:
            """Calculates Spearman correlation"""
            return spearmanr(sub_df["target"], sub_df["prediction"])[0]

        # Calculate metrics
        corrs = df.groupby("era").apply(_score)
        print(corrs)
        payout_raw = (corrs / 0.2).clip(-1, 1)
        spearman = round(corrs.mean(), 4)

        payout = round(payout_raw.mean(), 4)
        numerai_sharpe = round(sharpe_ratio(corrs), 4)
        mae = mean_absolute_error(df["target"], df["prediction"]).round(4)

        # Display metrics
        print(f"Spearman Correlation: {spearman}")
        print(f"Average Payout: {payout}")
        print(f"Sharpe Ratio: {numerai_sharpe}")
        print(f"Mean Absolute Error (MAE): {mae}")
        return spearman, payout, numerai_sharpe, mae
        
feature_spearman_val = [spearmanr(val["prediction"], val[f])[0] for f in feature_list]
feature_exposure_val = np.std(feature_spearman_val).round(4)
spearman, payout, numerai_sharpe, mae = evaluate(val)
```

<br>

## 2E.予測結果が書き込まれたcsvファイルの準備 <br>
中和用のファイルをsubmission_file.csvに書き込みます。このファイルにはidとpredictionのカラムが必要です。また、idはValidationデータ、testデータ（＋Liveデータ）の順であることが必要です。順番が違うとNumerai側でリジェクトされますのでご注意ください。
<br>

```
test.loc[:, "prediction"] =0
test.loc[:, "prediction"] = model.predict(test[feature_list])
test[['id', "prediction"]].to_csv("submission_test.csv", index=False)

val[['id', "prediction"]].to_csv("submission_val.csv", index=False)

test=0
val=0

directory = "/kaggle/working"
full_path = f'{directory}/numerai_dataset_{NAPI.get_current_round()}/'

test_path = full_path + 'numerai_tournament_data.csv'

tournament_data = pd.read_csv(test_path)
tournament_data_id=tournament_data['id']
tournament_data_id2=tournament_data['feature_dexterity7']
tournament_data_id=pd.concat([tournament_data_id,tournament_data_id2],axis=1)

val=pd.read_csv("submission_val.csv")
test=pd.read_csv("submission_test.csv")

test_val_concat=pd.concat([val[['id', "prediction"]],test[['id', "prediction"]]],axis=0).set_index('id')
tournament_data_id=tournament_data_id.set_index('id')

conc_submit=pd.concat([tournament_data_id,test_val_concat],axis=1).drop(columns='feature_dexterity7').reset_index()
conc_submit=conc_submit.rename(columns={'index': 'id'})
conc_submit.to_csv("submission_file"+".csv", index=False)
```

## 2F.中和の方法 <br>
Example_model（Numeraiが公式に配布しているサンプルモデル）と自分のモデルを線形回帰させることで、それぞれの特徴量と予測結果の相関を下げつつ、シャープ比を向上させることができます。ただし、やりすぎるとCorrが大きく下がってしまうので、0.3～0.5くらいがいいと思います。どのようなモデルをどれだけ中和するかも一つの検討要素となります。（＊中和をしない、というのも選択肢の一つです）
得られたneutralized_submission_file.csvを、NumeraiのホームページのUpload predictionsから提出すれば完了です。

```
def neutralize(series,by, proportion):
    scores = series.values.reshape(-1, 1)
    exposures = by.values.reshape(-1, 1)
    exposures = np.hstack((exposures, np.array([np.mean(series)] * len(exposures)).reshape(-1, 1)))
    correction = proportion * (exposures.dot(np.linalg.lstsq(exposures, scores)[0]))
    corrected_scores = scores - correction
    neutralized = pd.Series(corrected_scores.ravel(), index=series.index)
    return neutralized
    
by=pd.read_csv('/kaggle/working/numerai_dataset_'+str(NAPI.get_current_round())+'/example_predictions.csv')

neut=pd.read_csv("submission_file.csv")
neut=pd.DataFrame({'prediction':neutralize(neut['prediction'],by['prediction'], 0.3)})

conc=pd.concat([by.drop(columns="prediction"),neut],axis=1)
conc.to_csv("neutralized_submission_file.csv", index=False)#submission file
```

## 3.モデル診断の読み方 <br>

**以下に示す目安はあくまでも一例です。参考程度にとどめてください。事実、以下の指標が悪いものでも上位にランクされるモデルも存在します。**<br>
<br>
**Validation Sharpe：** Validationデータのシャープレシオは1以上が良い結果を得やすいです。<br>
**Validation Mean:** ValidationデータのCorr平均値が0.025～程度であると良いです。<br>
**Feature Neutral Mean:** 全ての特徴量で中和した場合のCorr平均値（あまり参考になりません）<br>
**Validation SD：** 各Eraの予測値とValidationデータの相関の標準偏差（あまり参考になりません）<br>
**Feature Exposure：** 特徴量の露出度。特徴量と予測結果のバランスの良さを示す指標です。小さければ小さいほど良いです。<br>
**Max Drawdown** -0.05以下を目安としましょう。<br>
**Corr + MMC Sharpe：** CorrとMMCの合算シャープレシオ<br>
**MMC mean：** MMCの平均値<br>
**Corr with Example Preds：** サンプルモデルとの相関性 0.5～0.8が目安です。<br>


# 4.新規参加者向けのTips<br>
#### Numeraiとコミュニティに関連する便利なリンク<br>

* [RocketChat \#newUsers チャンネル](https://community.numer.ai/channel/newusers)に参加することでさらなるヒントやサポートを得られます！
* [Slack](https://t.co/a9i06PrSsN?amp=1) に参加することで、日本人参加者とコミュニケーションがとれます！
* データ分析、ヒント、チュートリアルに関する投稿は、[Numeraiフォーラム](https://forum.numer.ai/)をチェックしてください。

【初心者向け】<br>
[@tit_BTCQASH](https://twitter.com/tit_BTCQASH):[NumeraiのHPの見方＋サブミット＋便利リンク集](https://qiita.com/tit_BTCQASH/items/366a2d1c273507dd4b8c)<br>


【Numeraiに関する説明・HPの見方等】<br>
[Numerai公式](https://numer.ai/tournament):[Numerai 日本語ドキュメント](https://jp.docs.numer.ai/)<br>
[@blog_UKI](https://twitter.com/blog_uki):[機械学習による株価予測　はじめようNumerai](https://qiita.com/blog_UKI/items/fb401725288e58c92bd6)<br>
[@blog_UKI](https://qiita.com/blog_UKI/items/469143fe6940f3148880):[Numeraiトーナメント　－伝統的クオンツと機械学習の融合－](https://qiita.com/blog_UKI/items/fb401725288e58c92bd6)<br>
[@blog_UKI](https://twitter.com/blog_uki):[機械学習による株価予測　さがそうNumerai Signals](https://qiita.com/blog_UKI/items/adba89950c4f70c2167d)<br>
[@blog_UKI](https://twitter.com/blog_uki):[機械学習による株価予測　さがそう 真のNumerai Signals](https://qiita.com/blog_UKI/items/6f044b41819f1f003426)<br>
[@katsu1110](https://twitter.com/kk1110tt):[KagglerへのNumeraiのススメ](https://zenn.dev/katsu1110/articles/bb2b5cba9b04c9e30bfe)<br>
[@developer_quant](https://twitter.com/developer_quant
):[【ファイナンス機械学習】著者によるNumerai解説スライドを日本語でまとめてみる](https://quantcollege.net/financial-machine-learning-numerai
[@Y_oHr_N](https://twitter.com/y_ohr_n):[Numeraiはいいぞ](https://speakerdeck.com/yohrn/an-encouragement-of-numerai)<br>
)<br>

【計算モデル関連】<br>
[@katsu1110](https://twitter.com/kk1110tt):[Numerai tournamentベースライン](https://www.kaggle.com/code1110/numerai-tournament)<br>
[@katsu1110](https://twitter.com/kk1110tt):[[numerai] MLP with KerasTuner Starter](https://www.kaggle.com/code1110/numerai-mlp-with-kerastuner-starter/notebook)<br>
[@tit_BTCQASH](https://twitter.com/tit_BTCQASH):[Numeraiに上位20%以上のスコアがでる予測値を提出する方法
](https://qiita.com/tit_BTCQASH/items/4b321f06f7fea9709e05)<br>

【Corr,MMC関連】<br>
[@blog_UKI](https://twitter.com/blog_uki):[NumeariトーナメントのValid Corrをちょびっとだけ上げる小技](https://qiita.com/blog_UKI/private/c71ec4d34624afaf1a2d)<br>
[@kunigaku](https://twitter.com/kunigaku):[Numerai で Random Seed Average](https://zenn.dev/kunigaku/articles/914efe9855ad2d8f487b)<br>
[@blog_UKI](https://twitter.com/blog_uki):[Numeraiトーナメント：直交化に関するテクニック
](https://qiita.com/blog_UKI/private/fbf4520278569db8b880)[@katsu1110さん](https://twitter.com/kk1110tt):[[Numerai] 成功が約束された特徴量を試してみる
](https://zenn.dev/katsu1110/articles/0d96b293b547e0)<br>

【Era selection】<br>
[@katsu1110](https://twitter.com/kk1110tt):[Metric learningでlive eraに近いeraを見つける
](https://www.kaggle.com/code1110/numerai-metric-learning-and-live-era/notebook)<br>


【feature neutralization】<br>
[@yaaku](https://twitter.com/yaaku123):[[Numerai] 成功が約束された特徴量を試してみる
](https://yaakublog.com/numerai-feature-neutralization)<br>

【Era boost】<br>
[@pegion_hole](https://twitter.com/pegion_hole):[Era Boost について
](https://zenn.dev/ageonsen/articles/aab408111bf952)<br>

【Numerai compute/Numerai api関連】<br>
[@murenoha](https://twitter.com/murenoha):[Numerai APIとnumerapiライブラリのraw_queryメソッド
](https://qiita.com/murenoha/items/a64f4c6e473066b0ce22)<br>
[@reo3313](https://twitter.com/reo3313):[Numerai-Computeのエラー対応
](https://reon777.com/2020/07/06/numerai-compute/)<br>
[@tit_BTCQASH](https://twitter.com/tit_BTCQASH):[Numerai-cliを使って予測ファイルの提出を自動化する方法
](https://qiita.com/tit_BTCQASH/items/fbcc9271c0a8977ff216)<br>

【fireside chat】<br>
[@katsu1110](https://twitter.com/kk1110tt):[Numerai 2021Q1炉端会議メモ
](https://zenn.dev/katsu1110/articles/7cdf98af5d3b57)<br>
[@katsu1110](https://twitter.com/kk1110tt):[Numerai 2020Q4炉端会議メモ
](https://zenn.dev/katsu1110/articles/3fc47534cdc8c1807102)<br>
[@katsu1110](https://twitter.com/kk1110tt):[Numerai Numerai 2021Q2炉端会議メモ
](https://zenn.dev/katsu1110/articles/7ce69ccd5212fb)<br>

【掲示板】<br>
[【日本語】Numeaiについて雑談・質問](https://forum.numer.ai/t/numeai/1473/11
)<br>
[【日本語】Numeai　Slack](https://t.co/05yh6pPy4T?amp=1)<br>

【Advent Calendar】<br>
[@kunigaku](https://twitter.com/kunigaku):[Numerai Advent Calendar 2020](https://adventar.org/calendars/5031
)<br>


#### Numeraiに関するチュートリアル \(＊英語版\)
[Numerai notebook](https://numer.ai/submit)<br>
[@SurajP](https://numer.ai/surajp):[Google Colabを使った簡単なガイド](https://medium.com/@parmarsuraj99/a-guide-to-the-hardest-data-science-tournament-on-the-planet-748f46e83690)<br>
[@perfect\_fit](https://numer.ai/perfect_fit):[Kaggleカーネルを使ったチュートリアル](https://app.wandb.ai/carlolepelaars/numerai\_tutorial/reports/Build-the-World-s-Open-Hedge-Fund-by-Modeling-the-Stock-Market--VmlldzoxODU0NTQ)<br>
[@perfect\_fit](https://numer.ai/perfect_fit):[Kaggleカーネルを使ったチュートリアル②](https://www.kaggle.com/carlolepelaars/how-to-get-started-with-numerai)<br>
[@MesozoicMetallurgist](https://numer.ai/mesozoicmetallurgist):[MesozoicMetallurgist Numerai Model List
](https://docs.google.com/document/d/19P_e8ahJUr6HbaOfFAmJSLXcXZWgzSj3lf_zyecBatM/edit)


