# Numerai Compute

## Introduction

Computeは、あなた自身のインフラストラクチャを使用して毎週のsubmission ワークフローを自動化するのに役立つフレームワークです。

[numerai-cli](https://github.com/numerai/numerai-cli) を使用してインフラストラクチャをprovision（提供）し、新しいトーナメントデータをlisten（待機）し、モデルを実行し、予測値をNumeraiにアップロードするサーバとして、事前にトレーニングされたモデルをデプロイします。

![](../.gitbook/assets/image%20%2816%29.png)

## Quick start

```text
pip3 install numerai-cli

mkdir example-numerai
cd example-numerai

# set up your compute node in AWS
numerai setup

# copy a python example model
numerai docker copy-example

# build the docker container and deploys it to AWS
numerai docker deploy

# trigger your compute node in AWS
numerai compute test-webhook

# watch the logs of the running compute node from AWS
numerai compute logs -f
```

## Timing

[アカウント設定](https://numer.ai/account)にwebhookのURLを追加すると、Numeraiは土曜日の19:00 UTC（日本時間で04:00）（ラウンド開始から1時間後）にwebhookを実行します。もし、日曜日の2:00 UTC（日本時間で11:00）までにあなたの投稿を正常に受信できなかった場合は、あなたのコンピュートジョブが失敗したようだという警告をメールでお知らせします。もし失敗した場合は、日曜日の19:00 UTC（日本時間で04:00）に再度compute webhookを起動し、もしまた失敗した場合は、月曜日の2:00 UTC（日本時間で11:00）に最終的なメールを送信します。

## Help <a id="getting-started"></a>

ステップバイステップの[チュートリアル](https://docs.numer.ai/help/compute-tutorial)に従うか、[YouTube](https://www.youtube.com/watch?v=YFgXMpQszpM)のビデオをご覧ください。 

[compute rocketchat channnel](https://community.numer.ai/channel/compute)で助けを求めてください。

