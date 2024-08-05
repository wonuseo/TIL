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
**동일한 타입의 데이터가 연속적인 메모리 공간에 저장된 자료구조.**  

각 요소는 인덱스를 통해 접근할 수 있으며, 인덱스는 0부터 시작한다. 선언 시 크기가 고정되어 크기를 변경할 수 없다.
- 장점
	- 임의의 위치에 있는 요소에 접근 시 $O(1)$ 시간 복잡도로 접근 가능.
	- 연속된 메모리 공간을 사용하기 때문에 메모리 효율성이 높다.
- 단점
	- 배열의 크기는 선언 시 고정되어, 변경될 수 없다.
	- 중간 요소에 삽입 또는 삭제 시, 나머지 요소를 이동 시켜야 해서 $O(n)$ 시간 이 소요된다.

| Operation | Worst Case ($O$) | Best Case ($Ω$)  |
| --------- | ---------------- | ---------------- |
| Access    | $O(1)$           | $Ω(1)$           |
| Search    | $O(n)$           | $Ω(1)$ : 첫번 째 요소 |
| Insert    | $O(n)$ : 중간 삽입   | $Ω(1)$ : 끝 삽입    |
| Delete    | $O(n)$ : 중간 삭제   | $Ω(1)$ : 끝 삭제    |
``` java
public class ArrayOperations {
    public static void main(String[] args) {
        
        int[] numbers = {1, 2, 3, 4, 5};

        // Access
        System.out.println("Access element at index 2: " + numbers[2]);

        // Search
        int target = 3;
        boolean found = false;
        for (int i = 0; i < numbers.length; i++) {
            if (numbers[i] == target) {
                found = true;
                System.out.println("Found target " + target + " at index " + i);
                break;
            }
        }
        if (!found) {
            System.out.println("Target " + target + " not found");
        }

        // Insert
        int[] newNumbers = new int[numbers.length + 1];
        int insertIndex = 2;
        int newValue = 99;
        for (int i = 0, j = 0; i < newNumbers.length; i++) {
            if (i == insertIndex) {
                newNumbers[i] = newValue;
            } else {
                newNumbers[i] = numbers[j++];
            }
        }
        System.out.print("Array after insertion: ");
        for (int number : newNumbers) {
            System.out.print(number + " ");
        }
        System.out.println();

        // Delete
        int deleteIndex = 2;
        int[] numbersAfterDeletion = new int[numbers.length - 1];
        for (int i = 0, j = 0; i < numbers.length; i++) {
            if (i != deleteIndex) {
                numbersAfterDeletion[j++] = numbers[i];
            }
        }
        System.out.print("Array after deletion: ");
        for (int number : numbersAfterDeletion) {
            System.out.print(number + " ");
        }
    }
}
```




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