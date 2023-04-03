---
layout: post
title:  Factorization Machines (ICDM'10)
categories: dl
---
## Factorization Machines (ICDM'10)
- [https://ieeexplore.ieee.org/document/5694074](https://ieeexplore.ieee.org/document/5694074)
- 왜 이름이 Factorization Machine 인가?
  - polymonial SVM 에서 directly optimized 되었던 $w_{ij}$ 를 $\langle v_i, v_j\rangle$ 로 모델링했기 때문
    - $W \approx VV^\intercal$ - factorization!
  - 이렇게 해서 high sparsity condition 에서도 잘 fitting 할 수 있게 되었음
    - 여기서 sparse 하다는 것은, 일반적으로 $U \times I$ matrix 가 sparse 하다는 의미라기보단 변수의 입장에서 sparse 하다는 것을 의미한다
      - 변수 개수가 너무 많기도 하고, 각 데이터포인트에 0이 많다. $w_{14}$ 를 모델링하고 싶은데, $x_1, x_4$ 둘 다 1인 데이터가 많지 않다는 것이다 - sparse, Fig.1
    - 논문에서 예시를 들어 설명하고 있는데, 그 부분이 이 논문의 핵심인 것 같음
      - 3-A-3) Parameter Estimation Under Sparsity 부분
- 시간복잡도를 $O(n^2k)$ 에서 $O(nk)$ 로 줄였다는 게 나오는데
  - 첫번째 부분 그러니까 $\sum_{i=1}^n\sum_{j=i+1}^n$ 이 부분을 $\sum_{i=1}^n\sum_{j=1}^n$ 으로 식변형하는 부분이 핵심
  - 이렇게 함으로써 겹치는 형태가 생기고, 그러면서 $O(nk)$ 로 시간복잡도가 줄어들 수 있음
- 논문에선 2-way 만 보여줬지만 3-D 에서 나오듯 d-way 도 가능함
  - 수식 마지막 부분이 내적하는 부분임
    - $\sum_{f=1}^{k_l} \Pi_{j=1}^l v_{i_j, f}^{(l)}$
    - 다 곱하고 다 더한 거임
- SVM 과 비교하는 게 나오는데, 핵심은 $W$ 의 factorization 이다
- dual form, primal form 이 뭐지? SVM 을 대충 공부해서 잘 모르겠다
  - 커널 메소드는 아는데.. mml 을 다시 펼쳐야 할 것 같다
  - mml 최적화 이론 쪽도 좀 가라로 넘겼는데.. 방학 때 다시 봐야겠다 - 당장은 시간이 너무 없다 ㅠ
- PITF, FPMC, PARAFAC 는 처음 들어보고 SVD++ 는 들어보긴 했는데 기존 SVD 와 뭐가 다른지 잘 모르겠다
- 왜 논문 제목이 factorization machine-'s' 일까? 왜 복수형이지..?

---

first draft: 2023.04.03 19:05