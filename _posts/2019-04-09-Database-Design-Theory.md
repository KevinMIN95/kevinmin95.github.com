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

!['Functional Dependencies'](/assets/images/post/post_2_1.png){: width="400px"}


### Rules about Functional Dependencies
지금부터는 FD의 몇가지 특성들에 대해 살펴보자.

1. Equivalent FDs

우선 두개의 sets of FD's S 와 T 가 주워졌을 때, S 와 T를 만족하는 각각의 relations 들이 동일하다면, S와 T는 *equivalent*하다. 또한 만약 T를 만족하는 모든  relations 들이 S을 만족한다면 *S follows from T* 이다. 따라서 S와 T가 equivalent할 필요충분 조건은 S follows from T 이고 T follows from S 일 때다.

2. The Splitting/Combining Rule

$$ A_1,A_2,...,A_n \rightarrow  B_1,B_2,...,B_m $$

이면 오른쪽 항을 하나씩 나눌 수 있다.

$$ A_1,A_2,...,A_n \rightarrow  B_1, A_1,A_2,...,A_n \rightarrow B_2,...,A_1,A_2,...,A_n \rightarrow B_m $$
물론 반대도 가능하다. 하지만 주의할 점은 왼쪽 항에 대해서는 적용할 수 없다.

3. Trivial Functional Dependencies

어떤 FD가 어떤 constraints 들이 있는지에 관계없이 모든 relation들에 대해 만족한다면 우리는 그 FD가 trivial 하다고 한다. 다른 말로 $\{B_1,B_2,...,B_m\} \subseteq \{A_1,A_2,...,A_n\}$ 일 때,
$$\text{FD  } A_1,A_2,...,A_n \rightarrow  B_1,B_2,...,B_m $$
는 trivial 하다.

## Key and Superkeys
Relation R 에 대해 attributes의 집합 $\{A_1,A_2,...,A_n\}$ 이 key가 될 조건은 다음과 같다.
1. $\{A_1,A_2,...,A_n\}$ 이 R의 모든 다른 attributes을 functionally determine 한다.
2. $\{A_1,A_2,...,A_n\}$의 어떠한 subset도 R의 모든 다른 attributes을 functionally determine 하지 못한다.

즉, 다시 말해서 Relation R의 모든 attributes 을 최소한(minimal)의 attributes 집단으로 functionally determine 할 수 있다면 그 집단을 R의 key라고 부른다.
그리고 *Superkey* 는 key을 포함하고 있는 attributes의 집단을 의미한다.

## Closure of attributes
다음은 Closure 에 대해 알아보자. A set of FD's S 가 있고 attributes 집합 $\{A_1,A_2,...,A_n \}$ 이 있을 때, S에 대한 $\{A_1,A_2,...,A_n\}$ 의 closure은 S 하에서 $A_1,A_2,...,A_n \rightarrow  B$ 을 만족하는 모든 $B$의 집합이다. 그리고 $\{A_1,A_2,...,A_n\}+$ 로 표기한다.

!["Closure of attributes"](/assets/images/post/post_2_2.png){: width="300px"}

즉, 어떤 attributes 집단 $\{A_1,A_2,...,A_n \}$의 closure 는 $\{A_1,A_2,...,A_n \}$ 가 functionally determine 할 수 있는 모든 attributes을 의미한다. 따라서 만약 어떤 attributes 집단의 closure가 relation R의 전체 attributes이면 그 집단은 Superkey 이다.  

## Closing sets of FDs
앞에서 우리는 하나의 FD가 여러개의 FD로 나눠질 수도 있고 여러개의 FD들이 하나의 FD를 표현하는 경우도 있다는 것을 알았다. 그렇다면 만약 어떤 relation의 모든 FD의 집합을 대표하는 FD의 집합을 알고 싶다면 어떻게 할까? 주어진 FD의 집합 S에 대해서 S와 어떤 FD들의 집합이 equivalent 할 때, 우리는 그 집합을 S의 *basis* 라고 한다. 그리고 그 중 최소한의 basis을 *minimal basis* 라고 한다. minimal basis M 의 조건은 다음과 같다.
1. M의 모든 FD들의 우변항은 singleton이어야 한다.
2. 만약 M의 FD 중 하나라도 지워진다면 더 이상 M은 basis가 아니다.
3. M의 어떤 하나의 FD 에서 좌변항의 attributes 가 하나라도 없어진다면 더 이상 M 은 basis가 아니다.

다음은 minimal basis을 구하는 예시이다.

!["minimal basis example"](/assets/images/post/post_2_3.png){: width="500px"}   


이번 글에서는 적절한 relational database schema design을 하기 위해 필요한 여러 개념들을 정리해 보았다. 다음 글 에서는 적절하지 못한 design이 야기할 수 있는 여러 anomolies 와 decompsition을 위한 Boyce-Codd normal form, 3NF, 4NF 등의 개념에 대해 정리해 볼 것이다.     
