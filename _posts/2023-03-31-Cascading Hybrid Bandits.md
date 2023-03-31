---
layout: post
title:  Cascading Hybrid Bandits (Recsys'20)
categories: dl
---

## Cascading Hybrid Bandits: Online Learning to Rank for Relevance and Diversity (Recsys '20)
- https://arxiv.org/abs/1912.00508
- 키워드: online learningto rank, cascading bandits, diversity
- reward 는 ~(추천 리스트의 아이템들을 하나도 안 클릭할 확률) 를 의미하는 것 같음
  - 하나라도 클릭할 확률
  - $1-\Pi_{i=1}^K(1-A_t(\mathcal R_t(i)))$ 라서..
- 저 reward 로 expected regret 라는 걸 정의하는 데 뭔지 모르겠음
- submodular coverage model 이라는 개념이 나옴
  - monotonicity, submodularity 를 만족하는 function 으로 diversification 을 하겠다는 건데
  - submodularity 라는 게 흥미로웠음
    - 대충 가진 게 많을수록 추가되는 게 적어진다는 의미
    - 경제학에서의 효용과도 비슷한 것 같음
    - $g(\mathcal B \cup \\{a\\}) - g(\mathcal B) \geq g(\mathcal A \cup \\{a\\}) - g(\mathcal A)$ for all item sets $\mathcal A, \mathcal B$ s.t. $\mathcal B \subseteq \mathcal A$
- greedy benchmark
  - NP-hard 인 조합론적 최적화 문제를 greedy 한 방식으로 풀겠다는 것
  - $\eta$-approximation 이라는.. 게 나오는데 뭔지 모르겠음
    - 이렇게 했을 떄 이정도 정확도로 근사한다~ 라는 건가?
- algorithm 부분에서 행렬 연산을 막 하는데, 어떻게 나온 값인지 모르겠음
  - $\bf M_t, \bf H_t, \bf B_t$ 같은 변수들이 뭘 의미하는지
  - UCB 는 exploration 방법론 같음
- 그 아래 analysis 부분에서 막 confidence bound 같은 걸로 증명하는데, 뭔지 모르겠음
- 모르는 게 너무 많았다. 뒷부분은 그냥 안 읽었음. 하지만 논문에서 제시하는 방향성과 방법론은 아주 신기했다. bandit 이라는 것도 처음 보고, CF 를 쓰지 않고 user 의 행동에 기반해서 추천한다는 게 신기했다
  - 지금까지 공부한 것과 방향성과 결이 많이 달랐음
- 강화학습을 공부하며 기초를 다져야겠다. 교수님께서 주신 자료를 더 자세히 봐야겠다.

---

first draft: 2023.03.31 18:30