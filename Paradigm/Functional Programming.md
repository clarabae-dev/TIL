## Functional Programming  
1. 함수를 사용한다.  
기존에는 객체를 통해 메소드를 호출하였다.  
함수형 프로그래밍은 함수를 먼저 쓰고, 데이터(객체 포함 무엇이든)를 input으로 넣는다.  
2. Side Effet 없이 구현한다.  
객체지향 프로그래밍은 객체와 객체 간의 연관관계로 구성된다. 객체지향 프로그래밍에서 객체는 멤버변수와 메소드를 가지고 있다.  
그리고 메소드가 수행될 때는 멤버변수가 활용된다. 이 멤버변수의 상태에 따라 메소드의 결과가 달라진다.  
ex. 캐릭터가 공격할 때, 공격력이라는 멤버변수에 따라 결과는 달라질 수 있다. 
함수형 프로그래밍은 함수와 각 함수의 입력과 결과가 연결되어 구성된다.  
순수 함수는 항상 동일한 입력에 대해 동일한 결과를 낸다. 그 말인 즉슨, 함수는 상태를 가지지 않는다.  
함수의 결과는 입력에만 의존하기 때문에 함수의 실행 순서는 그 중요도가 낮아진다.  
*OOP와 FP의 차이는 State의 유무이다.*  
*순수함수: 어떤 값을 언제 어느 상황에 어떻게 넣더라도 동일한 결과가 나오는 함수*  
3. 선언적으로 프로그래밍 한다.  
Imperative Programming(명령형 프로그래밍): 어떤 과정을 거치는가.  
Declarative Programming(선언형 프로그래밍): 어떤 결과를 얻는가.  
  
### Why Functional Programming is Matter?  
1. Concurrency Programming  
멀티스레드를 활용한 동시성 프로그래밍을 구현할 때, 기존의 Imperative Programming 환경은 deadlock이 발생할 가능성이 컸다.  
명령형 프로그래밍 환경에서 deadlock이 발생하는 주요 원인은 스레드 간에 공유되는 데이터나 상태값이 mutable하기 때문이다.  
그러나 함수형 프로그래밍 환경에서는 사용하는 모든 데이터가 immutable하며, 함수는 부수적인 효과는 없다.  
*https://jcsoohwancho.github.io/2019-09-04-%EB%8F%99%EC%8B%9C%EC%84%B1-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D(1)-%EB%8F%99%EC%8B%9C%EC%84%B1-%EA%B8%B0%EB%B3%B8/  
swfit 동시성 프로그래밍 참고*  
2. Testable  
함수는 내부적으로 어떠한 상태값도 가지지 않으며, 입력값에 대한 출력값을 책임질 뿐이다.  
그렇기 때문에 함수 자체애 대한 테스트가 용이하며, 함수의 역할이 명확해진다.  
3. Used as a Value  
함수는 그 자체로 값처럼 쓰일 수 있어서 함수가 입력 또는 출력이 될 수 있다.  
함수를 매개변수로 받는 함수를 고차함수(Higher-order Function)라 한다. 대표적인 고차함수에는 map, filter, reduce가 있다.  
이 특징 덕분에 함수 간 결합, 조합이 쉬워지며, 좀 더 간결한 코드를 만들 수 있다.  
  
```swift
Observable.from(["a", "b", "c", "d"])
	.subscribe(onNext: { s in
			print(s)
		})

// onNext 클로져를 함수로 빼낼 수 있다.
func output(_ s: Any) -> Void {
	print(s)
}

Observable.from(["a", "b", "c", "d"])
	.subscribe(onNext: output) // 함수 그 자체로 값으로 쓰인다.
```