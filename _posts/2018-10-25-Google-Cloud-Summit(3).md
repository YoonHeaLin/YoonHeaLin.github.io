---

title : "Google Cloud Summit 데이터를 활용한 머신러닝과 IoT(3)-데이터 사이언스 전문 지식 없이 Cloud AutoML속으로 깊이 들어가보기"
date : 2018-10-25 10:00:00 + 0000
tags: seminar
category: seminar

---

# Intro
---
Google Cloud Summit 2018에 다녀왔다. "데이터를 활용한 머신러닝과 IoT" Track을 참관하였고, 총 6번에 나누어 진행된 각 세션의 내용을 공유하고자 한다. 이번 포스트에서는 **"데이터를 활용한 머신러닝과 IoT(3)-데이터 사이언스 전문 지식 없이 Cloud AutoML속으로 깊이 들어가보기"** 발표 내용을 정리하였다.


# 데이터 사이언스 전문 지식 없이 Cloud AutoML속으로 깊이 들어가보기
---

"We will move from mobile...?"
"기업과 개발자들이 쉽게 접근해 빠르고 유용하게 AI를 사용할 수 있게 하겠다."

## AI를 도입하기 위해서는..
AI를 도입하는 것이 어려운 이유는 많은 부분이 갖추어져야 실질적인 효과를 볼 수 있기 때문이다. 그렇다면 어떤 조건들이 필요할까?
1. Infrasrructure at Massive Scale
Chips(CPUs, GPUs, TPUs), Enginds Storage, Network, Replication
2. Security
Software, Data, Hardware
3. Data
User data, Application data, Usage data, Batch, Streaming, Structured, Unstructured
4. Models
DNNs, CNNs, RNNs,... for vision, speech, language, video,...

## Google Cloud AI Platform
AI 도입을 위한 조건들을 고려했을 때, Google Cloud AI Platform이 제공하는 서비스가 얼마나 강력한지를 짐작할 수 있다.

(사진-Google Cloud AI Platform)

TPU

2. Security
3. Data
4. Models

## 어떤 종류의  ML 문제를 해결하기 원하는가
개냐 고양이냐? 라면 오픈소스로 가능하지만, 고양이의 이름이 뭐냐라고 한다면, 직접 모델을 만들어야 한다.

### Google 비전 API 데모
구글 클라우드 사이트에서 직접 test 가능
- Drag & Drop으로 test 가능
- 일반적인 정보는 API를 호출하는 것 만으로도 충분

### But 나만의 모델을 만들려면 어려움 발생

- CNN 단계

- Tensor 예시
