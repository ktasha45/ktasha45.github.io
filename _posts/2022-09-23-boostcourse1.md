---
layout: post
title:  boostcourse ai 4th
categories: math
---

# boostcourse ai tech 4기 1주차 회고
## learned
 - vector, matrix, gradient descent

## thought
 - Moore-penrose 역행렬이 선형 회귀에서 최적의 해를 나타내는 이유
   - 관련 설명: [link](https://angeloyeo.github.io/2020/11/11/pseudo_inverse.html)
 - Moore-penrose 역행렬을 구할 때 $A^\intercal A$나 $AA^\intercal$의 determinant는 고려하지 않아도 되는 것인가?
 - $\partial_{\beta_k}||\bold y - X\beta||$ 의 결과에서 분모에 $n$이 나오는 이유. 실제로 l2 norm으로 계산해보면 $\sqrt{n}$이 나옴. 
   - 이유: norm이 새롭게 정의되었기 떄문  
     -> norm을 임의로 설정해도 되는 건가?( l2 norm은 유클리디안 거리인데)  
     -> 1/n을 루트 안에 넣는 거랑 밖에 두는 거랑 차이는 뭘까?
  $$||\bold y - X\beta|| = \sqrt{\frac{1}{n}\sum_{i=1}^n\left(y_i - \sum_{j=1}^d X_{ij}\beta_j\right)}$$
  - 아래 사진은 각각 $f(x, y) = x^2 + 2y^2$, $f(x, y) = x^2 + y^2$에서 gradient descent를 수행했을 때 x와 y의 궤적을 나타낸다.  
  <img src="https://user-images.githubusercontent.com/47550287/191882708-0db9fced-fe8c-43d5-88d1-7b854040d717.png" width="50%">
  <img src="https://user-images.githubusercontent.com/47550287/191882948-0148765a-524b-4f3c-94d6-0483c83d4d57.png" width="49%">  
  전자의 경우 타원이기 때문에 궤적이 곡선을 그리게 되는데, 사이클로이드처럼 보이기도 한다. 코드는 [다음](https://d2l.ai/chapter_optimization/gd.html)을 참고했다.

## not boostcamp
 - overparameterized $\left(N<<M\right)$ 선형회귀에서 gradient descent를 하면 항상 zero-loss 평면에 수직으로 접근한다.
 - overparameterized 선형회귀에서 $\text{span}(x_1, ..., x_n)$ 은 zero-loss를 이루는 가중치 $\theta$들의 집합($m$차원 공간에서의 hyperplane)과 orthogonal하다는 게 이해가 안 됨.
   - $\Theta_0 := \{\theta \in \R^M \ | \ \theta^\intercal - y_i = 0, \forall i \in [N]\}$
   - 변수가 2개, 데이터가 1개인 경우를 생각해보면 직교함을 쉽게 보일 수 있음. 어떻게 일반화할 수 있을까?
 - cnn과 fourier transform의 관계?
   - fourier transform은 n차원의 신호를 무한차원 벡터공간(힐베르트 공간)으로 선형변환하는 걸로 알고 있는데, 이론적으로 이 이해가 맞는 건가?
   - fourier transform을 단기간에 이해할 수 있는 참고자료가 어떤 게 있을지
 - prml chap 3에서 나오는 least square의 기하학적 해석과 Moore-penrose 역행렬을 기하학적으로 해석한 것은 결국 같은 걸 의미하고 있다.
 - 






