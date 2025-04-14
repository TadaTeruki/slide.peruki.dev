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

ブラックボックスで物理的な裏付けが乏しく
学習時の計算コストの考慮が必要であることが課題

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

 - 生成済みのシミュレーション結果を複数重ね合わせ
未知の地震パターンに対する津波の
シミュレーション結果を生成

![bg right:28% w:350](img/nankai_81_000255_slip_dtopo.webp)

---

