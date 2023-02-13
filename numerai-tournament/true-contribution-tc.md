# True Contribution (TC)

現在最先端のスコアリングとペイアウトの仕組み

## True Contribution とは？

真の貢献度（TC）とは、仮想ポートフォリオの全体的なリターンを増加させるために、ステークをどのように変更すべきかを表すスコアです。過去にはMMCなど様々な指標が使われていましたが、2022年10月現在はTCがメタモデルへの貢献を表す指標として使われています。

---

## TCはどのように計算されるのか？

まず、Numeraiがどのようにエンド・ツー・エンドで動作するかを説明する必要があります。以下の説明は、[Richard CraibのMedinumのpost](https://medium.com/numerai/alien-stock-market-intelligence-numerais-true-contribution-6bc7652bd6ac)から引用したものです。

1. Numeraiは、すべてのシグナルの賭け金加重平均を介して提出された予測を組み合わせ、Stake-Weighted Meta Model (SWMM) を作成します。自分のモデルに大量のNMRを賭けるデータサイエンティストは、Steak-Weighted Meta Modelでより大きなウェイトを持つことになります。

2. SWMMと数百のリスク制約（市場、国、セクターのリスク中立化など）は、オプティマイザーに入力されます。これにより、SWMMは現実的な仮想ポートフォリオに変換されます。

3. Numeraiは、そのポートフォリオの仮想的なリターンを観察し、賭け金に対する最適化されたポートフォリオのリターンの勾配を計算します。真の貢献度とは、SWMMを構成する各予測セットに対するこの勾配の大きさである。

4. Numeraiは、この勾配の大きさをスケーリングしたものをベースにユーザーに支払います。これは、ニューラルネットワークのアーキテクチャや勾配降下の考え方に似ています。

![Numeraiのポートフォリオ構築のエンドツーエンド図](https://1574901745-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-LmGruQ_-ZYj9XMQUd5x%2Fuploads%2FfTBIoG4lUsAEHJv3OoN7%2Ftc-e2e-signal-eval.png?alt=media&token=255301d3-84aa-4f59-80bd-06c1dd87bb61 "Numeraiのポートフォリオ構築のエンドツーエンド図")

これは、スタンフォード大学のスティーブン・ボイド、Facebook AIのブランドン・エイモスらが開発した新しい技術によって可能になりました（参照：[Differentiable Convex Optimization Layers](https://web.stanford.edu/~boyd/papers/pdf/diff_cvxpy.pdf)）。

[cvxpylayers](https://github.com/cvxgrp/cvxpylayers)を使うことで、cvxpyで定義された凸型ポートフォリオ最適化をPyTorchモデルのレイヤーとして取り込むことができます。これにより、最適化されたポートフォリオのリターンのステーク値に対する勾配を効率的に計算し、Numeraiに提出されたすべてのシグナルの真の寄与を決定することができます。

---

## TCを最適化する方法

私たちは、いくつかのメトリクスがTCの良い指標として機能するようであることを発見しました。現在では、FNCv3が現在最も優れています。Numeraiの研究者であるMichael Oliverも、[TCについて論じた記事](https://forum.numer.ai/t/true-contribution-details/5128)を書いています。
