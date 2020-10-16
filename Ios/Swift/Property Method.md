## Property  
1. 저장 프로퍼티: 인스턴스의 변수 또는 상수를 의미하고, class와 struct에서 쓰인다.  
2. 연산 프로퍼티: 연산을 실행한 결과값으로 저장값이 아니다. class, struct, enum에 쓰인다.  
3. 타입 프로퍼티: 특정 타입에 사용된다.  
4. 프로퍼티 감시자: 프로퍼티 값이 변하는 것을 감시하다가 값이 변할 때 그에 따른 특정 작업을 수행한다.  
  
  
### 저장 프로퍼티  
- with var: 변수 저장 프로퍼티.  
- with let: 상수 저장 프로퍼티.  
  
#### 지연 저장 프로퍼티  
lazy var, 실제 사용이 될 때 값이 할당되는 프로퍼티이다. 호출이 있어야 값을 초기화하기 때문에 불필요한 공간 낭비를 줄일 수 있다.  
다만, 멀티스레드 환경에서는 한번만 초기화 된다는 보장이 없다.  
  
### 연산 프로퍼티  
실제 값을 저장하지 않고 값을 연산하여 var로만 선언할 수 있는 프로퍼티이다. getter/setter와 동일한 동작을 한다.  
종류에는 접근자 get과 설정자 set이 있다.  
읽기 전용으로 구현할 수는 있지만, 쓰기 전용으로는 구현할 수 없다.  
  
```swift
var oppositePoint: CoordinatePoint {
	get {
		return CoordinatePoint(x: -x, y:-y)
	}
	set {
		x = -newValue.x // 매개변수를 생략하고 newValue를 사용할 수 있다.
		y = -newValue.y
	}
}
```  
  
  
### 타입 프로퍼티  
인스턴스가 아닌 타입 자체에 속하는 프로퍼티로 인스턴스를 생성하지 않고도 사용할 수 있다.  
인스턴스 생성 여부와 관계없이 타입 프로퍼티의 값은 하나이며, 해당 타입의 모든 인스턴스가 공유하는 값이다.  
저장 타입 프로퍼티는 변수 또는 상수로 선언할 수 있고, 연산 타입 프로퍼티는 변수로만 선언할 수 있다.  
멀티 스레드 환경이라도 단 한번만 초기화된다.  
  
```swift
Sample {
	static var typeProperty: Int = 0
}
Sample.typeProperty = 300
```  
  

### 프로퍼티 감시자  
프로퍼티 값이 변경됨에 따라 적절한 작업을 수행할 수 있다.  
lazy var, 지연 저장 프로퍼티에서는 사용할 수 없으며 저장 프로퍼티에서만 사용할 수 있다.  
- willSet: 프로퍼티 값 변경 직전 호출되는 메소드이다.  
- didSet: 프로퍼티 값이 변경된 직후 호출되는 메소드이다.  
  
```swift
var credit: Int = 0 {
	willSet {
		print("잔액이 \(credit)원에서 \(newValue)원으로 변경될 예정입니다.")
	}
	didSet {
		print("잔액이 \(oldValue)원에서 \(credit)원으로 변경되었습니다.")
	}
}
```  
  
  
  
  
## Method  
  
  
### Mutating  
struct, enum 등 값 타입은 메소드 앞에 mutating 키워드를 사용해 해당 메소드가 인스턴스 내부의 프로퍼티를 변경한다는 것을 명시해주어야 한다.  
참조 타입인 class와 달리 값 타입은 self 프로퍼티를 사용해 자기 자신을 치환할 수도 있다.  
  
```swift
enum OnOffSwitch{
    case on, off
    mutating func nextState(){
        self = self == .on ? .off : .on
    }
}
```  
  
  
### Type Method  
타입 자체에 호출할 수 있는 메소드로 static과 class 키워드를 사용할 수 있다.  
- static: 상속 후 메소드 오버라이드가 불가능하다.  
- class: 상속 후 메소드 오버라이드가 가능하다.  
  
```swift
class AClass{
    static func staticTypeMethod()
    class func classTypeMethod()
}

class BCalss: AClass{
    override class func classTypeMethod(){
        print("BClass classTypeMethod")
    }
}
AClass.staticTypeMethod()
BClass.classTypeMethod()
```  
  
  
  
  
출처: https://velog.io/@wimes/10.-%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0%EC%99%80-%EB%A9%94%EC%84%9C%EB%93%9C  