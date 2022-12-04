---
layout: post
title:  Machine Learning Meetup - Incheon
categories: seminar
---

<style>
  table {
    width: 100%;
    border-top: 1px solid #444444;
    border-collapse: collapse;
  }
  th, td {
    border-bottom: 1px solid #444444;
    padding: 1px;
  }
</style>

# INDEX
- [1. JAX에 대한 소개: 효율적이고, 재현 가능한 ML framework](#1-jax에-대한-소개-효율적이고-재현-가능한-ml-framework)
- [2. 블록체인 데이터와 머신러닝으로 만들어내는 금융업계의 고객 가치](#2-블록체인-데이터와-머신러닝으로-만들어내는-금융업계의-고객-가치)
- [3. GCP와 TFX로 쉽게 MLOps 시작하는 법](#3-gcp와-tfx로-쉽게-mlops-시작하는-법)
- [4. 텐서플로우로 만나는 Graph Neural Network](#4-텐서플로우로-만나는-graph-neural-network)
- [5. 후기](#5-후기)

---

- 아마 난생 처음 참여해본 세미나
- 8월 29일 쯤 대학생 인공지능 오픈채팅방에서 머신러닝 세미나를 한다는 소식을 들었다 ([festa.io](https://festa.io/events/2562))
- 8월 31일에 링크에 있는 오픈채팅방에 들어갔고, 9월 17일 행사에 참여했다
- 11월 19일에 한 devfest 와 멀지 않은 곳에서 한 행사였다
- 이때 잠을 거의 안 자고 갔었는데 그래서 정말 힘들었다

## 1. JAX에 대한 소개: 효율적이고, 재현 가능한 ML framework
- JIT
  - Just in time compilation
  - 코드 내의 비효율적인 연산 간소화
    - Arithmetic simplifications
    - Broadcast minimization
    - Better use of intrinsics
    - Remove redundant ops or op pairs
    - Hoist chains of unary ops ay Concat/Split/SplitV
  - graph 내의 불필요한 memory allocation 확인 및 제거
    - gpu 의 bandwidth 는 가장 부족한 resource 중 하나임  
    -> cpu에서 성능 향상은 크지 않음
- kaggle 의 tf-jax-tutorials-part1 노트북
  - Aakash Nain - GDE 커뮤니티 tech-talk 의 presentation 도 볼 만하다
- JAX?
  - ||TensorFlow|JAX|PyTorch|
    |:---:|:---:|:---:|:---:|
    |활용 목적|산업/연구|연구|연구|
    |graph 특성|Static<br>(Dynamic 은 느림)|Static<br>(Dynamic 은 느림)|Dynamic<br>(Static 은 불편)|
    |속도|빠름|빠름|느림|
    |코딩난이도|중간|중간|낮음|
    |기반<br>코드베이스|거의 없음|구글|아주 많음|
    |huggingface<br>model|4869|7136|46530|

## 2. 블록체인 데이터와 머신러닝으로 만들어내는 금융업계의 고객 가치
- NFTbank
- [link](https://www.visualcapitalist.com/cp/big-tech-revenue-profit-by-company/)
  - quarterly income statements

1. 공헌 이익
    - 모델 AB 테스트를 통해 모델 성능이 좋아지는 만큼 바로 공헌 이익이 계산되는 파이프라인
2. 생산성
    - 머신러닝 프로젝트는 너무 비쌈  
    제한된 리소스로 최대한 가치 있는 머신러닝 프로덕트를 만들어야 함
3. 품질
    - 머신러닝 모델이 비즈니스 문제를 해결하여 공헌이익을 가져다준다면,  
    품질 관리 활동은 수익 창출 활동임

## 3. GCP와 TFX로 쉽게 MLOps 시작하는 법
- Two key GCP services for AI
  - dataflow
    - google's compatible solution to apache beam
    - suitable to handle a large amount of data processing
    - optionally accelerators can be allocated
    - scalability out-of-the-box
  - vertec ai
    - gogole's all-in-one solution for ai
    - kubeflow v2.x pipeline, training, serving(online/batch), endpoint, model registry, artifact store, feature store, automl, datasets
    - scalability out-ot-the-box for both training and serving
- semi-auto pipeline trigger / deployment with github action
  - github action 을 통해 TFX pipeline 을 실행 가능 (trigger)

## 4. 텐서플로우로 만나는 Graph Neural Network
- AI Wave: deep learning
  - imagenet (2012)
  - alphago (2016)
  - attention / transformer (2017 / 2018)
  - xlnet / t5 (2019)
  - alphastar (2019)
  - gpt-3 (2020)
  - pathway (2021)
  - palm and minerva (2022)
- common sense
  - fields with same attributes
    - data cn be projected on 1/2-dim
      - image, sequence, series, ...
    - distance can be well defined on the data
      - in other words, deterministic euclidean distance between datum
- data relations in real world
  - data without physical constraints
  - we already know so many examples: networks
    - citation network
    - social network
    - transportation network
    - molecular structure / reactions
  - network
    - representation of relationship
- physical explanation about gnn
  - information extraction from limited data
    - find 'hidden information' in the system
    - use the information to do logical tasks
    - how to find the hidden information from data?
  - deep neuralnet
    - latent space: hyperspace to project data
    - deep neuralnet is one method to build the discrete, nonlinear space
  - Encoder
    - distort the latent space into out own projection with training
    - as a result, we get the distorted hyperspace
  - decoder
    - reduce the latent space dimension size to the target dimension
    - from the projected space
  - inference
    - project data to the hyperspace to get the information
- pinSAGE / taking graphSAGE to extreme
  - 3 billion nodes / 18 billion edges
  - pinterest user recommendation for new posts
- tools on the table (July 2022)
  - NSL (neural structured learning)
  - spektral
  - jraph
  - DGL
  - StellarGraph
  - Graph Nets
  - TensorFlow GNN (google)
- tensorflow gnn
  - still on super early stage
    - direct port of google internal package
    - requires tensorflow 2.7+
  - heterogeneous graph type
    - graph can have different types of nodes and edges
  - graphtensor type
    - broadcast / pooling options
    - prebuilt convolutions
  - pre-baked high-lebel gnn apis with
    - sample graphs / datasets
  - TF-GNN: Graph Neural Networks in TensorFlow
- Transformer is spacial case of GNN?

## 5. 후기
- 끝나고 밥을 줬다 - 치킨/피자
  - 이때 거의 가사 상태였다 잠을 못 자서
  - 이때도 비슷한 실수를 했었구나..
- 부캠 시작 전에 간 행사였다
  - 부캠 언제 시작했는지 보려고 이전 기록들을 들춰보는데 팀원들 관련 이야기가 하나도 없다.. 이땐 어떻게 생각했는지 보려 했는데
  - ...
  - 여기에 지금까지의 부캠을 회고했다. 감상 위주로  
  방금까지 있었다
    - 너무 일기 같아서 그냥 private 으로 옮겼다
    - 공개된 곳에 올려서 lv1, lv2 팀원들이 내가 어떤 생각을 하고 있는지 다 알았으면 좋겠다는 마음도 있었다
      - 근데 뭐 링크를 주고 읽으라고 할 수도 없고
    - 부질없다
  - 대회에나 집중하자-

---

first draft: 2022.12.05 05:15