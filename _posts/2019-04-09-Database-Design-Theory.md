---
layout: post
title: "[Database] Design Theory(1)"
date: 2019-04-09
use_math: true
---

## 들어가며
Relational database schema을 design 하는 방법에는 여러가지가 있다. 하지만 적절하지 못한 design은 Update anomalies, Deletion anomalies 등 여러 문제를 발생시킨다. 특히, 주로 너무 많은 정보를 하나의 relation에 담는 경우 발생한다. 따라서 이 글에서는 한 relation을 여러 개의 relations 들로 나누는 법(Normalization)에 대해 정리할 것이다. 그 전에 그에 필요한 functional dependencies, superkey, key 등 여러 개념들을 살펴보자.

## Functional Dependencies
우선 Functional Dependencies 에 대해서 알아보자. Relation R 에 대한 Functional dependencies(FD) 의 정의는 다음과 같다. 만약 R의 두  tuple이 attributes $A_1,A_2,...,A_n$ 모두가 일치할 때, 다른 attributes 인 $B_1,B_2,...,B_m$ 들이 모두 일치한다면

$$ "A_1,A_2,...,A_n \text{ functionally determine } B_1,B_2,...,B_m" $$

이라고 하며 다음과 같이 표기한다.

$$ A_1,A_2,...,A_n \rightarrow  B_1,B_2,...,B_m $$

그림으로 보면 다음과 같다.

{% include image.html url='{{"/assets/img/post_2_1.png"| relative_url}}' description='A functional dependency on two tuples' alt='Functional Dependencies' %}

### Rules about Functional Dependencies
지금부터는 FD의 몇가지 특성들에 대해 살펴보자.
우선 두개의 sets of FD's S 와 T 가 주워졌을 때, 


## Key and Superkeys
Relation R 에 대해 attributes의 집합 $\{A_1,A_2,...,A_n\}$ 이 key가 될 조건은 다음과 같다.
1. $\{A_1,A_2,...,A_n\}$ 이 R의 모든 다른 attributes을 functionally determine 한다.
2. $\{A_1,A_2,...,A_n\}$의 어떠한 subset도 R의 모든 다른 attributes을 functionally determine 하지 못한다.

즉, 다시 말해서 Relation R의 모든 attributes 을 최소한(minimal)의 attributes 집단으로 functionally determine 할 수 있다면 그 집단을 R의 key라고 부른다.
그리고 *Superkey* 는 key을 포함하고 있는 attributes의 집단을 의미한다.
