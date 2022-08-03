---
title: 'Optimal Transport: Minimax Principle'
date: 2021-09-11
permalink: /posts/2021/09/OT-basics-2/
tags:
  - Optimal Transport
  - Probability Theory
  - Functional Analysis
  - Notes
---

I describe Rockafellar's minimax principle and other related concepts herein.

$$ \begin{align*}
	\DeclareMathOperator{\Ma}{\mathrm{Ma}} \DeclareMathOperator{\contf}{\mathcal{C}} \DeclareMathOperator{\LL}{\mathrm{L}}
	\DeclareMathOperator{\dif}{\mathrm{d}\:}
	\newcommand{\set}[1]{\left\{ #1 \right\}}
	\DeclareMathOperator{\suchthat}{\text{ s.t. }}
		\newcommand{\condset}[4]{\left\{ #1  : \: #2 #3 #4 \right\}}
	\newcommand{innerproduct}[2]{\left\langle #1, #2 \right\rangle}
	\DeclareMathOperator{\R}{\mathbb{R}}
	\DeclareMathOperator{\closure}{\mathrm{cl}}
	\DeclareMathOperator{\interior}{\mathrm{int}}
\end{align*} $$

The classical approach is to borrow functional analytic tool to establish approximations of solutions on different functional classes. A formal minimax principle follows via applying the Legendre-Fenchel transform, in order for one to work with normed linear spaces and their duals. First, a brief reminder: a **Radon measure** is a Borel measure that is finite on compact sets,
outer regular on all Borel sets, and inner regular on open sets. Some useful facts are the following:

**Proposition**.
If $\mu$ is a Radon measure on a $\sigma$-finite set $X$. Then, $\contf_c(X)$ is dense in $\LL^p (\mu)$ for $p \in [1,\infty)$. Here, $\contf_c(X)$ denotes the space of bump (test) functions.


**Lemma (Urysohn)**.
If $X$ is a locally compact, Hausdorff space, and $K \subset U \subset X$, where $K$ is compact, and $U$ is open, then there exists a continuous function $f : X \to [0, 1]$ such that $f \equiv 1$ on $K$ and $f \equiv 0$ outside a compact subset of $U$.


Note that Urysohn's Lemma is extremely helpful in situations when we're trying to prove the regularity of a measure: we have a compact $K$ contained in an open set $U$, and often want to approximate a characteristic function with a continuous function. It says such a continuous function exists, approximating the characteristic functions of $K$ and $U$, and---in fact---this holds true up to $U \setminus K$.

**Fact**.
A Radon measure is inner regular on all of its $\sigma$-finite sets.

**Definition**.
A Hausdorff space $X$ is called a Radon space if every finite Borel measure on X is a Radon measure.

**Fact**.
Let $X$ be a locally compact Hausdorff space in which every open set is $\sigma$-compact. Then, every Borel measure on $X$ which is finite on compact sets is regular, therefore Radon.

It follows from basic topology that if $X$ is second countable, then every open set is $\sigma$-compact.


Now, fix the notation $\Ma(X)$ as the collection of Radon measures on $X$. Let $\Ma_{+} (X)$ denote the collection on positive Radon measures on $X$. Clearly, $\Ma_{+} (X) \subset M(X)$ is closed under addition and scalar multiplication, for scalars $\lambda \geq 0$, and $\Ma_{+} (X)$ contains the constant functions (in particular, $m \equiv 0$); therefore, $\Ma_{+} (X)$ is a pointed convex cone.

We then adopt the following "relaxation" of the primal problem: let
\begin{equation}
	\label{Eq:Primal_Problem_Radon}
	\inf_{\pi \in \Pi(\mu,\nu)} M(\pi) = \inf_{\pi \in \Ma_{+} (X \times Y)} M(\pi) + \iota_{\Pi(\mu,\nu)}^{\infty} (\pi)
\end{equation}
where $\iota_{\Pi(\mu,\nu)}^{\infty}$ is the "indicator function" taking value $0$ if $\pi \in \Pi(\mu,\nu)$, and $+\infty$ otherwise.

We have the relationship
\begin{equation}
	\label{Eq:iota_equivalence}
	\iota_{\Pi(\mu,\nu)}^{\infty} (\pi) = \sup_{(\phi,\psi) \in \contf_b (X) \times \contf_b (Y)} \int_{X} \phi \dif \mu + \int_{Y} \psi \dif \nu - \int_{X \times Y} \phi \oplus \psi \dif \pi
\end{equation}
Why is this true? Take any measure zero sets $N_x$ and $N_y$ on $X$ and $Y$, respectively. Then, in either case we have the left-hand side of \eqref{Eq:iota_equivalence} is zero, so we have one side of the inequality.

For the other side, notice that if $\pi \notin \Pi(\mu,\nu)$, the left-hand side is $+\infty$, but right-hand side is

$$
\begin{align*}
	\int_{X} \phi \dif \mu + \int_{Y} \psi \dif \nu - \int_{X \times Y} \phi \oplus \psi \dif \pi &\leq \int_{X} \phi \dif \mu + \int_{Y} \psi \dif \nu - \int_{X \times Y} \phi \oplus \psi \dif \eta \\
	%
	&= \int_{X} \phi \dif \mu + \int_{Y} \psi \dif \nu - \int_{X \times Y} c(x,y) \dif \eta \\
	&\leq \int_{X \times Y} c(x,y) \dif \pi^{\star} - \int_{X \times Y} c(x,y) \dif \eta
\end{align*}
$$

where $\pi^{\star}$ is some admissible potential (may not be optimal), so the right-hand side is either finite or infinite. In any case, we have the other inequality. Therefore, we have equality in \eqref{Eq:iota_equivalence}.

With the equivalence in \eqref{Eq:iota_equivalence} established, we can write the dual problem in the following minimax form:
\begin{equation}
	\label{Eq:K_Minimax_Problem}
	\inf_{\pi \in \Ma_{+} (X)} \sup_{(\phi, \psi) \in A(c)} \int_{X \times Y} c(x,y) \dif \pi + \int_{X} \phi \dif \mu + \int_{Y} \psi \dif \nu - \int_{X \times Y} \phi \oplus \psi \dif \pi
\end{equation}
which one can interpret as the minimum discrepancy between the actual total cost of transportation under optimal transport plan, and the actual total cost under admissible transport plans.

Taking for granted that we can appeal to minimax principles, we would have

$$
\begin{align*}
	&\sup_{(\phi, \psi) \in A(c)} \inf_{\pi \in \Ma_{+} (X)} \int_{X \times Y} c(x,y) \dif \pi + \int_{X} \phi \dif \mu + \int_{Y} \psi \dif \nu - \int_{X \times Y} \phi \oplus \psi \dif \pi \\
	=& \sup_{(\phi, \psi) \in A(c)} \set{ \int_{X} \phi \dif \mu + \int_{Y} \psi \dif \nu - \sup_{\pi \in \Ma_{+} (X)} \int_{X \times Y}  \phi \oplus \psi - c(x,y) \dif \pi } ~.
\end{align*}
$$

from \eqref{Eq:K_Minimax_Problem}, after some algebra. Observe that if $\xi (x,y) \triangleq \phi \oplus \psi - c(x,y) > 0$ for some $(x_0, y_0)$, then $\pi = \lambda \delta_{(x_0,y_0)}$. Passing $\lambda \to \infty$, one observes the the supremum is $+\infty$ when the potentials \textit{are not admissible}. If the potentials are admissible, we have $\xi = 0$, hence $\pi = 0$ (measure). This observations allows us to conclude that the primal problem is equivalent to the dual problem.

**Definition**.
Let $E$ be a normed linear space, and $\Theta$ be a convex function such that $\Theta : E \to \R \cup \set{+\infty}$. Then, the \textbf{Legendre-Fenchel transform} is defined as
\begin{equation}
		\label{Eq:L-F-Transform}
		\Theta^{\star} (z^{\star}) = \sup_{z \in E} \set{\innerproduct{z^{\star}}{z} - \Theta(z)}
\end{equation}
which is defined on the dual of $E$, denoted $E^{\star}$.

A useful, and serious, minimax principle is the following. Continue to denote $E$ as a normed vector space, $E^{\star}$ is the topological dual, $\Theta, \Xi : E \to \R \cup \set{+\infty}$ are convex functions, $\Theta^{\star}, \Xi^{\star}$ are the associated Legendre-Fenchel transforms.

**Theorem (Legendre Duality)**.
If there exists some $z_0 \in E \suchthat \Theta(z_0) < +\infty$, $\Xi (z_0) < +\infty$, and $\Theta$ is continuous at $z_0$, then

\begin{equation}
		\label{Eq:Minimax_Rigourous_Equation}
		\inf_{z \in E} \Theta + \Xi = \sup_{z^{\star} \in E^{\star}} \left[ - \Theta^{\star} (-z^{\star}) - \Xi^{\star} (z^{\star}) \right]
\end{equation}


**Proof of Legendre Duality**.	
Note that 

$$
		- \Theta^{\star} (-z^{\star}) = \innerproduct{z^{\star}}{z} + \Theta (z), \: \: \Xi^{\star} (z^{\star}) = \innerproduct{z^{\star}}{z} - \Xi (z)
$$

It remains to show that 
\begin{equation}
		\label{Eq:Minimax_Rigorous_Proof}
		\sup_{z^{\star} \in E^{\star}} \inf_{x,y \in E} \Theta (x) + \Xi (y) + \innerproduct{z^{\star}}{x-y} = \inf_{x \in E} \Theta(x) + \Xi(x)
\end{equation}
(If this is true, then \eqref{Eq:Minimax_Rigourous_Equation} holds).
	
Clearly, if $x=y$, then \eqref{Eq:Minimax_Rigorous_Proof} trivially shows that left-hand side is less than or equal to the right-hand side. So, the difficult part is the reverse inequality.
	
I define "good" sets

$$
\begin{align*}
		C &\triangleq \condset{(x,\lambda) \in E \times \R}{\lambda > \Theta (x)}{}{} \\
		%
		C' &\triangleq \condset{(y,\mu) \in E \times \R}{\mu \leq}{\left[ \inf_{x,z \in E} \Theta(x) + \Xi (z) \right] - }{\Xi (y)}
\end{align*}
$$

One can easily see that $C$ is the subgraph of $\Theta(x)$, and $C'$ is the epigraph of the function $\left[ \inf_{x,z \in E} \Theta(x) + \Xi (z) \right] - \Xi (y)$. Clearly, both are convex by construction. It is also clear that $(z_0, \Theta(z_0) + 1) \in \interior C$ (why? observe this by continuity and set $\varepsilon = 1$). It follows that $\interior C \neq \emptyset$, so $\closure{C} = \closure{\interior C}$.
	
Finally, note that $C$ and $C'$ are disjoint, since $\Theta (x) > \left[ \inf_{x,z \in E} \Theta(x) + \Xi (z) \right] - \Xi (y)$. Therefore, by Hahn-Banach extension theorem, there exists a bounded linear function $\ell \in (E \times \R)^{\star}$ such that

$$
		\inf_{c \in C} \innerproduct{\ell}{c} = \inf_{c \in \interior C} \innerproduct{\ell}{c} \geq \sup_{c' \in C'} \innerproduct{\ell}{c'}
$$

by linearity, we have there exists a $w^{\star} \in E^{\star}, \alpha \in \R_{+}$ such that $(w^{\star}, \alpha) \neq (0,0)$, and $\innerproduct{w^{\star}}{x} \geq \innerproduct{w^{\star}}{y} + \alpha \mu$ on sets $C$ and $C'$. Further note that this statement has no hope of being true if $\alpha \leq 0$! So, setting $z^{\star} = \frac{w^{\star}}{\alpha}$, we have $\innerproduct{z^{\star}}{x} + \lambda \geq \innerproduct{z^{\star}}{y} + \mu$, which means 

$$
		\innerproduct{z^{\star}}{x} + \Theta(x) \geq \innerproduct{z^{\star}}{y} - \Xi (y) + \inf_{x,z \in E} \Theta(x) + \Xi (z)
$$

which holds for all $x,y \in E$. Rearrange the terms, then take $\sup$ on both sides over all elements in the dual $E^{\star}$, we have recovered the other inequality. $\quad \blacksquare$
