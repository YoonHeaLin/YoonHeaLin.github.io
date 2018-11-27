---

title : "Muchine Learning 알고리즘 - Linear Regression(선형 회귀 분석)"
date : 2018-11-27 10:00:00 + 0000
tags: Muchine_Learning
category: Muchine Learning

---

# Intro

Regression(회귀 분석)에 대해 정리하였다.

***

# Linear Regression(선형 회귀 분석)

- 지도학습
- 예측: 기존 데이터를 기반으로 생성된 회귀 모델을 이용하여, 새로운 데이터가 들어왔을 때 예측하는 문제
- 독립 변수와 종속 변수가 연속형 변수일 때 사용(설명변수가 범주형이면, 이를 더미 변수로 변환하여 적용해야함)

## Ⅰ Linear Regression(선형 회귀 분석)이란?
Linear Regression은 변수와 변수 사이의 관계를 알아보기 위한 통계적 분석 방법으로, 독립 변수(Independent varibale)가 종속 변수(Dependent varibale)에 미치는 영향력을 예측하기 위해 사용한다.

### 1. 독립 변수와 종속 변수
- 독립 변수(Independent varibale): 종속 변수에 영향을 미치는 변수 X
- 종속 변수(Dependent varibale): 분석의 대상이 되는 변수 Y
- 산포도(Scatter diagram): X와 Y의 통계적 관계를 그림으로 나타낸 것

### 2. 선형 회귀 분석 분류
종속 변수와 독립 변수의 개수에 따라 선형 회귀 모델의 종류를 분류하면 다음과 같다.
![Regression의 종류](/assets/images/2018-11-27-Linear-Regression/1.png){: width="640" height="500"}

## Ⅱ 회귀 분석의 4가지 가정
==*추후 업데이트 예정*==
1. 선형성: 독립 변수와 종속 변수 간의 관계 분포는 선형성을 가진다.
2. 독립성: 설명 변수와 다른 설명 변수 간의 상관 관계가 적다.
3. 잔차의 등분산성: 잔차가 특정한 패턴을 보이지 않는다.
4. 잔차의 정규성: 잔차가 정규분포이다.

## Ⅲ 회귀 모형
==*추후 업데이트 예정*==
㉠

### 1. Simple Regression Analysis(단변량 단순 회귀 분석)
선형 회귀 분석은 주어진 데이터를 대표하는 하나의 직선(**회귀선**)을 찾는 것이며, 이 선을 함수로 표현한 것이 **회귀식** 이다. 단변량 단순 회귀 분석은 독립 변수 X와 종속 변수 Y를 이용하여, ㉡와 같은 하나의 선형 관계식으로 표현되며, ㉡회귀식을 그래프로 표현하면 아래와 같다.

==*그래프 그림 추가*==

### 2. Multiple Regression Analysis(단변량 다중 회귀 분석)
==*추후 업데이트 예정*==

## Ⅳ 선형 회귀 함수의 추정

### 1. Least Square Method(최소제곱법)
선형 회귀 함수를 이해하기 위해서는 **잔차(Residual)** 의 개념을 이해해야 한다. 추정된 선형 회귀 함수는 ㉠와 같다. 이때, 관찰값 ㉢과 예측값 ㉣가 일치하지 않는 것이 보통이고, 이러한 "관찰값 ㉢와 예측값 ㉣간의 차이"를 "잔차"라고 한다. 잔차는 ㉤로 표시한다.
㉥

선형 회귀 분석은 최소제곱법을 사용하여 선형 회귀 함수를 추정하며, **최소제곱법** 은 잔차의 제곱의 합(SSE: Sum of squared errors of prediction, ㉦)이 최소가 되게 하는 직선을 회귀선(데이터를 대표하는 하나의 직선)으로 한다는 것을 의미한다.

### 2. 회귀 분석을 한다는 것
결론적으로 회귀 분석을 한다는 것은 데이터, 독립 변수 X, 종속 변수 Y를 지정하고, 최소제곱법을 이용해 회귀식 ㉡에서 회귀계수 ㉧(Regression coefficient, 계수의 크기와 부호가 독립변수 X가 종속 변수 Y에 주는 영향력을 결정)와 ㉨ 회귀계수(또는 y절편)를 구하는 과정을 의미한다.

## Ⅴ 회귀 유의성 검증





























# 참고
https://m.blog.naver.com/PostView.nhn?blogId=istech7&logNo=50152984368&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F
http://cau.ac.kr/~orist/2006_2/STAT/ch16_2p.pdf
