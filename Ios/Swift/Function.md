### _ underscore  
Swift는 함수 argument마다 name을 붙일 것을 요구한다. 함수를 호출할 때도 argument name을 꼭 명시한다.  
name없이 underscore를 argument 앞에 붙일 경우, 함수 호출에서 argument name을 명시하지 않아도 된다.  
단일 argument나 name을 명시할 필요가 없는 경우 활용하면 좋다.  
  
### Argument  
1. 기본값  
매개변수에 전달될 기본값을 미리 지정할 수 있다. 기본값을 갖는 매개변수는 가장 뒤쪽에 위치하는 것이 좋으며 함수 호출 때 생략할 수 있다.  
  
```swift
func greeting(friend: String, me: String = "gogo")
greeting(friend: "Kim")
```  
  
2. 레이블  
함수를 호출할 때 매개변수의 역할을 더 명확하게 표현할 수 있다.  
  
```swift
func greeting(to friend: String, from me: String)
```  
  
3. 가변 매개변수  
매개변수로 넘어올 값의 개수를 알기 어려울 때 사용하며, 함수당 하나만 가질 수 있다.  
  
```swift
func hello(me: String, friends: String...) -> String {
	return "Hello \(friends)! I'm \(me)."
}
hello(me: "gogo", friends: "hana", "eric", "wing")
// Hello ["hana", "eric", "wing"]! I'm gogo.
```  
  
  
### First-Class Object  
일급 객체란, 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가리킨다.  
Swift는 함수형 프로그래밍 패러다임을 포함하는 다중 패러다임 언어로 Swift의 함수 또한 일급 객체이다.  
그래서 함수를 변수, 상수, 등에 할당할 수 있고 매개변수로 전달할 수도 있다.  

### 랜덤함수  
1. arc4random() -> UInt32  
0 ~ (2^32 - 1) 사이의 난수를 반환  
2. arc4random_uniform(UInt32) -> UInt32  
UInt32 타입의 파라미터를 받을 수 있다.  
0 ~ (파라미터로 넣은 UInt32 - 1) 사이의 난수를 반환  
3. drand48() -> Double  
0 ~ 1.0 사이의 난수를 반환  

### @discardableResult  
값을 리턴하는데 결과를 사용하지 않는 함수 또는 메소드가 호출될때 컴파일러 경고를 표시 하지않을 때 사용한다.  
Warning: Result of call to '~~' is unused  
  
  
  
출처: https://github.com/yagom/swift_basic/tree/master/contents/04_function  