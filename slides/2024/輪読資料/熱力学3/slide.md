---
marp: true
theme: peru24doc
title: 熱力学 現代的な視点から 第3章 3-7
description: 第3章 等温操作とHelmholtzの自由エネルギー 3-7の資料です。
math: mathjax
author: Teruki TADA
session: FUNAI輪読会
date: 2024-11-05
tags: FUNAI
thumbnail: img/kanku.webp
---

**熱力学 現代的な視点から**
# 第3章 等温操作とHelmholtzの自由エネルギー 3-7

多田 瑛貴
公立はこだて未来大学 システム情報科学部
複雑系知能学科 複雑系コース 3年

*写真: 大阪国際空港*

![bg right:40%](img/kanku.webp)

---

# 前回学んだこと

### Kelvinの原理
- ある平衡状態が、等温操作を経てもとの平衡状態に戻るとき (「等温サイクル」)
  外界に対して正の仕事をすることはありえない
  *反例があるとしたら「第二種の永久機関」が存在することになる*

- 等温準静サイクルの外界に対して行う仕事は0

---

# 前回学んだこと

### Helmholtzの自由エネルギー

適当な値 $X_0(T)$ を基準点として
$$ F[T;X] = W_{max}(T;X \rightarrow X_0 (T)) $$

- 等温操作では、ある平衡状態から別の平衡状態に移る際に外界に行う仕事は
  操作の具体的な方法に依存してしまう
- そこで「最大仕事」から「Helmholtzの自由エネルギー」を定義
  平衡状態が移る際に外界に行う仕事の最大値は
  二つの状態のHelmholtzの自由エネルギーの差に等しくなる
  *力学のポテンシャルエネルギーのように扱える*

---

# 圧力と状態方程式

---

## 圧力とHelmholtzの自由エネルギー

平衡状態 $(T;V,N)$ に、以下の等温操作を施し、体積を変化させる
$$(T;V,N)\overset{\text{iq}}{\longrightarrow}(T;V+\Delta V,N)$$

$\Delta V$は$V$より十分小さいとする
このとき、断面積$A$のピストンから大きさ$F$の力が加わるとする

![](img/3.3.webp)

---

このとき、最大仕事は
$$W_{max}(T;(V,N)\rightarrow(V+\Delta V,N))$$

これを外界のマクロな力学の言葉で表すと
ピストンの移動距離を$\Delta\ell$として

$$W_{max}(T;(V,N)\rightarrow(V+\Delta V,N)) = F\Delta\ell+O((\Delta\ell)^2)$$

と書ける

---

## 圧力の導入

圧力...一般に、力の大きさを面の面積で割った量

圧力$p=F/A$と書くと、$A\Delta\ell=\Delta V$から

$$
\begin{equation}
\begin{split}
W_{max}(T;(V,N)\rightarrow(V+\Delta V,N)) & = F\Delta\ell+O((\Delta\ell)^2) \\
& = p\Delta V+O((\Delta V)^2)
\end{split}
\end{equation}
 $$


この式を逆に見ると
力学的な量として導入されている圧力$p$は
熱力学的な状態$(T;V,N)$によって定まる状態量であるとみなせる

---

すると、状態量としての圧力は
$$
\begin{equation}
\begin{split}
p(T;V,N) & = \lim_{\Delta V \searrow 0} \frac{W_{max}(T;(V,N)\rightarrow(V+\Delta V,N))}{\Delta V} \\
& = \lim_{\Delta V \searrow 0} \frac{F[T;V,N]-F[T;V+\Delta V,N]}{\Delta V} \\
& = -\frac{\partial}{\partial V}F[T;V,N]
\end{split}
\end{equation}
$$

となり、Helmholtzの自由エネルギーと結ばれる


---
<!-- _class: smartblockquote -->

> 圧力と自由エネルギーの関係 $p(T;V,N) = -\frac{\partial}{\partial V}F[T;V,N]$

$(V, N)$をそのまま$(\lambda V, \lambda N)$に置き換えると
Helmholtzの自由エネルギーの示量性から

$$
p(T;\lambda V,\lambda N) = -\frac{\partial F[T;\lambda V,\lambda N]}{\partial (\lambda V)} = -\frac{\lambda \partial F[T;V,N]}{\lambda \partial V} = p(T;V,N)
$$

より、圧力は示強的な熱力学関数であるといえる

---
<!-- _class: smartblockquote -->

> 圧力と自由エネルギーの関係 $p(T;V,N) = -\frac{\partial}{\partial V}F[T;V,N]$

さらに、任意の$T$と$N$について
基準点$X_0$での体積$v(T)N$から任意の$V$まで積分すれば


$$
F[T;V,N]= \int_{v(T)N}^{V}dV' p(T;V',N)
$$

これにより、測定可能な力である圧力を使って
Helmholtzの自由エネルギーを定めることができる

*$X_0(T)=(v(T)N, N)$としていることについては、教科書p47を参照*

---

## 状態方程式

平衡状態での流体の圧力$p(T; V,N)$を$T,V,N$の関数として表現した式を
**状態方程式**と呼ぶ

適当な温度範囲で、体積が十分大きい場合の状態方程式について
一連の実験によって次の式が見出された
$$p(T; V, N) \simeq \frac{NRT}{V}$$

$R$は気体定数$(R \simeq 8.3145 [N \cdot m \cdot (K \cdot \text{mol})^{-1}])$

*高校物理でも出てくる状態方程式と同じ*

*上の式が成り立つように選ばれた温度は**理想気体温度**とも呼ばれる*

---

## 理想気体

圧力が正確に$p(T; V, N) \simeq \frac{NRT}{V}$で与えられるような仮想的な気体
現実には存在しない *相転移も考慮されていない*

---

理想気体のHelmholtzの自由エネルギー

$$
F[T;V,N]= \int_{v(T)N}^{V}dV' \frac{NRT}{V'} = -NRT\log{\frac{V}{v(T)N}}
$$

Helmholtzの自由エネルギーは
「我々が『自由に使えるエネルギー』」であると表現されていた
実際に上の式が$V$についての減少関数であり、体積が増えるほど減少する
(↔体積が小さければ、膨張の際に仕事をする能力を持っている)
ことを考えれば、自然な解釈と思える

---

補足 (筆者によると)

熱力学の理論体系からは、具体的な系の状態方程式は決定できない
- 状態方程式は個々の熱力学に応じて決まるもので、何らかの一般論で決まるわけではない
- 具体的な系の状態方程式を知る最良の方法は、実験によって様々な温度と密度で系の圧力を測定することである


---

# まとめ

- 体積を微小に変化させる等温操作に注目して、圧力を導入

- 圧力と自由エネルギーの関係 $p(T;V,N) = -\frac{\partial}{\partial V}F[T;V,N]$ が成り立ち、以下のことがわかる
  - 圧力は示強的な熱力学関数
  - 圧力を使ってHelmholtzの自由エネルギーを定めることができる

- 状態方程式を用いて実際にHelmholtzの自由エネルギーを計算
