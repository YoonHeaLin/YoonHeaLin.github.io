---

title : "Google Cloud Summit 데이터를 활용한 머신러닝과 IoT(2)-빅데이터 & AI 무기로 비즈니스 성공적으로 이끌기!"
date : 2018-10-25 10:00:00 + 0000
tags: seminar
category: seminar

---

# Intro
Google Cloud Summit 2018에 다녀왔다. "데이터를 활용한 머신러닝과 IoT" Track을 참관하였고, 총 6번에 나누어 진행된 각 세션의 내용을 공유하고자 한다. 이번 포스트에서는 **"데이터를 활용한 머신러닝과 IoT(2)-빅데이터 & AI 무기로 비즈니스 성공적으로 이끌기!"** 발표 내용을 정리하였다.

***

# 빅데이터 & AI 무기로 비즈니스 성공적으로 이끌기!
미래 가치가 높은 기업으로 선정된 기업들의 공통점은 방대한 양의 데이터 수집과 지능화를 이미 활용하고 있다는 것이다. 따라서 매일 쏟아지는 방대한 데이터를 저장, 분석, 활용하는 것이 미래 비즈니스의 판을 완전히 바꿀 것으로 예측되고 있으며, 이를 위한 환경 구축부터 혁신이 시작될 것으로 전망하고 있다. (업계에서는 AI를 도입하지 않는 기업은 10년안에 망할 것이다라고 예측하고 있다.)

***

## Ⅰ 왜 AI 도입이 어려운가
그렇다면 비즈니스에 AI 도입이 어려운 이유는 무엇일까? 다양한 이유를 종합하여 정리하면, 다음과 같다.

### 1. 데이터의 부족
### 2. 데이터가 많더라도 학습할 수 있는 컴퓨팅 리소스 부재
### 3. 전문가의 부족

![Complex & Time Intensive](/assets/images/2018-10-25-Google-Cloud-Summit/2/1.png){: width="320" height="250"}

그러나 최근 수많은 데이터를 모으고 정제하는 OSS/CS가 등장하고, GPU 등의 등장으로 컴퓨팅 파워가 강력한 환경이 제공되면서 사실상 첫 번쨰와 두 번째 문제는 거의 해결되었다고 볼 수 있다. 따라서 남은 문제는 "전문가의 부족"이다.

![TPU](/assets/images/2018-10-25-Google-Cloud-Summit/2/2.png){: width="320" height="250"}
![Chart](/assets/images/2018-10-25-Google-Cloud-Summit/2/3.png){: width="320" height="250"}


***

## Ⅱ 그래서 Cloud AutoML
그래서 구글은 Cloud AutoML을 해결 방안으로 제시한다. 구글의 AutoML은 또 하나의 Cloud Service로, 머신 러닝을 as a service로 제공하는 형태이다. 전통적인 머신러닝 workflow와 구글의 AutoML workflow를 아래의 사진에서 비교하였다.

![Traditional ML Workflow](/assets/images/2018-10-25-Google-Cloud-Summit/2/4.png){: width="320" height="250"}
![AutoML Workflow](/assets/images/2018-10-25-Google-Cloud-Summit/2/5.png){: width="320" height="250"}

구글의 AutoML은 전통적인 ML workflow의 복잡한 단계를 AutoML을 통해 제공하므로, ML 전문가가 아니더라도 빅데이터를 정제하고, 데이터를 학습하고, 의미있는 결과를 도출하고, 이를 분석할 수 있게 한다.

![Cloud AutoML](/assets/images/2018-10-25-Google-Cloud-Summit/2/6.png){: width="320" height="250"}

***

## Ⅲ AutoML 비즈니스 적용 사례
그렇다면, AutoML을 비즈니스에 어떻게 적용할 수 있을까? 발표자는 **"사용자들이 원하는 장면으로 갈 수 있는 영상 검색 서비스"** 를 제공하는 비즈니스를 사례로 들었다.

![영상 검색 서비스1](/assets/images/2018-10-25-Google-Cloud-Summit/2/7.png){: width="320" height="250"}

사용자들이 원하는 장면으로 갈 수 있는 영상 검색 서비스 구축을 위해서 사용된 플랫폼은 **Cloud AutoML Vision** 이다.

![영상 검색 서비스2](/assets/images/2018-10-25-Google-Cloud-Summit/2/8.png){: width="320" height="250"}

Cloud AutoML Vision을 통해 비즈니스를 하는 기업은 다음과 같은 서비스를 제공할 수 있다.

![영상 검색 서비스3](/assets/images/2018-10-25-Google-Cloud-Summit/2/9.png){: width="320" height="250"}

***

## Ⅳ 베스빈: 클라우드 엔지니어 기업
**"SI(System Integraion)에서 CSI(Cloud Service Integration)로"**
CSI는 새로운 개념의 SI라고 생각하면 될 것 같다. 기업의 AI/BigData 도입을 위해 컨설팅, 플랫폼 구축, 기술지원, 운영을 지원을 제공한다는 점에서 시대의 흐름에 맞춰 탄생한 SI인 것이다. 베스빈은 CSi 기업 중 하나로, 이번 포스트 내용을 발표하신 분도 베스빈 직원 분이셨다.
