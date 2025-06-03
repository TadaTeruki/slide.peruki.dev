---
marp: false
theme: peru24lab
title: Physics Informed Newral Networks for tsunami inundation modeling
description: Physics Informed Newral Networks for tsunami inundation modeling
math: mathjax
author: Teruki TADA
session: 研究室活動
date: 2025-06-02
tags: 研究室活動
thumbnail: img/himeji.webp
paginate: true
---

# 論文紹介: Physics Informed Newral Networks for tsunami inundation modeling

島内研究室 2025年6月2日 輪読会

発表者: 多田 瑛貴
(公立はこだて未来大学 複雑系知能学科 複雑系コース)

---

# 書誌情報

**Physics Informed Newral Networks for tsunami inundation modeling**
著者: Rüdiger Brecht, Elsa Cardoso-Bihlo, Alex Bihlo
arXiv:2406.16236v1 (https://arxiv.org/abs/2406.16236v1)

2024年7月23日発表

---

# Introduction

第2章 関連研究の内容とあわせて言及します

---

## 津波のモデリング

津波のモデリングにおける課題
- データの収集
- (?) 固体と流体の相互作用に関する十分な理解の不足
- 長期にわたる断層滑りの過程の不確実性

津波の様々な要因
- **物理的パラメータ** (海底地形、断層滑り量...) の考慮が必要
- (?) 海底地震における、地盤の変位・水柱へのエネルギー伝達の問題との関連性
- 火山噴火や隕石衝突といったより空間スケールの小さい場合のモデリング

---

## 津波の数値解析

様々な波動力学の支配方程式と離散化手法が用いられた

- 差分法
- 有限要素法・不連続ガラーキン法
- メッシュレスなアプローチ

これらを用いて以下の支配方程式を解く

- **Shallow-water equations** (浅水方程式)
- Boussinesq equations
- Serre–Green–Naghdi equations
- Navier–Stokes equations 

検討されているアプローチのほとんどは上記に基づく

---

## データ駆動型アプローチ

近年は、機械学習などデータ駆動型アプローチへの移行がみられている

- 関心のある関係性をモデル化
  - 外洋の水位変位と特定の地点における遡上との関係
  - 低解像度・高解像度シミュレーションの関係 (→ 超解像？)
- (一度学習すれば) 即時の計算が可能

--- 

## 科学技術機械学習 (Scientific machine learning)

微分方程式や物理的な性質(対称性・保存則)といったで与えられる帰納バイアスを
機械学習ベースのアルゴリズムに組み込む

**Physics-informed neural networks (PINNs)** は特に注目を集める
他の数値計算同様に微分方程式を直接解く・メッシュレス・逆問題に応用可能

---

PINNsには課題も存在:
- 長い時間間隔での解を得るのが難しい
- 学習時間が長く、即時予測では適用が困難になる場合がある

幾つかの軽減策も見られている
- Multi-model approaches
- Improved training and optimization strategies
- Preservation of geometric properties
- **Operator learning techniques** (Physics-informed DeepONetsなど)

---

## 本論文の内容

- **Physics-informed neural networks**と**Physics-informed DeepONets**の説明
- 浅水方程式に上記のアプローチを取り入れるためのフレームワークと性能評価

---

# A primer on physics-informed neural networks

---

$\Omega = [0, t_f] \times \Omega_s$, where $\Omega_s \subset \mathbb{R}^d$ として

$$
\begin{aligned}
\Delta_l(t, \mathbf{x}, \mathbf{u}^{(n)}) &= 0, \quad l = 1, \dots, L, \quad t \in [0, t_f], \mathbf{x} \in \Omega,\\
\mathcal{I}_{l_i}(\mathbf{x}, \mathbf{u}^{(n_i)}\vert_{t=0}) &= 0, \quad l_i = 1, \dots, L_i, \quad \mathbf{x} \in \Omega,\\
\mathcal{B}_{l_b}(t, \mathbf{x}, \mathbf{u}^{(n_b)}) &= 0, \quad l_b = 1, \dots, L_b, \quad t \in [0, t_f], \mathbf{x} \in \partial \Omega,
\end{aligned}
\tag{1}
$$

- $t$: 時間変数
- $\mathbf{x} = (x_1, \dots, x_d)$: 空間独立変数
- $\mathbf{u} = (u_1, \dots, u_q)$: ...

---

# Physics-informed neural networks for the shallow-water equations with bottom topography

---

---

# Numerical results

---

---

# まとめ