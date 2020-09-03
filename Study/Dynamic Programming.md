#### 개념  
계산 결과를 저장해두었다가 이를 재활용해 복잡한 문제를 해결하는 방법이다.  
모든 경우의 수를 전부 계산하는 전역 탐색을 기본으로 하지만, 이미 저장해둔 결과를 재활용하기 때문에 반복되는 계산을 줄인다.  
  
#### 원리  
1. 상위 문제를 하위 문제로 나눌 수 있다.  
2. 하위 문제에서 구한 값은 상위 문제에서도 동일한 값으로 적용된다.(Memoization)  
하위 문제에서 값을 구해 배열에 저장해둔 뒤, 상위 문제에서 동일한 하위 문제가 나오면 저장해둔 그 값을 사용한다.  
일반적인 부분정복 문제는 하위 문제의 값을 재사용하기 힘들다. 하위 문제가 서로 독립적일 때 적용하는 기법이기 때문이다.  
DP는 계산횟수를 줄일 수 있기 때문에 하위 문제 수가 기하급수적으로 증가할 때 유용하다.  

일례로 피보나치를 구현할 때, 재귀함수를 사용하면 시간복잡도는 O(2^n)이지만, DP를 사용하면 O(N)이다.  
func fib(_ n: Int) -> Int {// 일반 재귀 피보나치 함수  
    guard n > 1 else { return n }  
    if n == 2 { return 1 }  
    return fib(n - 1) + fib(n - 2)  
}  
  
func dpfib(_ n: Int) -> Int {// Memoization 피보나치 함수  
    guard n > 1 else { return n }  
    var fibs: [Int] = [0, 1]  
    (2...n).forEach { i in  
        fibs.append(fibs[i - 1] + fibs[i - 2]) // Memoization  
    }  
    return fibs.last!  
}  
print("\(dpfib(5))")  
  
#### 목적  
DP는 optimal value와 optimal solution을 찾는 것이 목적이다.  
그래서 DP 알고리즘은 최단 경로 문제 등 문제의 '최적화'에 사용된다.  