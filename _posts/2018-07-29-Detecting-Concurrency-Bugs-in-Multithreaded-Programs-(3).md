---

title : "Detecting Concurrency Bugs in Multithreaded Programs (3)"
date : 2018-07-29
tags: Multithread
category: Multithread Programming

---

# Intro

---

오늘은 Multithread를 사용했을 때 발생하는 버그 패턴 중 빈번히 발생하면서 상대적으로 어렵지 않은 쪽에 속하는 'Deadlock'에 관해 간단히 이야기를 해보려 한다.
  
    
      
      



# Deadlock

---

## Deadlock이란?
> Deadlock  occurs when each of a set of threads is blocked, waiting for another thread in  a set.

## Finding Deadlock is difficult?
이번 파트에서는 Deadlock을 찾아내는 것에 대한 어려움을 간단히 논해보고자 한다.
우선, Deadlock은 specific한 thread scheduling 상황에서만 발생하기 때문에 패턴화를 통한 탐지가 어렵다. 또한, system program에는 lock의 개수가 너무 많아서 deadlock이 발생했을 때 어느 시점에서 잡아냈는지 정확히 파악하기 어렵다. 게다가 concurrency한 상황을 만들어내기 위해 lock을 i-node별로 만들곤 하는데, 이 경우 lock마다 종류가달라서  deadlock이 발생한 당시의 상황을 파악하는 것이 더 어려워진다.

## How to avoid bugs?
Deadlock의 특징에 따르면 deadlock이 발생하지 않는 완벽한 상황을 보장하는 것은 어렵다.
하지만, 몇 가지 방법을 사용하면 그것을 사용하는 것만으로 꽤 많은 수의 deadlock을 예방할 수 있다.
- Use recursive locking  
(lock을 두 번 잡는 것을 허용한다. 두 번 잡아으면 두 번 풀게끔 설계한다.)
- Lock ordering (partial order for locks)
lock을 type별로 분류해서 우선순위를 정의하는 방법으로, resource deaklock을 예방할 수 있다.
- Locking에 대한 side effect(예: lock을 들고 나옴)가 생기는 경우 주석을 잘 쓰자.
