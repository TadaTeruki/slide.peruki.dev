---
marp: true
theme: peru24lab
title: 論文紹介 Scenario Superposition Method for Real-Time Tsunami Prediction Using a Bayesian Approach
description: Scenario Superposition Method for Real-Time Tsunami Prediction Using a Bayesian Approach
math: mathjax
author: Teruki TADA
session: 研究室活動
date: 2025-04-15
tags: 研究室活動
thumbnail: img/rumoi.webp
paginate: true
---

# 論文紹介: Scenario Superposition Method for Real-Time Tsunami Prediction Using a Bayesian Approach

発表者: 多田 瑛貴
(公立はこだて未来大学 複雑系知能学科 複雑系コース)

2025年4月15日 島内研究室

![bg right:20%](img/rumoi.webp)

---

## 書誌情報

**Scenario Superposition Method for Real-Time Tsunami Prediction Using a Bayesian Approach (2024)**

- DOI: 10.1029/2024JC021565
- 著者: Saneiki Fujita, Reika Nomura, Shuji Moriguchi, Yu Otake, Randall J. LeVeque, Kenjiro Terada
  - 全員が東北大学関連機関に所属
- 掲載誌: Journal of Geophysical Research: Oceans
  - アメリカ地球物理学連合 (AGU) が発行する査読つき学術雑誌
  Journal of Geophysical Research (JGR) のセッションの一つ

---

提案手法の実験にあたり、南海トラフ沖地震を想定した
津波シミュレーションのデータセットが作成され、全て公開されている
*詳細は後述。提案手法自体によるシミュレーション結果ではないことに注意*

**Pythonコード** DOI: 10.5281/zenodo.14029637.
**シミュレーションデータ** DOI: 10.5281/zenodo.12696848.

---

## 背景

津波の早期警報システムは、災害時の被害を軽減する重要な役割を果たす
津波の広がりや波高を予測するための計算が必要
*主に、流体現象のシミュレーション*

---

## 既存手法: 即時シミュレーション

津波の流体現象を支配方程式を用いて計算
- Oishi et al. (2015): K-computer/13498コア/5mメッシュ/約1.5分
- Musa et al. (2018): SX-ACE/512コア/10m(等)メッシュ/4分以内
*ドメイン領域やシミュレーション上での経過時間など実験設定が異なるため*
*ここで単純比較はできないことに注意。以降の手法も同様*

初期入力値による不確実性の考慮、計算コストと精度の兼ね合いが課題

観測データを用いてその結果を修正していく手法 (Assimilation) も存在
ただし、計算コストと精度の兼ね合いの課題は残る

- Wang et al. (2018): 14分で信頼性の高い到達予測を実現
*各Assimilationの計算時間は10秒以内でほぼ無視可能*

---

## 既存手法: データベース検索

津波のシミュレーション結果を事前に計算し、データベースとして保存
津波発生時には観測データに最も近いものを予測結果として参照

- Fauzi and Mizutani (2020): CNN+MLPによるシナリオ検索、1秒以内
*Open AccessではないためAbstractのみ参照。おそらく画像分類に近いアプローチ？*
- Nomura et al. (2022): ベイズ推定によるシナリオ検索

取り得るパターンを網羅する大量のシミュレーション結果が必要

---

## 既存手法: 機械学習

*WIP: もう少しちゃんと調べる*

観測データから予測結果を直接導出 (学習)

- Mulia et al. (2022): MLP
- Makinoshima et al. (2021), Rim et al. (2022): CNN

時系列予測

- Alan et al. (2023): LSTM

流体現象のシミュレーションに比べ高速な予測が可能、モデルの柔軟性もある

ブラックボックスで物理的な裏付けが乏しいほか
学習にかかる計算コストの考慮が必要であることが課題

---

## 既存手法: 確率的手法

*WIP: やる*

---

## 提案手法の概要

**シミュレーション結果の重ね合わせによる即時予測**

- 複数のシナリオによる
津波のシミュレーション結果を事前に用意
 *シナリオごとに想定する地震のパターンが異なる*
 *図は、あるシナリオでのシミュレーション結果の例*
 *図上: 断層すべり量の分布, 図下: 波高の分布*

 - 生成済みのシミュレーション結果を
複数重ね合わせ (線型結合し)
未知の地震パターンに対する津波の
シミュレーション結果を生成

![bg right:28% w:350](img/nankai_81_000255_slip_dtopo.webp)

---

重ね合わせに用いるシミュレーション結果への重みを
ベイズ推定を用いて確率分布の形式で導出
不確実性を考慮した予測を行う
*このアプローチ自体は、Nomura et al. (2022)で同様に行われている*
*ただし、こちらはあくまでデータベース検索のアプローチに基づく*

![w:500](img/fig-7.webp)

---

# Methodology

---

## 背景知識: 観測装置 (gauges) について

災害に関わる自然現象の観測網が日本各地に存在

- 海底に設置/地震計や水圧計など搭載/
地震・津波を対象
  - S-net: 太平洋沖
  - DONET (1,2): 南海トラフ沖
 - 沖合に設置/波高計など搭載/波浪を対象
   - NOWPHAS

*右図: S-netによる海底観測網*
*https://www.seafloor.bosai.go.jp/S-net/*

以降、説明に用いる「観測点」は
このような観測装置が存在する地点に対応

![bg right:30%](img/gauges-snet.webp)

---

## シナリオ重ね合わせ (Scenario Superposition)

シナリオ $j$ における観測点 ($N_g$個) ・時間 ($N_t$ステップ) ごとの
波高データを次のように表す ($\mathbf{x}$ は$N_g$次元のベクトル):

$$
X_j = \left[ \mathbf{x}^j_{t_1}, \mathbf{x}^j_{t_2}, \cdots, \mathbf{x}^j_{t_{N_t}} \right] \in \mathbb{R}^{N_g \times N_t}
$$

同様に、観測器による観測データを次のように表す ($\mathbf{y}$ は$N_g$次元のベクトル):
$$
Y = \left[ \mathbf{y}_{t_1}, \mathbf{y}_{t_2}, \cdots, \mathbf{y}_{t_{N_t}} \right] \in \mathbb{R}^{N_g \times N_t}
$$

観測データを、事前に作成した$N_s$シナリオ分のシミュレーション結果を用いて
次のような線形結合で近似する → **目標: 各シナリオへの重み $\mathbf{w}\in \mathbb{R}^{N_s}$の導出**

$$Y = \sum_{j=1}^{N_s} w_j X_j$$

---

## 大まかな流れ

- Offline Phase: $X$を低ランク近似により次元圧縮
- Online Phase: 重み$\mathbf{w}$をベイズ推定により定める
---

## Offline Phase: $X$を低ランク近似により次元圧縮

特異値分解 (SVD) により、データの次元を$r$まで落とした$X$の低ランク近似$X_r$を導出:

$$X_r =  \Phi_r D_r V_r^{\mathrm{T}}$$

ここで、$\Phi_r$は時間に依存せず固定の値を取る *なぜそう言えるのかまでは追えませんでした*
時間$t$での$X_r$の各要素について、$D_r v_t^{j\mathrm{T}} = a_t^j$ とまとめ:

$$\mathbf{x}_t^j \approx \Phi_r D_r v_t^{j\mathrm{T}} = \Phi_r a_t^j$$

以上より、$\mathbf{y}_t$と$\mathbf{x}_t$ (=$\Phi_r a_t^j$)の関係は次のように表せる:

$$\mathbf{y}_t \approx \sum_{j=1}^{N_s} \Phi_r a^j_t w_j$$

---

**参考: 特異値分解**

データを以下のように分解 ($D$は対角行列で、一意に定まる):

$$X = \Phi D V^{\mathrm{T}}$$

各成分を、$D$が次のようになるよう並べ替える: *主成分は大きな特異値$\sigma$をとる*

$$
D = 
\begin{bmatrix}
\sigma_1 & 0 & \cdots & 0 \\
0 & \sigma_2 & \ddots & \vdots \\
\vdots & \ddots & \ddots & 0 \\
0 & \cdots & 0 & \sigma_{N}
\end{bmatrix},
\quad \text{where } \sigma_1 > \sigma_2 > \cdots > \sigma_{N}.
$$

$\sigma_{1:r}$以外の特異値を0とした$D_r$を用いて、$X$を近似する階数$r$の$X_r$を得る:
*$X_r$は (フロベニウスノルムに基づくと) 元のデータを十分に近似することが知られている*

$$X_r =  \Phi_r D_r V_r^{\mathrm{T}}$$

---

<!-- _class: smartblockquote -->

## Online Phase: 重み$\mathbf{w}$をベイズ推定により定める

> 目標とする$\mathbf{y}_t$と$\mathbf{x}_t$ (=$\Phi_r a_t^j$)の関係: $\mathbf{y}_t \approx \sum_{j=1}^{N_s} \Phi_r a^j_t w_j$

誤差$\varepsilon_t$を考慮し、次のように表す:
*$\varepsilon_t$は観測誤差や次元圧縮による情報欠落、シミュレーション自体の予測誤差など様々な要因を内包*

$$\mathbf{y}_t  \approx \sum_{j=1}^{N_s} \Phi_r a^j_t w_j + \varepsilon_t$$

---

${\varepsilon }_{t}\sim \mathcal{N}\left(\mathbf{0},\,{\boldsymbol{\Sigma }}_{\varepsilon }\right)$と仮定し、行列形式で以下のように表す:

$$\mathbf{y}_t = \Phi_r \mathbf{A}_t \mathbf{w} + \varepsilon_t$$

ただし
$${\boldsymbol{A}}_{t}=\left[\begin{array}{@{}cccc@{}}\hfill {a}_{t}^{j=1}\hfill & \hfill {a}_{t}^{j=2}\hfill & \hfill {\cdots}\hfill & \hfill {a}_{t}^{j={N}_{s}}\hfill \end{array}\right]\in {\mathbb{R}}^{r\times {N}_{s}}$$

$$\boldsymbol{w}={\left\{\begin{array}{@{}cccc@{}}\hfill {w}^{j=1}\hfill & \hfill {w}^{j=2}\hfill & \hfill {\cdots}\hfill & \hfill {w}^{j={N}_{s}}\hfill \end{array}\right\}}^{\mathrm{T}}\in {\mathbb{R}}^{{N}_{s}}$$

これは**ベイズ線形回帰**の標準的な形に落とし込まれている

