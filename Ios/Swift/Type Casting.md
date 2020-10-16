## Type Casting  
스위프트에서 Type casting은 is와 as 연산자로 구현할 수 있다.  
1. 타입 확인 연산자  
is를 사용해 타입을 확인한다. Class 또는 Struct 또는 데이터의 타입을 확인할 수 있다.  
2. Up Casting  
as를 사용해 상위 클래스의 인스턴스로 사용할 수 있도록 컴파일러에 타입 정보를 전환해준다.  
Any 또는 AnyObject로도 타입 정보를 변환할 수 있다. 암묵적으로 처리되기 때문에 생략할 수 있다.  
  
```swift
var mike: Person = UniversityStudent() as Person
var jina: Any = Person()
```  
  
3. Down Casting  
하위 클래스로 변환하는 연산자이다. 하위 클래스의 인스턴스로 사용할 수 있도록 컴파일러에 인스턴스 타입 정보를 전환해준다.  
- as?  
조건부로 Downcasting하려는 타입의 Optional 값을 반환한다.  
실패할 경우 nil을 반환하며, 컴파일 타임에 타입 변환의 가능/불가능 여부를 알 수 없다.  
  
```swift
var optionalCasted: Student?
optionalCasted = mike as? UniversityStudent
```  
  
- as!  
강제로 Downcasting한 optional이 아닌 일반 값을 반환한다. 잘못된 Downcasting을 할 경우 런타임 에러가 발생한다.  
컴파일 타임에 타입 변환의 가능/불가능 여부를 알 수 없다.  
  
  
  
출처: https://github.com/yagom/swift_basic/tree/master/contents/17_type_casting  