---
layout: post
title:  real analysis 1
categories: Mathematics
---

- Archimedean property of $\mathbb R$
  - for $x, y> 0 $, there is always some $n \in \mathbb N$ with $nx>y$
    - 양수 x, y 에 대해서 항상 $nx>y$ 를 성립시키는 자연수 $n$ 이 존재한다
- least upper bound property (Completeness axiom)
  - set $S \subset \mathbb R$ is bounded above if there is a real number $M$  
  such that $s \leq M$ for all $s \in S$
    - 어떤 $M$ 이 존재해서, $S$ 의 모든 원소보다 크면 $S$ 는 bounded above 이다
      - 이때 $M$ 은 upper bound 이다
    - 정의의 순서를 바꿔놓으면 말이 달라진다
      - $S$ 의 원소 $s$ 에 대해서 그것보다 큰 $M$ 이 있으면~ 으로 순서가 바뀌면, 이 때의 $M$ 은 각 원소 $s$ 에 depend 한 값이 되므로 그냥 $M=s$ 로 잡으면 조건을 만족해버린다.
      - 순서가 중요함
  - Suppose a nonempty subset $S$ of $\mathbb R$ is bounded above, then $L$ is the supremum or least upper bound for $S$  
  if $L$ is an upper bound for $S$ that is smaller than all other upper bounds
    - for all $s\in S$, $s\leq L$ and if $M$ is another upper bound for $S$, then $L \leq M$.
      - $L < M$ 이어도 될 것 같은데..
    - It is denoted by $\sup S$
      - $\inf S$ 도 똑같은 방식으로 정의
    - supremum 이 존재한다면, 유일하다
    - $\sup S = +\infty$ 이면 not bounded above, $\inf -\infty$ 이면 not bounded below
    - By convention, $\sup \emptyset = +\infty, \inf \emptyset = -\infty$
  - set $S \subset \mathbb R$ 의 maximum 은, 만약 존재한다면, $S$ 의 원소이면서 $S$ 의 모든 원소보다 크거나 같아야 한다  
  (the element $m \in S$ such that $s \leq m$ for all $s \in S$)
    - 그리고 $\max S$ 가 존재한다면 그것이 $\sup S$ 이다
  - 당연하게도 upper bound 와 lower bound 는 무한히 존재할 수 있다
- 흥미로운 예시가 하나 있다
  - $B = \\{r \in \mathbb Q \vert r > 0, r^2 \leq 2\\}$
  - $B$ 는 0 라는 lower bound 를 가짐. 하지만 maximum element 를 갖지 않음
    - 이를 증명하기 위해서, 다음을 보이면 됨
    - if $p \in B$, then there exists $q \in B$ s.t. $p<q$
    - $q=p+\frac{2-p^2}{p+2}$ 로 잡으면 조건을 만족함  
    $\therefore$ 모든 $p$ 에 대해 그것보다 큰 $q$ 가 존재함
- 유리수에서는 maximum 을 찾을 수 없음
  - $\sqrt 2$ 를 표현하기 위해서 least upper bound 를 도입
    - 그냥 maximum 으로 나타내면 안 되나? 굳이 supremum 을 도입한 이유는?
    - 좀 더 general 한 경우까지 나타낼 수 있는 것 같음 - 애초에 열린 구간이면 maximum 이 존재하지 않음. 하지만 어떤 경우에도 supremum 은 존재함
- limit
  - A real number $L$ is the limit of a sequence of real numbers $(a_n)^\infty_{n=1}$ if for every $\epsilon > 0$, there is an integer $N=N(\epsilon) > 0$ such that $\vert a_n-L\vert < \epsilon$ for all $n \geq N$  
  We say that the sequence $(a_n)^\infty_{n=1}$ converges to $L$ and we write $\lim\limits_{n \to \infty} a_n = L$
  - 많이 쓰는 정의
  - $(a_n)^\infty_{n=1}$ 가 수렴하면, 집합 $\\{a_n:n\in \mathbb N\\}$ is bounded
- Monotone Sequence
  - A monotone increasing/decreasing sequence that is bounded above/below converges
    - 단조수열이면서 bounded 이면 수렴한다
  - $a_n$ 을 증가하는 위로 유계 수열이라고 가정하고, supremum 을 $L$ 으로 잡고
    - $$L-\epsilon < a_N \leq a_n \leq L \  \text{ for all } \ n \geq 1$$
    - 정리해서 증명 가능
  - 단조수렴정리를 통해 수렴 여부를 먼저 판단하고 수렴값을 구할 수 있음
- Nested intervals lemma - 축소구간정리?
  - corollary of the 단조수렴정리
  - $I_n = [a_n, b_n]$ 를 nonempty closed intervals such that $I_{n+1} \subseteq I_n$ for each $n \geq 1$ 이라고 하자. Then the intersection $\cap_{n \geq 1}I_n$ is nonempty
  - $a_n \leq a_{n+1} \leq b_{n+1} \leq b_n$ 이라는 정의를 사용해서 증명
- Subsequences
  - Original sequence 가 발산해도 subsequence 는 수렴할 수도 있다
  - A subsequence of a sequence $a_n$ is a sequence $(a_{n_k})^\infty_{n=1}=(a_{n_1}, a_{n_2}, a_{n_3}, \dots)$, where $n_1 < n_2 < \dots$
- Bolzano-Weierstrass Theorem
  - 모든 닫힌 실수 수열은 수렴하는 부분 수열을 가진다
  - nested interval lemma 로 증명 가능
- Caushy Sequences
  - 수렴값을 가정하지 않고 수열의 수렴성을 어떻게 확인할 수 있을까?
  - Let $(a_{n_k})^\infty_{n=1}$ be a sequence converging to $L$. For every $\epsilon > 0$, there is an integer $N$ s.t. $\vert a_n - a_m\vert < \epsilon$ for all $n,m \geq N$
    - 아까 converge 의 정의에서 쓴 것과 조금 다름
  - A sequence $(a_{n_k})^\infty_{n=1}$ of real numbers is called a Cauchy sequence provided that for every $\epsilon > 0$, there is an integer $N$ s.t. $\vert a_n - a_m\vert < \epsilon$ for all $n,m \geq N$
  - Every Cauchy sequence is bounded
  - A subset $S$ of $\mathbb R$ is said to be complete if every Cauchy sequence $(a_n)$ in $S$ (that is, $a_n \in S$) converges to a point in $S$
- Completeness Theorem
  - Every Cauchy sequence of real numbers converges. So $\mathbb R$ is complete.
  - 어떤 수열이 코시 수열인지 판단하는 것으로 수렴성을 확인할 수 있음

---

first draft: 2023.03.28 18:38  
second draft: 2023.03.29 19:53 - limit ~ cauchy sequence