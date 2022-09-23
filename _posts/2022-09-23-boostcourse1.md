---
layout: post
title:  boostcourse ai tech 4기 1주차 회고
categories: boostcourse
---

# boostcourse ai tech 4기 1주차 회고
## learned
 - vector, matrix, gradient descent

## thought
- Moore-penrose 역행렬이 선형 회귀에서 최적의 해를 나타내는 이유
   - 관련 설명: [link](https://angeloyeo.github.io/2020/11/11/pseudo_inverse.html)
- Moore-penrose 역행렬을 구할 때 $A^\intercal A$나 $AA^\intercal$의 determinant는 고려하지 않아도 되는 것인가?   
- $\partial_{\beta_{k}}||\mathbf{y}-X\beta||$ 의 결과에서 분모에 $n$이 나오는 이유. 실제로 l2 norm으로 계산해보면 $\sqrt{n}$이 나옴.  
  -> 이유: norm이 새롭게 정의되었기 때문  
  -> norm을 임의로 설정해도 되는 건가? (l2 norm은 유클리디안 거리인데) 
  가능하다고 함 (조교님: 많은 norm이 정의되어있고 다양하게 적용한 연구들이 많은 것으로 알고 있다) -> 구체적으로 어떤 게 있을까?  
  -> 1/n을 루트 안에 넣는 거랑 밖에 두는 거랑 차이는 뭘까?  
  -> 새롭게 정의된 norm은 다음과 같다.
  $$||\mathbf y - X\beta|| = \sqrt{\frac{1}{n}\sum_{i=1}^n\left(y_i - \sum_{j=1}^d X_{ij}\beta_j\right)}$$
- 부스트캠프 강의에서  
  <img src="https://user-images.githubusercontent.com/47550287/191895425-6087a4ef-a161-49d4-b319-7aeed7a9999d.png" width="80%">  
  위와 같은 그림이 나왔고, 직선으로 내려가야 하는 것 아닌가 싶어 실험해보았다.  
  아래 사진은 각각 $f(x, y) = x^2 + 2y^2$, $(f(x, y) = x^2 + y^2$에서 gradient descent를 수행했을 때 $x$와 $y$의 궤적을 나타낸다.  
  <img src="https://user-images.githubusercontent.com/47550287/191882708-0db9fced-fe8c-43d5-88d1-7b854040d717.png" width="45%">
  <img src="https://user-images.githubusercontent.com/47550287/191882948-0148765a-524b-4f3c-94d6-0483c83d4d57.png" width="45%">  
  강의의 시각자료는 틀리지 않았다.  
  전자의 경우 타원이기 때문에 궤적이 곡선을 그리게 되는데, 사이클로이드처럼 보이기도 한다. 코드는 [다음](https://d2l.ai/chapter_optimization/gd.html)을 참고했다.  
  
## not boostcamp
 - overparameterized $\left(N\text{<}\text{<}M\right)$ 선형회귀에서 gradient descent를 하면 항상 zero-loss에 수직으로 접근한다.
 - overparameterized 선형회귀에서 $\text{span}(x_1, ..., x_N)$ 은 zero-loss를 이루는 가중치 $\theta$들의 집합 ($M$차원 공간에서의 hyperplane)과 orthogonal하다는데 어떻게 그렇게 되는 건지 잘 이해가 안 됨.  
  zero-loss를 이루는 가중치 $\theta$들의 집합 $\Theta_0 := \left\\{\theta \in \mathbb{R}^M \ | \ \theta^\intercal\mathbf{x}_i - \mathsf{y}_i = 0, \forall{i} \in [N]\right\\}$  
   - 변수가 2개, 데이터가 1개인 경우를 생각해보면 직교함을 쉽게 보일 수 있음. 어떻게 일반화할 수 있을까?
 - cnn과 fourier transform의 관계?
   - fourier transform은 n차원의 신호를 무한차원 벡터공간(힐베르트 공간)으로 선형변환하는 걸로 알고 있는데, 이론적으로 이 이해가 맞는 건가?
   - fourier transform을 단기간에 이해할 수 있는 참고자료가 어떤 게 있을지
 - prml chap 3에서 나오는 least square의 기하학적 해석과 Moore-penrose 역행렬을 기하학적으로 해석한 것은 결국 같은 걸 의미하고 있다.
 - mathjax 너무 어렵다. vscode에서는 잘 나오는데... vscode에서 $ $ 으로 잘 되던 것들이 mathjax 형식으로 바꾸기만 하면 잘 안 됨. 그리고 일일이 다 바꿔줘야 하고. -> 두 번째 문제는 3.2.2에서 2.7.5로 버전을 낮춰서 해결함
- l1 norm과 l2 norm과 라그랑주는 어떤 관련이 있는 거지?
- 왜 sgd가 gd보다 빠르게 수렴하는 걸까?
- weight initalization과 relu는 어떤 관련이 있을까?
- KL divergence와 MLE는 결론적으로 같다는데, 무슨 의미이지?
  - 조교님: 1. MLE 와 KL divergence 가 결론적으로 같습니다. 물론, 같아지기 위해서는 KL divergence 값을 구할 때 인자로 들어가는 두 개의 확률 분포 p, q가 있을 때. p가 "데이터의 실제 분포"라는 조건이 필요합니다(이 때 q는 모델이 추정한 값 or 분포). 즉, 데이터의 실제 분포를 알고있다고 가정하는 것이죠.  
  그리고 MLE가 KL과 같아지는 이유는, MLE도 "충분한" 데이터가 주어진다면, 모델의 추정은 결국은 p분포(위에서 말한 실제 분포)와 같아지기 때문입니다. 왜냐하면, 영석님께서 설명해주시 듯 최대가능도를 가지고 학습하면 실제 분포에 가까이 가기 때문입니다.
- 라고 하시는데, 아직 KL divergence는 제대로 공부를 안 해서 무슨 의미인지 모르겠음. 두 확률분포의 정보량 차이 아닌가..

## miscellaneous
- 푸리에 변환을 공부해야 한다. gnn과 연관이 있을 뿐더러, gan artifact나 영상처리에선 기본임.
- prml을 좀 더 빡세게 해야 함. chap 3 읽다 말았음.
- 대회 2개를 병행하는 중이라 직문수 진도가 안 나가고 있음. 주말에 빡세게 해야 할 듯..
- d2lai recsys(chap 17) 수요일까지 17.4 읽어야 함. 웬만하면 17.6까지 하자.
- 프리드버그도 지금 안 보고 있음.. 직문수가 먼저라고 생각함.
- 라그랑주 승수법을 공부해야 한다.

## feeling
- 나름대로 ml 공부를 많이 했다고 생각했는데, 의사역행렬과 선형회귀의 관계는 이번에 처음 알았고, rnn 역전파인 bptt도 강의가 밀려 아직 제대로 공부하진 않았지만 제대로 공부할 기회가 생긴 것 같아 기분이 좋다. 항상 구글링으로만.. 야매로 공부하다가 수준 높은 제대로 된 코스웍을 밟으니 정말 지식이 쌓이는 기분이다.
- 공개된 곳에 밝히긴 어렵지만 오늘 기분 좋은 일이 있었다. 더 열심히 해야겠다.
- 5일밖에 안 지났는데 2주는 지난 것 같다.
- 일주일 동안 카페에만 하루종일 있었는데, 제대로 된 장소를 잡는 게 좋을 것 같다.
- 대회가 겹쳐서 다음 주는 아주 바쁠 것 같다. 다음 주 목요일에 끝나는데, 고생을 좀 해야할 것 같다..