---
title: 'Optimal Transport: Monge and Kantorovich Problems'
date: 2021-09-11
permalink: /posts/2021/09/OT-basics-3/
tags:
  - Optimal Transport
  - Probability Theory
  - Notes
---


In the mass transportation analogy, the "best way to transport mass" is the way that minimizes the total cost of transportation. The heuristic is to analyze the collection of maps

$$
	\newcommand{\dif}{\mathrm{d}}
	\newcommand{\LL}{\mathrm{L}}
	\newcommand{\condset}[4]{\left\{ #1  : \: #2 #3 #4 \right\}}
	\newcommand{\contf}{\mathcal{C}}
	\pi \mapsto \int_{X \times Y} c(x,y) \dif \pi(x,y)
$$

and figure out which map $\pi$ minimizes the total cost of transportation between sites (sets) $X$ and $Y$.

The *primal problem* is Monge's original formulation in the 18th century. Let $T: X \to Y$ be the *optimal transport map* if it solves the following problem:
\begin{equation}
	\label{Eq:Primal_Problem}
	\inf_{\pi \in \Pi(\mu,\nu) \: T_{\sharp} \mu = \nu} \int_{X} c(x,T(x)) \dif \pi (x,y)
\end{equation}
This is a dreadful problem. The cost function can be any function, so convexity of the objective is not necessarily the issue; the constraint that $T_{\sharp} \mu = \nu$ is highly non-convex/non-linear, so it is *a priori* unclear if the problem admits a solution. Showing existence of a solution---even under certain cost structure---was a very tricky variational problem (in fact, in the case of $\LL^1$ transport cost, standard calculus of variation techniques were insufficient). It took roughly 150 years for mathematicians to prove that the problem does admit a solution---albeit, in limited cases. Nevertheless, Monge assumed cost function was $\LL^1$, and made interesting geometric observations about the solution---assuming it exists.


Kantorovich introduced a relaxation of the primal problem in \eqref{Eq:Primal_Problem}, in which instead of searching for an optimal coupling, one would search for a pair of potential functions such that the cost is minimized. Moreover, as will be remarked later, this is a *linear programming problem*,  can easily be interpreted in terms of standard probability theory, and has valid economic interpretations and applications.

The *dual problem* to \eqref{Eq:Primal_Problem} is
\begin{equation}
	\label{Eq:Dual_Problem}
	\sup_{(\phi, \psi) \in A(c)} \int_{X}  \phi \dif \mu + \int_{Y} \psi \dif \nu
\end{equation}
where $A(c)$ is the set of *admissible potentials* defined as
\begin{equation}
	A(c) = \condset{(\phi,\psi) \in \LL^1(\mu) \times \LL^1(\nu)}{\phi \oplus \psi \leq c(x,y)}{}{}
\end{equation}
The goal of this section is to eventually prove the following fact: that for any cost function, the solutions to \eqref{Eq:Primal_Problem} and \eqref{Eq:Dual_Problem} are equal (i.e. we will prove equivalence between $\Pi(\mu,\nu)$ and $A(c)$). This is amazing because we do not need to worry about perturbation in one space having an effect on solutions in the other space.


Largely following Villani (2003), here is an elementary first step towards establishing equivalence.

**Lemma (Preliminary Equivalence)**.

$$
\label{Eq:prelim-equivalence}
\sup_{A(c) \cap \contf_b}  \int_{X}  \phi \dif \mu + \int_{Y} \psi \dif \nu \leq \sup_{A(c) \cap \LL^1} \int_{X}  \phi \dif \mu + \int_{Y} \psi \dif \nu \leq \inf_{\pi \in \Pi(\mu, \nu)} \int_{X} c(x,y) \dif \pi(x,y)
$$

**Proof**. 
The first inequality in \eqref{Eq:prelim-equivalence} is trivial, since $\contf_b \subset \LL^1$. 
	
For the second inequality, fix some potentials $(\phi, \psi) \in A(c) \cap \LL^1$. Take any $\pi \in \Pi(\mu,\nu)$\footnote{In lieu of this, I will say "take any coupling $\pi$" from now on, whenever the source and target measures are clear from context}. It follows that

$$
	\begin{align*}
		\int_{X}  \phi \dif \mu + \int_{Y} \psi \dif \nu &= \int_{X \times Y} \phi(x) + \psi(y) \dif \pi(x,y) \\
		%
		&\leq \int_{X \times Y} c(x,y) \dif \pi(x,y)
	\end{align*}
$$

i.e. the inequality is true except on sets of measure zero. Why is this true? Let $N_x$ and $N_y$ be measure zero sets on $X$ and $Y$, respectively. Then, $N_x^c \times N_y^c$ have full measure with respect to $\pi$. Without loss, take $(x,y) \in N_x^c \times N_y^c$ such that the inequality above holds. It follows that $\pi[ (N_x^c \times N_y^c)^c] = 0$, i.e. the inequality above holds without the supremum---for any admissible potentials.
	
Taking the supremum over $A(c) \cap \LL^1$ then infimum over $\Pi (\mu, \nu)$ gives us the desired inequality. $ \quad \blacksquare $

The rough roadmap for the rest of this section is to introduce tools from convex analysis that will help us in formally establishing equivalence between \eqref{Eq:Primal_Problem} and \eqref{Eq:Dual_Problem}. The rigourous derivation will show insight on why \eqref{Eq:Dual_Problem} is a linear programming problem. At the end, I will explicitly show that it is indeed a linear programming problem.


Finally, to make notations compact, I will write the following for the remainder of this section:

$$
\begin{align*}
	M (\pi) &\triangleq \int_{X} c(x,y) \dif \pi(x,y) \\
	%
	K (\phi, \psi) &\triangleq  \int_{X}  \phi \dif \mu + \int_{Y} \psi \dif \nu 
\end{align*}
$$

