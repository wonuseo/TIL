---
tags: 
  - O-Notation
---
#TIL 

# 개요
**알고리즘의 효율성과 성능을 평가할 때 사용하는 수학적 도구.**  

> ...인자가 특정한 값이나 무한대로 향할 때 함수의 극한적인 동작을 설명하는 수학적인 표기법 입니다. 
> ...간단히 말하자면 빅오 표기법이란 코드의 복잡도를 대수학 개념을 이용해 표현하는것입니다.

세부적인 계산 과정이나 상수를 무시하고, 알고리즘 성능의 근사 적 추이 만을 강조하여 일반적인 형태로 표현되어 비교가 간단해진다.
***
# 표기법과 읽는 법 (ex : 선택 정렬)
> 선택 정렬 알고리즘은 $O(n^2)$ 의 복잡도를 갖고 있는 전형적인 알고리즘 입니다.   

**선택 정렬은 배열 내에서 가장 작은 요소를 찾아, 배열의 맨 앞에 위치한 요소와 교체하는 과정을 반복하여 정체 리스트를 정렬하는 방식.**

선택 정렬에서 각 원소의 정렬을 위해 최소값을 찾는 과정은 배열의 크기가 점차 줄어드는 등차 수열을 형성한다.   
배열의 길이가 $n$ 일 때, 첫 번째 원소를 정렬하기 위해서는 $n-1$ 번의 비교가 필요하고, 두 번째 원소를 정렬하기 위해서는 $n-2$ 번, ... 마지막 원소 이전까지 1번 비교가 필요하다. 즉, 공차가 1인 등차수열의 역순이다. 전체 비교 횟수는 등차수열의 합으로 표현할 수 있다.  
$$총 \ 비교 \ 횟수={n(n-1) \over 2} = {n^2-n \over 2} = {n^2 \over 2} - {n \over 2}$$ 
> 빅오 표기법을 계산할 때에는 최고차항만 신경쓰고 나머지 계수들은 신경쓰지 않습니다. 그러므로 여기에서 우리는 점근 표기법의 값으로 $n^2$ 을 얻게 됩니다.  
> 이것은 $O(n^2)$로 표시하고 "빅오 n의 제곱"이라고 읽습니다.

**빅오 표기법에서는 최고차항만 고려하며 계수나 낮은 차수의 항은 무시된다. 따라서 $n^2$ 항이 선택 정렬의 성능을 결정하는 주요 요소로 간주된다.**

**$O(n^2)$ 는 데이터의 양이 늘어날수록 시간이 제곱으로 증가한다는 것을 의미한다.**
***
# 정의
**함수의 성장률을 다른 함수와 비교하여 나타내는 방법.**
$$n \geq n_0\ 에\ 대해 \ \ \vert\ f(n)\ \vert \leq C * \vert\ g(n)\ \vert$$
* $n \geq n_0$ 
	* $n$ 의 하한을 나타낸다.
	* $n_0$ 이상 모든 $n$ 에 대해 부등식이 성립한다.
	***
* $\vert f(n) \vert \leq C * \vert g(n) \vert$
	* $f(n)$은 $𝑔(𝑛)$ 에 비례하여 증가하며, $C$ 는 그 비율을 조정하는 상수이다.
	***
### 성립 과정
>...만약 $g(n)$ 함수를 $n^2$ 이라고 한다면, 계수 $c=1$ 와 $n_0=0$ 을 알 수 있습니다. 여기에서 $n>n_0$ 라는 조건이 만족하는 한, $n^2$ 는 $n^2/2-n/2$ 보다 항상 큰값이 됩니다.  
>이는 각 함수들에서 $n^2/2$ 를 빼봄으로써 쉽게 증명할 수 있습니다. 그렇다면 $n^2/2 > -n/2$ 는 $n>0$ 라는 조건에서 참이라는 걸 알 수 있습니다. 그러므로 $f(n)=O(n^2)$, 즉 선택 정렬에서는 "제곱의 시간이 걸린다(big O squared)"고 하는 결론을 낼 수 있는 것입니다.
1. 조건
	* $f(n)={n^2 \over 2}-{n \over 2}$
	* $g(n)=n^2$ 
	* $C=1$
	* $n_0=0$ 
2. 대입
	$$\vert\  {n^2 \over 2}-{n \over 2}\  \vert \leq 1 * \vert\  n^2\ \vert$$
3. 부등식 설명
    $${g(n)-f(n)}\ =\ n^2-({n^2 \over 2}-{n \over 2})\ =\ {n^2 \over 2}+{n \over 2}$$
***
# 전형적인 Big-O 복잡도 비교
- $n! > 2^n > n^2 > n\ log\ n > n > log\ n > 1$
![[Big-O Complexity Chart.png]]
## $O(1)$ - 상수
**입력 크기와 상관 없이 항상 일정한 시간이 소요된다. 즉, 작업 시간이 입력 크기에 독립적이다.**
![[O(1) Graph]]
``` java
public class ConstantTime {
    public static void main(String[] args) {
        int n = 1000;
        System.out.println("Hello, World!");
    }
}
```
## $O(log\ n)$ - 로그
**입력 크기가 증가할 때, 실행 시간이 로그에 비례하여 증가한다.**
![[O(log n) Graph]]
``` java
public class LogarithmicTime {
    public static void main(String[] args) {
        int n = 1000;
        int count = 0;
        for (int i = n; i > 1; i /= 2) {
            count++;
        }
        System.out.println("Count: " + count);
    }
}
```
## $O(n)$ - 선형
**입력 크기에 비례하여 실행 시간이 증가한다.**
![[O(n) Graph]]
``` java
public class LinearTime {
    public static void main(String[] args) {
        int n = 1000;
        for (int i = 0; i < n; i++) {
            System.out.println("i: " + i);
        }
    }
}
```
## $O(n\ log\ n)$ - 선형 로그
**입력 크기가 증가할 때, 실행 시간이  $n \log n$ 에 비례하여 증가**
![[O(n log n) Graph]]
``` java
public class MergeSortExample {
    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 4, 2, 7, 1, 10};
        mergeSort(arr, 0, arr.length - 1);
        for (int num : arr) {
            System.out.println(num);
        }
    }

    public static void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }
    }

    public static void merge(int[] arr, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        int[] leftArray = new int[n1];
        int[] rightArray = new int[n2];

        for (int i = 0; i < n1; i++) {
            leftArray[i] = arr[left + i];
        }
        for (int j = 0; j < n2; j++) {
            rightArray[j] = arr[mid + 1 + j];
        }

        int i = 0, j = 0;
        int k = left;
        while (i < n1 && j < n2) {
            if (leftArray[i] <= rightArray[j]) {
                arr[k] = leftArray[i];
                i++;
            } else {
                arr[k] = rightArray[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            arr[k] = leftArray[i];
            i++;
            k++;
        }

        while (j < n2) {
            arr[k] = rightArray[j];
            j++;
            k++;
        }
    }
}
```
***
## $O(n^2)$ 이차
**입력 크기가 증가할 때, 실행 시간이  $n^2$ 에 비례하여 증가**
![[O(n2) Graph]]
``` java
public class QuadraticTime {
    public static void main(String[] args) {
        int n = 100;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                System.out.println("i: " + i + ", j: " + j);
            }
        }
    }
}
```
***
## $O(2^n)$ - 지수
**입력 크기가 증가할 때, 실행 시간이  $2^n$ 에 비례하여 급격히 증가**
![[O(2n) Graph]]
``` java
public class ExponentialTime {
    public static void main(String[] args) {
        int n = 20;
        System.out.println("Fibonacci of " + n + " is " + fibonacci(n));
    }

    public static int fibonacci(int n) {
        if (n <= 1) {
            return n;
        }
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```
***
## $O(n!)$ - 팩토리얼
**입력 크기가 증가할 때, 실행 시간이  $n!$ 에 비례하여 매우 급격히 증가**
![[O(factorial) Graph]]
``` java
public class FactorialTime {
    public static void main(String[] args) {
        int n = 10;
        System.out.println("Permutations of " + n + " elements:");
        permute(new int[n], 0);
    }

    public static void permute(int[] arr, int k) {
        if (k == arr.length) {
            for (int i : arr) {
                System.out.print(i + " ");
            }
            System.out.println();
        } else {
            for (int i = 0; i < arr.length; i++) {
                boolean found = false;
                for (int j = 0; j < k; j++) {
                    if (arr[j] == i) {
                        found = true;
                        break;
                    }
                }
                if (!found) {
                    arr[k] = i;
                    permute(arr, k + 1);
                }
            }
        }
    }
}
```
***
# Ref:  
[빅오 표기법을 설명하다. 시간과 공간의 복잡도](https://www.freecodecamp.org/korean/news/big-o-notation-why-it-matters-and-why-it-doesnt-1674cfa8a23c/)   
[bigocheatsheet](https://www.bigocheatsheet.com/)