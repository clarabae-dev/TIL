1. 고차함수  
함수를 매개변수로 받는 함수.  
대표적인 고차함수에는 Map, Reduce, Filter 가 있다.  
고차함수를 사용할 수 있는 타입은 다음과 같다.  
- Sequence와 Collection 프로토콜을 따르는 타입: Array, Dictionary, Set  
- Optional  

2. Map  
컨테이너 내부 데이터를 연산할 때 활용한다. 기존 컨테이너 값들은 변경되지 않고, 새로운 컨테이너를 생성하여 반환한다.  
for-in 구문과 큰 차이는 없으나, 다음과 같은 장점이 있다.  
- 컴파일러 최적화 측면에서 성능이 좋다.  
- 멀티 스레드 환경에서 하나의 컨테이너에 여러 스레드들이 동시에 변경을 하려고 할 때 예측하지 못한 결과 발생을 방지할 수 있다.  
ex. Map 사용없이 구현  
	func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {  
    	var results: [Int] = []  
    	for command in commands {  
        	let splitedArray = array[(command[0] - 1)...(command[1] - 1)]  
        	let sortedArray = splitedArray.sorted()  
        	results.append(sortedArray[(command[2] - 1)])  
    	}  
    	return results  
	}  

	Map으로 구현 후,  
	- 표현이 간결하고 직관적이다.  
	- 새로운 컨테이너(배열)을 생성하여 반환하기 때문에 빈 컨테이너를 초기에 생성할 필요가 없다.  
	- append() 연산을 수행할 필요가 없다.  
	func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {  
        return commands.map({(key) in  
            return array[(key[0] - 1)...(key[1] - 1)].sorted()[key[2] - 1]  
        })  
    }  
  
    - 매개변수로 전달할 함수를 클로저 상수로 구현하면 코드를 재활용할 수 있다.  
    let evens = [0, 2, 4, 6, 8]  
	let odds = [1, 3, 5, 7, 9]  
	let multiplyTwo: (Int) -> Int = { $0 * 2 }  
	let doubledEvens = evens.map(multiplyTwo)  
	let doubledOdds = odds.map(multiplyTwo)  
  
3. Filter  
컨테이너 내부 데이터를 걸러내고자 할 때 활용한다. Filter의 매개변수로 전달되는 함수의 반환 타입은 Bool이다.  
true면 값을 포함하고 false면 값을 배제한다. Map과 마찬가지로 새로운 컨테이너를 생성하여 반환한다.
Map과 연결하여 활용가능하다.  
ex. let numbers = [0, 1, 2, 3, 4, 5]  
	let evens = numbers.filter{ $0 % 2 == 0 } // Results: evens = [0, 2, 4]  
	let odds = numbers.map{ $0 + 2 }.filter{ $0 % 2 != 0 } // Results: odds = [3, 5, 7]  
  
4. Reduce  
컨테이너 내부 데이터를 하나로 합산할 때 활용한다.  
정수 배열이라면 매개변수로 전달받은 함수의 연산대로 합산한다. 문자열 배열이라면 문자열을 하나로 합산한다.  
첫 번째 매개변수를 통해 초깃값을 지정할 수 있다. 이 초깃값이 최초의 $0으로 사용된다.  
다른 고차함수들과 함께 연결하여 활용가능하다.  
ex. let numbers = [1, 2, 3]  
	var sum = numbers.reduce(10) { $0 + $1 } // Results: sum = 16  