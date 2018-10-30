---

title : "Google Cloud Summit 데이터를 활용한 머신러닝과 IoT(6)-비즈니스를 위한 간편한 머신러닝"
date : 2018-10-25 10:00:00 + 0000
tags: seminar
category: seminar

---

# Intro
Google Cloud Summit 2018에 다녀왔다. "데이터를 활용한 머신러닝과 IoT" Track을 참관하였고, 총 6번에 나누어 진행된 각 세션의 내용을 공유하고자 한다. 이번 포스트에서는 **"데이터를 활용한 머신러닝과 IoT(6)-비즈니스를 위한 간편한 머신러닝"** 발표 내용을 정리하였다.

***

# 비즈니스를 위한 간편한 머신러닝
이 세션에서는 비즈니스를 위한 간편한 머신러닝을 다룬다. 비기술자가 아닌 사람들을 대상으로하는 서비스를 소개하는만큼, 머신러닝에 대해 매우 쉽고 차근차근 설명하는 것이 인상적이었다.

***

## Ⅰ 머신러닝이란?

(영상)

tensorflow playground([Tensor Playground 바로가기](https://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=4,2&seed=0.54893&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false))에 접속하면 ML test를 편리하게 시도해 볼 수 있다.

***

## Ⅱ 비즈니스 상황: 전문성 부족
이번 Google Cloud Summit의 컨셉을 "AI 민주화"로 제대로 잡은 것 같다. 아래의 사진은 사용자에 따라 제공되는 구글 클라우드 서비스인데, "Machine Learning API"는 비즈니스 맨들을 대상으로 서비스를 제공한다. **Machine Learning API는 Training을 할 필요가 없다!**

(사진-Google Cloud Platform의 ML 2번째 사진)

***

## Ⅱ 비정형 데이터 분석을 위한 API
>단일 REST API요청으로 사전에 학습된 모델 사용

비정형 데이터란 오디오, 이미지, 비디오, 텍스트 등을 포함한다. 비정형 데이터는 분석이 상당히 까다로우며, 데이터 사이즈가 (비디오와 같은 경우) 매우 크다. 구글은 사전 학습된 모델을 사용하여 일반적인 ML 학습을 수행하도록 지원한다.

**<Cloud Vision API>**
구글에서 제공하는 ML 모델 솔루션으로, 다음과 같은 서비스를 제공한다.
- 레이블 및 웹 감지
- OCR
- 로고 감지
- 랜드마크 감지
- 자르기 힌트
- 콘텐츠 감지

Cloud Vision API 데모 영상은 아래에서 볼 수 있다. 영상에 앞서, 다음과 같은 프로세스가 동작하는 것을 참고하면 도움이 될 것이다.

(사진-Cloud Vision API 데모)
(영상)

참고로 API는 파이썬에서도 호출 가능하다.

**<Cloud Translation API>**
이번 단락에서는 Translation API를 사용한 삼성전자의 사례("Translate with S Pen")를 소개한다. Translate with S Pen은 화면상의 단어나 문장을 인식해서 번역해주는 기능을 제공한다.

구글 클라우드를 선택한 이유
(사진-Why Google Cloud Traslation API)
- Larency: Translate with S Pen 서비스를 제공하게 위해서는 on-device 솔루션과 같이 빠른 응답이 중요
- Accuracy: 좋은 성능의 번역 엔진, 러닝 투 러닝
- Supports: 100여개의 언어 지원, 자동 언어 감지 기능 제공
- Simple Integraion: REST API 제공

**<Cloud Natural Language API>**
Netural Language API는 다음과 같은 서비스를 제공한다.
- 엔터티 추출
- 감정감지
- 구문 분석
- 콘텐츠 분류

Cloud Natural Language API 데모 영상은 아래에서 볼 수 있다.

(영상)

**<Cloud speech to text & text to speech API>**
Cloud speech to text & text to speech API 다음과 같은 서비스를 제공한다.
- STT
- TTS
- 자동언어감지
- 실시간 분석 지원
- 100개 이상의 언어 지원

**<Cloud Video Intelligence API>**
Cloud Video Intelligence API는 다음과 같은 서비스를 제공한다.
-비디오에서 라벨, 타임 스챔프 등의 엔티티 식별

Cloud Video Intelligence API 데모 영상은 아래에서 볼 수 있다.

(영상)

***

## Ⅳ 요약

(사진)

***

## Ⅴ 구글 클라우드 교육
구글에서 제공하는 강좌를 소개한다.

**Coursera**
[Coursera 바로 가기](http://www.coursera.org/googlecloud)

**추천 강좌**
Architecture with Google Cloud Platform Specialization

Data Enginnering on Google Cloud Platform Specialization

Machine Learning with Tensorflow on Google Cloud Platform Specialization
