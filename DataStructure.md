---
tags:  
  - DataStructure
  - TimeComplexity
  - SpaceComplexity
---
#TIL

# 개요
**데이터를 효율적으로 관리하고 접근할 수 있도록 조직화, 관리, 저장하는 방법을 말한다.**

이는 크게 데이터가 일렬로 나열되는 형태로, 각 요소가 이전 및 다른 요소와 직접 연결된 순차적 데이터 접근 방식인 **선형 자료구조** 와 데이터가 계층 및 그래프 형태로 조직되어, 각 요소가 여러 요소와 연결될 수 있는 비 순차적 데이터 접근 방식인 **비선형 자료구조** 로 나뉜다.  

데이터 구조에 사용된 알고리즘의 성능을 측정하고 평가하기 위해 복잡도를 고려해야 한다. 알고리즘이 실행을 완료하는데 걸리는 시간을 나타내는 **시간 복잡도** 와 알고리즘이 실행되는 동안 사용하는 메모리의 양을 나타내는**공간 복잡도** 를 사용한다. 두가지 복잡도를 사용해 다양한 입력 크기에서 얼마나 효율적으로 동작하는지 평가해 문제 해결 전략을 수립한다.

복잡도를 표기하는 방법으로 여러가지가 있으며, 각 표기법은 특정 관점을 강조한다.  
- 평균: 세타 표기법(Big Theta Notation, Θ)
- 최악: [빅오 표기법(Big-O Notation, O)](O-Notation.md)
	- 엄격한 상한: 소문자 오 표기법(Little-o Notation, o)
- 최선: 오메가 표기법(Big Omega Notation, Ω)
	- 엄격한 상한: 소문자 오메가 표기법(Little Omega Notation, ω)  

가장 많이 사용되는 것은 [빅오 표기법(Big-O Notation, O)](O-Notation.md) 으로 최악의 경우를 가정하기 때문에 실제 문제 상황에서의 성능을 고려할 수 있기 때문이다.
***
# Linear DataStructure
## Array
## Linked List
## Stack
## Queue
***
# NonLinear DataStructure
# Tree
# Graph
***
# Ref:
[big-O cheatsheet](https://www.bigocheatsheet.com/)   
[HAMMOND [알고리즘] Time Complexity (시간복잡도)](https://hanamon.kr/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-time-complexity-%EC%8B%9C%EA%B0%84-%EB%B3%B5%EC%9E%A1%EB%8F%84/)