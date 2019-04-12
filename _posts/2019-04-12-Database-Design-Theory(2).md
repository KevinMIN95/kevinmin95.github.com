---
layout: post
title: "[Database] Design Theory(2)"
date: 2019-04-12
use_math: true
---
이전 포스트... [[Database] Design Theory(1)](/blog/2019/04/09/Database-Design-Theory)

## 들어가며
Relational database schema을 design 하는 방법에는 여러가지가 있다. 하지만 적절하지 못한 design은 Update anomalies, Deletion anomalies 등 여러 문제를 발생시킨다. 특히, 주로 너무 많은 정보를 하나의 relation에 담는 경우 발생한다. 지난 포스트에서는 functional dependencies, superkey, key, multivalued dependencies 등 여러 개념들에 대해 정리해 보았다. 이번 글에서는 한 relation을 여러 개의 relations 들로 나누는 법(Normalization)에 대해 정리할 것이다.
