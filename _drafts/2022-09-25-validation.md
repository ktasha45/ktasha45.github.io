회귀 문제를 생각해버자. 그리고 모델의 학습이라는 것을, train 데이터의 모분포를 잘 추정하는 것이라 생각하겠다. 이때 잘 추정한다는 것은 말 그대로 잘, 즉 추정된 분포와 모분포의 차이가 거의 없게 추정하는 것을 의미한다. train data는 모분포에서 노이즈가 추가된 데이터라 생각하겠다.  
보통 validation은 train에서 떼어져 나오기에 train와 모분포가 같다. 따라서 validation은 train 데이터로 모델을 학습시킬 때, 모델이 train data에 overfitting되는 것을 막아준다. validation이 train과 같은 분포에서 추출된 값이 아니라면, train이 노이즈에 overfitting되는 것을 막을 수 없을 것이다.  
모델이 원래 분포를 잘 추정할수록 train loss와 validation loss는 같아질 것이다. train loss가 수렴한 상태에서 validation loss가 train loss와 비슷하다면 우리는 학습이 잘 되었다고, train data의 모분포를 잘 추정했다고 평가한다. 그리고 우리는 
일반적으로 test acc는 validation acc와 같을 것이라 기대한다. 왜냐하면   
하이퍼파라미터 튜닝은 무엇인가? train data의 분포를 잘 추정할 수 있도록 하는 최적의 하이퍼파라미터를 고르는 작업이다. 이때, val loss가 작아도 train-val gap이 크다면 로버스트하다 할 수 없다. validation에 과적합되어있을 수 있기 때문이다.  
Test data를 train data에서 분포가 조금 shift된 형태라 생각해보자. (예를 들어, train은 A사의 현미경으로 찍은 사진이고, test는 B사의 현미경으로 찍은 사진이다)이때, 만약 test data를 validation으로 사용하면 하이퍼파라미터 튜닝을 할 때 적은 양의, 그리고 노이즈가 있는 test data에 과적합될 수 있다. (특히 earlystopping을 사용할 경우에 그렇다. 이는 이후 문단에서 이야기한다) validation 의 존재는 이를 방지해주며, train data의 분포를 가장 잘 그리고 robust하게(validation loss와 train loss의 gap으로 평가) 추정할 수 있는 하이퍼파라미터를 찾게 해준다. 하지만 train과 test의 분포가 완전히 같다면, 이를 고려할 필요가 없다. 이때 test는 train 분포에서 추출된 값이다. 따라서 test data가 validation 데이터와 분포가 같아지고, 굳이 validation을 만들 필요가 없어진다. 왜냐하면, validation을 만드는 이유는 곧 test 데이터는 train 데이터와 약간 다르고, 노이즈가 추가된 형태라 생각하기 때문에 원래 train 분포를 최대한 로버스트하게 찾기 위함이기 때문이다. 그런데 test 데이터가 train 데이터의 모분포에서 추출되었다면, 필요가 없어진다. 그냥 test 데이터와 train 데이터로 train-test의 모분포를 찾으면 되는 것이다.  
근데 만약 test data와 train data가 분포가 같다면 어떨까. 그럼 사실 vlaidation이 필요가 없다. 왜냐하면 test가 validation의 역할을 잘 수행할 수 있기 떄문이다. 단지 제대로 된 성능 평가가 어려워질 뿐이다. train-test 데이터는 한정된 양인데, 이때 모델은 train+test에 과적합될 수밖에 없다. 다만 valid를 사용한다고 해도, 결론적으로는 train 데이터에 과적합된다. 결론적으로, test는 모델 성능 평가에 사용되고 편향된 결론을 도출하지 않기 위해서는 train 과정에 사용되지 않은 독립적인 데이터여야 한다.
validation은 왜 존재하는가. 결론적으로, 모델의 성능 평가를 편향되지 않게 하기 위함이다. 목적에 따라 다르다. 만약 이 모델을 실제로 쓴다고 한다면 test 데이터에 적합되게 하면 안 된다. 따라서 validation을 두는 것이다. train과 test 분포가 같다고 해도 마찬가지이다. 공정한 성능 평가를 위해 validation은 존재한다. 하이퍼파라미터 튜닝을 test로 한다면 test 성능은 좋겠지만 오히려 test에 적합될 수 있다. 하지만, valid를 둬도 valid에 적합되는 것과 test에 적합되는 것과 크게 다르지 않다. 왜냐하면 모분포가 같기 때문이다. 따라서 train-test가 추출된 모분포가 같다면 validation을 두는 데 큰 의미가 없다. validation을 둔다고 해도, test에 과적합될 것이기 때문이다. 하지만, 성능 평가의 측면에서는 의미가 있다. test 데이터로 hpo를 한다면 test 데이터에 대해 성능이 높아질 수밖에 없고, 이는 편향된 결과를 도출할 수 있다. valid와 test의 분포가 같아도, valid를 두는 것은, 편향된 결과를 도출하는 것을 방지할 수 있다. 이미 본 데이터에서 acc를 측정하는 것은 편향된 결과를 도출할 수밖에 없다.

머신러닝에서 모델을 학습시킬 때는 robust한 모델을 만들기 위해 주어진 train 데이터를 train-val으로 쪼갠 뒤 그것만을 가지고 validiation 성능을 높이는 형식으로 최적의 하이퍼퍼라미터를 선정한다.  
Test 데이터를 validation으로 사용해버리면 하이퍼퍼라미터 튜닝 과정에서, 그 하이퍼파라미터 set이 test 데이터에 overfitting될 수 있어서 robustness가 깨질 수 있다. 이렇게 학습된 모델은 주어진 test data에서 성능이 좋을지는 몰라도, 분포가 조금만 다른 데이터가 들어오면 성능이 떨어질 수 있다.  
따라서 test data는 단지 모델의 최종 성능을 ‘측정’할 뿐, 검증에 사용될 순 없다.
이 대회에서는 test data를 사전에 주었고, 그 test data에 대해서 성능을 높이는 것이 과제였다. 일반적인 대회에서는 public test data를 준 뒤, private test data로 점수를 측정한다(dacon 등). 결론적으로 이 대회는 일반적인 대회와는 다르다 생각했고, 우리 팀은 test data를 validation 용으로 사용해서 test data에서 가장 좋은 성능을 보이는 모델을 만들기로 방향을 잡았다.


earlystopping은 왜 있는가?  
사실 과적합을 막기 위해선 데이터를 증가시키거나 weight decay 같은 방법론을 사용해야 해결할 수 있다.  
earlystopping은 미봉책인가? validation에 과적합될 수 있다고 생각한다.




train 데이터를 늘리고 validation을 줄였더니 test 성능이 높아진다면, 어떤 걸 의미하는 건가
거대 모델이라 train 데이터에 과적합되어있다가, 늘어나니 과적합이 어느정도 완화된 것으로 생각할 수 있다.




train-test
만 있을 때는
train으로 계속 학습시키면서, test acc가 어떻게 변하는지 추이를 본다.
근데 이렇게 하면 안된다
한 번만 저렇게 하는 거라면 괜찮다.
하지만 하이퍼퍼라미터 튜닝을 한다면, test 데이터에 오버피팅된다.
따라서 validation을 둔다
보통 train-test는 본푸가 약간 다르다.
train-val은 분포가 같다
따라서 overfitting 을 방지할 수 있다.


---
아 이거 어떻게 정리해야 되지... 생각 정리가 잘 안 되는 느낌 무한루프에 빠진 것 같음