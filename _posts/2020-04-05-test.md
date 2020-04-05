---
title: 삽입 정렬(Insertion Sort)
categories: 
  - Data Structure & Algorithms
last_modified_at: 2020-04-05T13:00:00+09:00
use_math: true
---


정렬 알고리즘 중에서 기본적이고 간단한 삽입 정렬에 대해서 살펴보도록 하겠습니다. 삽입 정렬(Insertion Sort)는 배열의 앞에서부터 차례로 정렬된 부분부터 비교하며 위치를 찾아 삽입하는 알고리즘입니다. 아래 예를 보여 설명해 보겠습니다.


![ex_screenshot](https://i.imgur.com/JlOeSmH.png)


(a)에서 먼저 key 값을 2번째 값인 2로 지정하고 왼쪽 값들과 비교합니다. 이때 1번째 값이 5로 2보다 크기 때문에 자리를 바꿔줍니다. (b)도 마찬가지로 왼쪽 값들과 비교한 결과 5보다 작기에 서로 자리를 바꿔주게 됩니다. (c)의 경우 key 값이 6으로 왼쪽에 있는 값들보다 크기 때문에 자리를 바꾸지 않습다.


| key         | value         | 정렬 전       | 정렬 후        |
|----------------|----------------|----------------|----------------|
|       2         |      2          |   5, 2, 4, 6, 1, 3       |   2, 5, 4, 6, 1, 3   |
|       3         |      4          |   2, 5, 4, 6, 1, 3       |   2, 4, 5, 6, 1, 3   |
|       4         |      6          |   2, 4, 5, 6, 1, 3       |   2, 4, 5, 6, 1, 3   |


![ex_screenshot](https://i.imgur.com/Yrwd1fw.png)


(d)에서는 4번째 key 값인 1부터 왼쪽에 있는 모든 값들을 비교하며 자리를 바꿔주는데 1은 가장 작은 값이기 때문에 1번째로 정렬되게 됩니다. (e)는 배열의 마지막인 3을 key 값으로하여 왼쪽 값들과 비교한 후 3번째로 가면서 정렬이 (f)와 같이 완료됩니다.



| key         | value         | 정렬 전       | 정렬 후        |
|----------------|----------------|----------------|----------------|
|       5         |      1          |   2, 4, 5, 6, 1, 3       |   1, 2, 4, 5, 6, 3   |
|       6         |      3          |   1, 2, 4, 5, 6, 3       |   1, 2, 3, 4, 5, 6   |



위와 같은 삽입정렬 진행 과정을 <a href="https://visualgo.net/en/sorting?slide=1">https://visualgo.net/en/sorting?slide=1</a>에서 시험해 볼 수 있습니다. 아직 이해가 안되시면 여기서 한 번 실행해보고 의사코드를 보시면 이해가 빨리 될 것입니다.

이와 같이 삽입 정렬은 전체 데이터를 모두 비교하면서 진행되게 됩니다. 그렇다면 의사코드오 실제로 구현한 코드를 살펴보겠습니다.



## 의사코드(pseudocode)


의사코드는 프로그램을 작성하기 전 작동하는 논리를 표현하기 위한 언어입니다. 특정 프로그래밍 언어의 문법에 따라 쓴 것이 아니라 일반적인 언어로 코드를 흉내 내어놓은 코드를 말합니다.


```python
INSERTION SORT(A)
for i = 2 to R.length
	key = A[i]
    // 비교할 대상인 key 값을 지정합니다.
    while(i > 0 and A[i] > key)
		change A[i] with A[i-1]
        i = i - 1
    A[i + 1] = key
```



## 자바 코드


삽입 정렬을 자바 코드로 구현한 결과는 아래와 같습니다.

```java
public class Insertion {
	
	public static void insertionSort(int[] arr) {
		
		int[] a = arr;
		
		for(int index=1; index < a.length; index++) {
			int key = a[index];
			int temp = index - 1;
			while(temp >= 0 && a[temp] > key) {
				a[temp + 1] = a[temp];
				temp = temp - 1;
			}
			a[temp + 1] = key;
		}
		for(int i=0; i<a.length;i++) {
			System.out.print(a[i] + " ");
		}
		
	}
	
	public static void main(String[] args) {
		
		int []array = {1, 23, 6, 3, 5, 2, 7, 5, 43, 12};
		
		for(int i=0; i<array.length;i++) {
			System.out.print(array[i] + " ");
		}
		System.out.println("");
		insertionSort(array);
	}

}
```



## 시간복잡도


삽입정렬의 의사코드를 바탕으로 시간복잡도를 계산한 것은 아래와 같습니다. 의사코드에서 5~7행에서는 최악의 경우 모든 데이터를 다 비교하며 변경할 수 있습니다. 물론 미리 정렬이 되어 있을 경우에는 5~7행은 필요가 없겠지만요. $t_j$는 $j$번째 key를 정렬할 때 비교 연산 횟수로, 많이 정렬할 수록 그 횟수는 늘어납니다.


![ex_screenshot](https://i.imgur.com/iUaNqxd.png)


먼저 worst case인 경우에 대해서 보겠습니다.

$$T(n)={ c }_{ 1 }n+{ c }_{ 2 }(n-1)+{ c }_{ 4 }(n-1)+{ c }_{ 5 }(n-1)+{ c }_{ 8 }(n-1)$$

이는 2차식의 형태입니다. 따라서 worst case의 삽입정렬 계산복잡도는 $n^2$입니다. 이번에는 best case인 경우를 보도록 하겠습니다. 
정렬 대상 데이터 개수가 $n$이고, best case인 경우에는 $an+b$ 형태의 1차식 형태를 나타내고 시간복잡도는 $n$에 대해서 선형적으로 증가합니다.

$$
T(n)={ c }_{ 1 }n+{ c }_{ 2 }(n-1)+{ c }_{ 4 }(n-1)+{ c }_{ 5 }(\frac { n(n+1) }{ 2 } -1)\\+{ c }_{ 6 }(\frac { n(n-1) }{ 2 } )+{ c }_{ 7 }(\frac { n(n-1) }{ 2 } )+{ c }_{ 8 }(n-1)
$$

지금까지 삽입 정렬에 대해서 알아 보았습니다. 이 정렬 알고리즘은 적은 데이터에서는 사용할 수 있으나 많은 데이터를 정렬하고자 할때 그 효율성은 급격하게 떨어지게 됩니다. 그 이유는 위에서 말한 시간복잡도와 관련 있습니다. 시간복잡도 $n$과 $n^2$의 차이는 컴퓨팅 파워에 큰 차이를 보이기 때문입니다.



## Reference

위키피디아(<a href="https://ko.wikipedia.org/wiki/%EC%82%BD%EC%9E%85_%EC%A0%95%EB%A0%AC">https://ko.wikipedia.org/wiki/%EC%82%BD%EC%9E%85_%EC%A0%95%EB%A0%AC)</a>

Cormen et al. Introduction to Algorithms, 3rd edition, MIT Press, 2009.

