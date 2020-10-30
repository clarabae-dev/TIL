## Complexity  
알고리즘의 계산 복잡도는 다음 두가지 방법으로 표현한다.  
1. 시간 복잡도: 얼마나 빠르게 실행되는가.  
2. 공간 복잡도: 얼마나 많은 저장 공간이 필요한가.  
  
두가지를 모두 만족시키기는 어려우나, 대용량 시스템의 보편화로 시간 복잡도를 더 우선적으로 고려한다.  
  
  
### Time Complexity  
시간 복잡도란, 알고리즘이 문제를 해결하는데 걸리는 시간을 뜻한다.  
최악의 경우를 계산하는 방식을 빅오 표기법이라 부르는데, 이 방식을 가장 많이 사용하여 복잡도를 표현한다.  
1. O(1)  
input 크기에 상관없이 항상 일정한 시간이 걸리는 알고리즘이다. input 증가량은 성능에 거의 영향을 미치지 않는다.  
2. O(log n)  
input 크기가 커질수록 처리 시간이 log 만큼 짧아지는 알고리즘이다. (input x10 -> time x2)  
대표적으로 이진탐색이 있다.  
3. O(n)  
input 크기에 비례해 처리 시간이 증가하는 알고리즘이다. (input x10 -> time x10)  
대표적으로 1차원 for문이 있다.  
4. O(n log n)  
input 크기가 커질수록 처리 시간이 log 만큼 증가하는 알고리즘이다. (input x10 -> time x20)  
대표적으로 병합 정렬, 퀵 정렬이 있다.  
5. O(n^2)  
input 크기가 커질수록 처리 시간이 급수적으로 증가하는 알고리즘이다. (input x10 -> time x100)  
대표적으로 이중 루프가 있다.  
6. O(2^n)  
input 크기가 커질수록 처리 시간이 기하급수적으로 증가하는 알고리즘이다. 대표적으로 피보나치 수열이 있다.  
  
#### Calculation  
프로그램이 1라인 실행되는 것을 시간복잡도로 O(1)이라 표현한다.  
  
```swift
for i in 0..<n { // 반복문이 n만큼 반복되므로 시간복잡도는 O(n)
	a = i
}

for i in 0..n { // n만큼 반복되는 이중 for문이므로 시간복잡도는 O(n^2)
	for j in 0..n {

	}
}
```  
  
보통 반복문의 경우 가장 시간을 많이 소모하여 시간복잡도를 증가시키므로 반복문의 수를 줄이는 것이 중요하다.  
또한 자료구조와 알고리즘의 적절한 사용 역시 시간복잡도에 큰 영향을 준다.  
  
### Space Complexity  
공간 복잡도란, 프로그램을 실행하고 완료하는데 필요한 저장 공간의 양을 뜻한다.  
1. 고정 공간: 코드를 저장하는 공간으로 알고리즘과 관계없는 공간이다.  
2. 가변 공간: 실행 중 동적으로 필요한 공간으로 알고리즘과 관련이 있는 공간이다.  
  
총 필요한 저장 공간은 고정 공간 + 가변 공간으로 고정 공간은 상수이기 때문에 공간 복잡도는 가변 공간에 좌우된다.  
  
#### Calculation  
공간 복잡도를 구할 때는 알고리즘 실행 시 사용되는 저장 공간을 계산하면 된다.  
  
```swift
for i in 0..<n { // 반복문이 n만큼 반복되므로 공간복잡도는 O(n)
	a = i
}

for i in 0..n { // n만큼 반복되는 이중 for문이므로 공간복잡도는 O(n^2)
	for j in 0..n {

	}
}
```  
  
보통 재귀함수의 경우 매 함수 호출마다 함수와 관련된 데이터들을 저장할 공간이 필요하다.  
공간 복잡도만 고려한다면 재귀함수보다는 반복문을 사용해 구현하는 것이 더 효율적이다.  
  
  
  
출처:  
https://coding-factory.tistory.com/609  
https://coding-factory.tistory.com/608?category=794828  