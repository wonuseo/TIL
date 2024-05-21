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
***
![[O-Notation# 전형적인 Big-O 복잡도 비교]]
## $O(1)$
![[O(1) Graph]]
> $O(1)$ 는 일정한 복잡도 (constant complexity) 라고 하며, 입력값이 증가하더라고 시간이 늘어나지 않는다.
> 다시 말해 입력값의 크기와 관계없이, 즉시 출력값을 얻어낼 수 있다는 의미이다.
#### 예제: 배열 출력
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
## $O(log\ n)$
![[O(log n) Graph]]
> $O(log n)$ 는 로그 복잡도 (logarithmic complexity) 라고 부르며, Big-O 표기법 중 O(1) 다음으로 빠른 시간 복잡도를 가진다.  
> ...이해하기 쉬운 게임으로 비유해 보자면 up & down 을 예로 들 수 있다.  
> ...매번 숫자를 제시할 때 마다 경우의 수가 절반 씩 줄어들기 때문에 (1~100 사이의 숫자의 경우) 최악의 경우에도 7번이면 원하는 숫자를 찾아 낼 수 있게된다.  
> BTS 의 값 탐색 또한 이와 같은 로직으로, $O(log n)$ 의 시간 복잡도를 가진 알고리즘(탐색기법)이다.
#### 예제: 이진 탐색(Binary Search Tree)
```java
public class BinarySearch {

	public static int binarySearch(int[] arr, int target) {
		int low = 0; 
		int high = arr.length - 1;
	
		while (low <= high) {
			int mid = low + (high - low) / 2;
	
			if (arr[mid] == target) {	
				return mid; 
			} else if (arr[mid] < target) {
				low = mid + 1; 
			} else {
				high = mid - 1; 
			}
		}

		return -1;
	}
	
	public static void main(String[] args) {
		int[] data = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};	
		int target = 7;
	
		int result = binarySearch(data, target);
	
		if (result == -1) {
			System.out.println(target + " is not in the array");
		} else {
			System.out.println(target + " found at index " + result);
		}
	}
}
```
* `low + high / 2`  대신  `low + (high - low) / 2` 를 사용한 이유.
	1.  오버플로 방지
		* `int low, high` 가 최대 값에 인접한 상태에서  `low + high`  를 수행한다면, 오버플로 발생.
	2. 정확한 계산
		* 현재 탐색 범위에서 중간 위치를 찾아, `low` 를 기준으로 하는 상태 값으로 계산.

이진 탐색의 기본 원리는 분할 정복 (Divide and Conquer) 전략에 기반을 두고 있어, 절반씩 범위를 줄여가면서 타겟을 찾는다.
## $O(n)$
![[O(n) Graph]]
>$O(n)$ 은 선형 복잡도 (linear complexity) 라고 부르며, 입력값이 증가함에 따라 시간 또한 같은 비율로 증가하는 것을 의미한다.
#### 예제: 배열 출력2
```java
public class LinearComplexity {

	public static void printArrayElements(int[] array) {
        for (int i : array) {
            System.out.println(i);
        }
	}
	
	public static void printArrayElementsTwice(int[] array) {
		for (int i = 0; i < 2 * array.length; i++) {
			System.out.println(array[i % array.length]);
		}
	}
	
	public static void main(String[] args) {
		int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
		
		printArrayElements(numbers);
		printArrayElementsTwice(numbers);
	}
}
```
`printArrayElementsTwice` 는 배열 출력 반복문에 상수가 선언되어 있어 $O(2n)$ 일 것 같지만, 빅 오 표기법에서는 상수 계수를 생략한다. 이는 알고리즘의 성능을 입력 크기가 매우 큰경우에 초점을 맞추기 때문이다. 
입력이 아주 큰 값일 때, $2n$ 과 $n$ 의 차이는 상대적으로 중요하지 않게된다.
## $O(n\ log\ n)$
![[O(n log n) Graph]]
>$O(n\ log\ n)$ 은 로그 선형 복잡도 (log-linear complexity) 라고 부르며, 입력값이 중가함에 따라 시간 복잡도가 입력값과, 로그 값인 $log\ n$ 의 곱에 비례하여 증가하는 것을 의미한다.  
>$O(n)$ 보다 느리게 증가하지만, 입력 값이 커질수록 둘 사이의 차이가 점점 커진다.
#### 예제: 병합 정렬
```java
public class MergeSort {  

    private static void merge(
	    int[] array
	    , int[] temp
	    , int leftStart
	    , int rightEnd
    ) {  
        int leftEnd = (leftStart + rightEnd) / 2;  
        int rightStart = leftEnd + 1;  
        int size = rightEnd - leftStart + 1;  
  
        int left = leftStart;  
        int right = rightStart;  
        int index = leftStart;  
  
        while (left <= leftEnd && right <= rightEnd) {  
            if (array[left] <= array[right]) {  
                temp[index] = array[left];  
                left++;  
            } else {  
                temp[index] = array[right];  
                right++;  
            }  
            index++;  
        }  
 
        System.arraycopy(array, left, temp, index, leftEnd - left + 1);  
        System.arraycopy(array, right, temp, index, rightEnd - right + 1);  
        System.arraycopy(temp, leftStart, array, leftStart, size);  
    }  
    
    private static void mergeSort(
	    int[] array
	    , int[] temp
	    , int leftStart
	    , int rightEnd
    ) {  
        if (leftStart >= rightEnd) {  
            return;  
        }  
  
        int middle = (leftStart + rightEnd) / 2;  
        mergeSort(array, temp, leftStart, middle);  
        mergeSort(array, temp, middle + 1, rightEnd);  
        merge(array, temp, leftStart, rightEnd);  
    }  
  
    public static void sort(int[] array) {  
        int[] temp = new int[array.length];  
        mergeSort(array, temp, 0, array.length - 1);  
    }  
  
    public static void main(String[] args) {  
        int[] array = {38, 27, 43, 3, 9, 82, 10};  
        System.out.println("Unsorted array:");  
        for (int num : array) {  
            System.out.print(num + " ");  
        }  
  
        sort(array);  
  
        System.out.println("\nSorted array:");  
        for (int num : array) {  
            System.out.print(num + " ");  
        }  
    }  
}
```
***
# Linear DataStructure
# NonLinear DataStructure
***
# Ref:  
[bigocheatsheet](https://www.bigocheatsheet.com/)   
[HANAMON [알고리즘] Time Complexity (시간복잡도)](https://hanamon.kr/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-time-complexity-%EC%8B%9C%EA%B0%84-%EB%B3%B5%EC%9E%A1%EB%8F%84/)