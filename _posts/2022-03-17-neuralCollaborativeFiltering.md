---
layout: post
title: Neural Collaborative Filtering (WWW ‘17)
categories: dl
---

# Neural Collaborative Filtering (WWW '17)
- auxiliary information 의 임베딩에 쓰이던 neural network 를 collaborative filtering 에서의 user-item interaction 을 모델링하는 데에 사용함
  - inner product 를 쓰는 것이 일반적이었음 - inner product 에 bias 를 조금 추가한 형태 - MF
- MF 는 latent factor model=based recommendation 에서 defacto approach 였음
  - 많은 연구들이 MF 를 enhancing 시키려 노력했고
    - neighbor-based, topic model, factorization model..
- 이 논문에선 마지막, inner product 를 neural network 로 대체해서 성능을 높였음
  - inner product 가 성능을 제한한다는 것은 잘 알려져 있었고, 실제로 MF 에서도 bias term 을 추가해서 성능을 높였음
- neural network 를 사용해서 더 복잡한 interaction structure 를 포착할 수 있음
- 논문에서 linear 한 공간에 cosine sim 을 사용해 user, item 을 임베딩하는 것의 한계에 대해 설명하고 있음
  - 물론 이런 한계는 더 높은 차원의 latent space 에 임베딩시키는 것으로 해결할 수 있지만
  - 이 경우 파라미터 수가 많아져 overfitting 될 가능성이 높음
    - implicit feedback 은 아주 noisy 한 데이터임  
    또한 sparsity 가 높음 - scarsity
- pointwise method 를 사용해 학습시켰고, 특이한 것은 $w_{ui}$ 라는 하이퍼파라미터가 존재한다는 것임
  - 정확히 어떤 역할을 하는 것인지 모르겠음 - denoting the weight of training instance $(u, i)$ 라는데, $(u, i)$ 쌍은 아주 많음. 어떻게 각 instance 에 weight 를 결정하려는 것인지 모르겠음
- squared loss 는 target 의 분포가 gaussian 이라고 가정했을 때 MLE 를 시도하는 것이라 해석될 수 있음
  - 하지만 implicit feedback 은 그렇지 않고 binary 한 값임. 그래서 BCE 를 사용
  - negative sampling
- MF 를 포함하면서 더 general 한 아키텍쳐인 GMF 제안
  - $\mathbf h$ 가 uniform vector of 1 이고, activation function 이 identity fucntion 이라면 기존의 MF 와 동일함
  - $\mathbf h$ 는 임베딩 벡터끼리 내적할 때, 각 차원의 곱에 가중치를 주는 것이라 해석할 수 있음
    - $k\times k$ 의 파라미터를 만들어서 $v_u W_{k\times k} v_i$ 를 하면 더 표현력이 좋아지지 않을까?
    - 아무튼 이렇게 해서 varying importance of letent dimensions 를 가능하게 한다고 하고 있음
- Neural Tensor Network 에서처럼 embedding vector 를 공유하는 방식도 생각했지만, 이렇게 하면 성능이 제한될 수 있음
  - 같은 임베딩 차원을 사용해야 한다는 것이 대표적
  - 그래서 연산이 끝난 뒤 마지막에 합쳤음
- 이렇게 탄생한 모델을 NeuMF 라고 함

## summary
- inner product $\rightarrow$ neural network (MLP)
- GMF 도입
- GMF 와 MLP 퓨전 $\rightarrow$ NeuMF

---

first draft: 2023.03.17 15:59