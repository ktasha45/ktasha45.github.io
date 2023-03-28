---
layout: post
title:  real analysis 1
categories: mathematics
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
  - $B = \\{r \in \mathbb Q \vert r > 0, r^2 < 2\\}$
  - $B$ 는 0 라는 lower bound 를 가짐. 하지만 maximum element 를 갖지 않음
    - 이를 증명하기 위해서, 다음을 보이면 됨
    - if $p \in B$, then there exists $q \in B$ s.t. $p<q$
    - $q=p+\frac{2-p^2}{p+2}$ 로 잡으면 조건을 만족함  
    $\therefore$ 모든 $p$ 에 대해 그것보다 큰 $q$ 가 존재하고, maximum 은 존재하지 않음
- 유리수에서는 maximum 을 찾을 수 없음
- 

---

first draft: 2023.03.28 18:38