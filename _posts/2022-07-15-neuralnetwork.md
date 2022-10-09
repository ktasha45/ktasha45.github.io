---
layout: post
title:  How neural networks work
categories: dl
---

## how neural networks work
신경망은 어떻게 작동하는 걸까?  

loss function을 최적화시키며 가중치와 편향을 자동으로 검색하는 알고리즘(경사 하강법)과, 그렇게 형성된 신경망이 인상적인 성능을 보이는 작금의 상황은 단지 신비롭게만 보인다.  
신경망이 어떻게 작동하는지 명확히 설명하기란 너무 어렵다. 사람이 쓴 숫자를 분류하는 신경망의 작동 원리를 어떻게 이해할 수 있을까? 이해할 수 있는 방법은 무엇일까? 신경망이 학습하거나 추론하는 원리와 원칙들을 고려할 때 더 나은 신경망을 제작할 수 있을 텐데 말이다.  

딥러닝 관련 인터넷 글들을 보면 `블랙박스`라는 말이 많이 나온다. 유의미한 결과가 나오긴 하지만, 무엇을 근거로 어떻게 그런 결과가 나왔는지 알 수가 없다는 것이다. 인간의 사고 또한 블랙박스일 것이다. 우린 아직 뇌(뉴런)의 화학적, 물리적(전기적) 작용이 어떻게 논리적 사고와 기억으로 이어지는지 알지 못하니까 말이다.  

신경망은 정답을 찾는 기계가 아니다. 정확히는 입력과 출력이 주어졌을 때, 입력이 어떻게 출력을 도출하는지 그 방법을, 즉 입력이 주어졌을 때 어떻게 원하는 출력을 낼 수 있을지 학습한다. 즉, \\(x\\)와 \\(y\\)가 있을 떄, \\(f(x)=y\\)인 함수 \\(f\\)를 찾아내는 것이 신경망이 하는 일이다.  

그렇다면 왜 네트워크가 어떻게 작동하는지 이해하기 어려운 것일까? 왜 네트워크의 작동 과정은 불투명한 것일까? 그 이유는 아마 네트워크가 자동으로 학습되기 때문일 것이다. AI 연구 초장기의 연구자들은, AI를 구축하려는 노력이 지능의 원리와 더 나아가 인간의 두뇌를 이해하는 데에 도움이 되기를 바랐다. 하지만 지금의 우리는, 결국 뇌도, 인공지능도 명확히 이해하지 못하고 있다.  

최근에 이와 관련된 흥미로운 설명을 읽어서, 정리해보려 한다.

## perceptron
신경망의 작동 원리에 대해 생각해보기 전에 먼저 퍼셉트론에 대해 생각해보자. 퍼셉트론은 입력에 가중치를 매겨 결정을 내리는 장치이다. 이때 변수는 증거(evidence) 혹은 특징(feature)라고도 불린다. 책의 예시를 들어보자, 다가오는 주말 페스티벌이 열린다고 가정했을 때, 당신은 세 가지 요소를 가늠해 페스티벌에 갈지 말지 결정해야 한다.  

1. 날씨가 좋은가?
2. 같이 갈 수 있는 가족이나 지인이 있는가?
3. 그 날 마감인 과제가 있는가?

세 가지 요소를 변수 \\(x_1, x_2, x_3\\)라고 표현할 수 있다. 날씨가 더할 나위 없이 좋다면 \\(x_1\\)의 값은 1일 것이고, 그럭저럭 나쁘지 않다면 0.7 정도의 값일 것이다.  
그리고 당신이 날씨에 민감하거나, 같이 갈 지인이 없다면 절대 혼자 그런 것에 가지 않는다면, 그 특정 요소는 아마 당신의 결정에 강력하게 반영될 것이다. 그리고 그런 식으로 반영되는 정도를 수치로 표현한 것이 가중치, \\(w\\)이다.  
그래서 이때의 가중합<sup>weighted sum</sup>인 \\(\sum_jw_jx_j\\)이 역치<sup>threshold</sup>보다 큰지 작은지에 따라 0 또는 1의 값을 출력한다. 이때의 역치와 가중치를 이 퍼셉트론의 파라미터<sup>parameter</sup>라고 표현한다.

$$\text{output}=
\begin{cases}
0, & \text{if} \quad {\sum_jw_jx_j \le \text{threshold}} \cr
1, & \text{otherwise}
\end{cases}$$

threshold를 편향<sup>bias</sup>로 치환해서 식을 간단히 나타내곤 한다. \\(\sum\\)도 벡터 내적으로 간략하게 표현할 수 있고, 그 결과는 다음과 같다.  

$$\text{output}=
\begin{cases}
0, & \text{if} \quad {w \cdot x + b \le 0} \\
1, & \text{otherwise}
\end{cases}$$

이렇게 표현하면 편향은 퍼셉트론의 출력이 1이 되기 쉬운 정도로 생각할 수 있을 것이다. 생물학적인 용어로, 편향은 퍼셉트론이 얼마나 활성화<sup>*fire*</sup>되기 쉬운지를 나타낸다.

## toward deep learning
신경망에서 하나의 뉴런은, 따라서 하나의 퍼셉트론으로서 해석될 수 있다. 이미지 픽셀을 신경망의 입력으로 하고, 신경망의 출력으로 하나의 뉴런을 사용해 사람인지 아닌지 이진 분류를 해야 한다고 해보자.  

학습 알고리즘(경사 하강법)을 사용하지 않고 이 문제를 풀고 싶다. 그러기 위해선, 가중치와 편향을 사람이 적잘한 값으로 직접 선택해 신경망을 직접 설계해야 할 것이다. 생각해볼 수 있는 것은, 문제를 하위 문제<sup>subproblem</sup>로 나눠보는 것이다: '왼쪽 위에 눈이 있는가?', '이미지의 중간에 코가 있는가?', '머리 쪽에 머리카락이 있는가?' 이런 질문들에 대한 답이 긍정적이라면, 아마 그 이미지는 사람일 것이다. 그 반대라면 아닐 것이다.  

물론 이 방법은 무식한 방법이다. 딱 봐도 결함이 있어 보인다. 사람이 대머리인 경우 머리카락이 없을 수도 있다. 또한 사진에 있는 사람의 얼굴이 항상 정면으로 찍히는 것도 아니다. 하지만, 이런 식으로 하위 문제를 풀 수 있다면 그 문제에 대한 답의 조합으로 얼굴을 탐지하는 신경망을 구현할 수 있을 것이다.  

그리고 또, 하위 문제도 당연히 분해될 수 있다. '이미지의 왼쪽 위에 눈이 있는가?'라는 문제는, '눈썹이 있는가?', '속눈썹이 있는가?' 등의 하위 질문으로 또 분해될 수 있다. 물론 이런 질문들은 위치 정보뿐만 아니라, '그 눈썹이 이미지의 왼쪽 위에 있으면서 또 홍채 위에 있습니까?' 등의 정보를 더 포함해야 한다. 다만 이런 방법을 통해 '이미지의 왼쪽 위에 눈이 있는가?'라는 질문이 더 쉽고, 작은 문제들로 분해될 수 있다는 것이 중요하다. 복잡한 문제가 이런 식으로 더 작고 더 간단한 문제들로 분해되다 보면, 궁극적으로 우린 단일 픽셀의 수준에서 쉽게 해결할 수 있는 간단한 문제에 대한 답으로 '이미지의 왼쪽 위에 눈이 있는가?', '이미지의 중간에 코가 있는가?' 따위의 복잡한 문제를 풀어낼 수 있는 것이다.  

그래서 최종적으로, 이 이미지가 사람의 얼굴인지는, 단일 픽셀 수준에서 대답할 수 있는 간단한 질문들로 분해될 수 있다. 이처럼, 신경망의 초기 계층은 입력 이미지에 대한 단순하면서 **구체적인** 질문을 처리하고, 이후 계층은 더 복잡하고 **추상적인** 질문과 개념을 처리한다. 이것을 신경망의 추론 원리라고 볼 수 있으며, 이런 종류의 다층 구조를 심층 신경망<sup>deep neural network</sup>이라 한다.  

+ 시벤코 정리에 의하면 은닉층이 하나만 있어도 임의의 연속인 다변수함수를 근사할 수 있다. 따라서 위 설명은 그저 다층 신경망에서, feature의 추출을 이해하는 방식 중 하나라고 생각해야 할 것이다.

---
## **reference**
* [neural networks and deep learning](http://neuralnetworksanddeeplearning.com/)

---