---
tags:  
  - DataStructur
  - TimeComplexity
  - SpaceComplexity
---
#TIL 

# 개요
**데이터를 효율적으로 관리하고 접근할 수 있도록 조직화, 관리, 저장하는 방법을 말한다.**   

이는 크게 데이터 요소들이 순차적으로 나열된 구조인 '선형 자료구조'와 데이터 요소들이 계층적 및 그래프 형태로 연결된 구조인 '비선형 자료구조'로 나뉜다. 효율성, 성능 등을 예측하여 적합한 자료구조를 선택하기 위해 복잡도 를 지표로 사용한다.

복잡도 는 자료구조 및 알고리즘의 효율성을 수치화하는 척도로, 크게 두가지로 나뉜다.  
실행 시간(반복 횟수)이 입력 크기에 따라 어떻게 변화하는지 평가를 위해 시간 복잡도를 계산하고, 입력 크기에 따라 필요한 메모리 공간의 양을 측정하기 위해 공간 복잡도를 계산한다. 이러한 복잡도를 표현하는 표준적인 방법으로 [빅오-표기법](O-Notation.md)을 사용한다.
***
# 시간 복잡도
**알고리즘이 문제를 해결하는데 필요한 시간(연산 횟수)을 측정하는 척도로, 알고리즘 수행 시 발생하는 반복문, 조건문, 재귀 호출 등 기본 연산의 수행 횟수 기반으로 측정된다.**
# 공간 복잡도
**알고리즘이 실행 되면서 소비하는 총 메모리 공간의 양을 나타내는 척도로, 임시 데이터 저장, 변수 할당 스택 공간 등 모든 메모리 요구사항을 포함한다.**

![[O-Notation# 전형적인 Big-O 복잡도 비교]]
### $O(1)$
![[O(1) Graph]]

> $O(1)$ 는 일정한 복잡도 (constant complexity) 라고 하며, 입력값이 증가하더라고 시간이 늘어나지 않는다.
> 다시 말해 입력값의 크기와 관계없이, 즉시 출력값을 얻어낼 수 있다는 의미이다.
##### 예제 : $O(1)$
```java
public class ConstantTimeExample {
	public static void main(String[] args) {
		int[] array = {10, 20, 30, 40, 50};

		System.out.println(array[2]); // 30
		System.out.println(array[0]); // 10
		System.out.println(array[1]); // 20
	}
}
```
배열에서 요소를 인덱싱하는 연산은 $O(1)$ 복잡도를 가진다. 어떤 요소에 접근하던 그 작업에 걸리는 시간은 항상 일정하다.
### $O(log\ n)$
![[O(log n) Graph]]


***
# Linear DataStructure
# NonLinear DataStructure
***
# Ref:  
[bigocheatsheet](https://www.bigocheatsheet.com/)   
[HANAMON [알고리즘] Time Complexity (시간복잡도)](https://hanamon.kr/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-time-complexity-%EC%8B%9C%EA%B0%84-%EB%B3%B5%EC%9E%A1%EB%8F%84/)