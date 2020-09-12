#### ARC  
Swift는 앱의 메모리 사용을 추적하고 관리하기 위해 Automatic Reference Counting을 사용한다.  
대부분의 경우, Swift에서 메모리 관리는 ARC가 맡아서 처리하며, 개발자는 메모리 관리를 신경쓸 필요가 없다.  
ARC가 자동으로 더이상 사용되지 않는 클래스 인스턴스에 사용된 메모리를 해제하기 때문이다.  

그러나 몇몇의 경우, ARC는 메모리 관리를 위해 더 많은 정보를 필요로 한다.  
참조 카운팅은 클래스 인스턴스에만 해당한다. Structure와 Enum은 참조 타입이 아닌 값 타입이며, 참조로 저장되거나 전달되지 않는다.  
  
#### 작동 방식  
클래스 인스턴스를 새로 만들 때마다 ARC는 해당 인스턴스의 정보를 저장하기 위한 메모리를 할당한다.  
할당된 메모리는 해당 인스턴스의 타입 정보와 인스턴스와 관련된 모든 저장된 속성값을 가지고 있다.  

그리고 인스턴스가 더이상 사용되지 않을 때, ARC는 메모리를 해제하여 다른 필요한 곳에 쓰일 수 있도록 한다.  
ARC는 클래스 인스턴스가 더이상 사용되지 않을 때 메모리에 자리를 차지하지 않도록 보장해준다.  

ARC가 여전히 사용 중인 인스턴스를 메모리에서 해제하면, 인스턴스의 속성에 더이상 접근할 수 없으며, 인스턴스의 메소드를 호출할 수 없다.  
해당 인스턴스에 접근하려할 경우, 앱은 강제 종료될 것이다.  

인스턴스가 여전히 사용 중일 때 사라지지 않도록 하기 위해, ARC는 각 클래스 인스턴스들이 어떻게 속성, 상수, 변수들을 참조하는지 추적한다.  
ARC는 하나라도 활성 참조가 남아있다면 인스턴스 메모리를 해제하지 않는다.  

속성, 상수, 변수에 클래스 인스턴스를 할당할 때마다 해당 속성, 상수, 변수는 인스턴스에 대해 강한 참조를 만든다.  
참조는 인스턴스를 확고하게 유지하고 강한 참조가 유지되는 한 메모리에서 해제하지 않기 때문에 '강한' 참조라 부른다.  
  
``` swift
class Person {
    let name: String
    init(name: String) { // 초기화
        self.name = name
        print("\(name) is being initialized")
    }
    deinit { // 초기화 해제
        print("\(name) is being deinitialized")
    }
}

var reference1: Person? // optional 타입이기 때문에 아직 참조되지 않는다.
var reference2: Person?
var reference3: Person?

reference1 = Person(name: "John Appleseed")
// Person 클래스의 Initializer를 호출했으므로 "John Appleseed is being initialized"가 출력되고,
// 메모리가 할당되었음을 알 수 있다.
// 변수 reference1은 Person 인스턴스에 대해 강한 참조를 한다.
// 최소 하나의 강한 참조가 있으므로 ARC는 Person 인스턴스를 메모리에 유지한다.

reference2 = reference1
reference3 = reference1 // 이제 3개의 강한 참조가 생겼다.

reference1 = nil
reference2 = nil // 강한 참조를 중단하려면 nil을 변수에 할당하면 된다.

reference3 = nil // 마지막까지 남아있던 강한 참조를 중단한다.
// "John Appleseed is being initialized"가 출력된다.
// ARC는 마지막 강한 참조가 중단될 때까지 Person 인스턴스를 메모리에서 해제하지 않는다.
```
  
#### 클래스 인스턴스 간의 강한 참조 순환  
두 클래스 인스턴스가 서로에게 강한 참조가 형성되어 있을 때, 각각의 인스턴스는 상대 인스턴스가 유지되도록 붙들어둘수 있다.  
이를 강한 참조 순환이라 하는데, 강한 참조 순환은 다음의 과정을 통해 해결할 수 있다.  
"클래스 간 관계성을 강한 참조 대신 weak 또는 unowned 참조로 선언하기."  
  
#### 강한 참조 순환의 발생 과정  
``` swift
class Person {
    let name: String
    init(name: String) { self.name = name }
    var apartment: Apartment?
    deinit { print("\(name) is being deinitialized") }
}

class Apartment {
    let unit: String
    init(unit: String) { self.unit = unit }
    var tenant: Person?
    deinit { print("Apartment \(unit) is being deinitialized") }
}

var john: Person?
var unit4A: Apartment?

john = Person(name: "John Appleseed")
unit4A = Apartment(unit: "4A")
```
  
위에 따르면, 변수 john은 Person 인스턴스에 대해 강한 참조가 생기고, 변수 unit4A는 Apartment 인스턴스에 대해 강한 참조가 생긴다.  
![Alt text](https://docs.swift.org/swift-book/_images/referenceCycle01_2x.png)  
  
``` swift
john!.apartment = unit4A
unit4A!.tenant = john
```
  
위와 같이 Person과 Apartment 두 인스턴스를 연결하면 두 인스턴스 간의 강한 참조 순환이 발생한다.  
![Alt text](https://docs.swift.org/swift-book/_images/referenceCycle02_2x.png)  
  
따라서 변수 john, unit4A의 강한 참조를 중단할 때, 참조 카운트는 0이 되지 못하고 ARC는 인스턴스를 메모리에서 해제하지 못한다.  
``` swift
john = nil
unit4A = nil
```
  
두 변수에 nil을 지정해도 deinitializer는 호출되지 않는다.  
강한 참조 순환이 Person, Apartment 인스턴스가 메모리에서 해제되는 것을 막아서 메모리 누수의 원인이 된다.  
![Alt text](https://docs.swift.org/swift-book/_images/referenceCycle03_2x.png)  
  
Person 인스턴스와 Apartment 인스턴스 간의 강한 참조는 여전히 남아있으며 중단될 수 없다.  
  
#### 클래스 인스턴스 간 강한 참조 순환 해결하기  
Swift는 강한 참조 순환을 해결하기 위해 다음 두가지 방법을 제공한다: weak 참조와 unowned 참조  

weak과 unowned 참조는 참조 순환 내의 한 인스턴스가 다른 인스턴스를 강한 연결 없이도 참조할 수 있다.  
인스턴스들은 강한 참조 순환 발생 없이 서로를 참조할 수 있다.  
  
weak 참조는 다른 인스턴스가 더 짧은 생명주기를 갖고 있을 때 사용한다. 즉, 다른 인스턴스가 먼저 메모리에서 해제될 수 있다.  
위 예제에서 Apartment는 생명주기 중 어느 시점에 tenant가 없을 수 있다.  
이 경우 weak 참조는 참조 순환을 중단하는 적절한 방법이다.  
반대로 다른 인스턴스의 생명주기가 동일하거나 더 긴 경우 unowned 참조를 사용한다.  
  
#### Weak 참조  
weak 참조는 인스턴스 참조를 강하게 유지하지 않아서 ARC가 참조 인스턴스를 메모리에서 해제하는 것을 멈추지 않는다.  
그래서 강한 참조 순환이 발생하지 않도록 방지해준다.  
속성이나 변수 선언 전에 weak 키워드를 사용하여 weak 참조를 할 수 있다.  
  
weak 참조는 참조하는 인스턴스를 강하게 유지하지 않기 때문에 weak 참조가 아직 참조 중임에도 해당 인스턴스가 메모리에서 해제될 수 있다.  
따라서 ARC는 참조하는 인스턴스가 해제될 때 자동으로 weak 참조를 nil로 지정한다.  
weak 참조는 런타임 중에 값을 nil로 바꿔야하기 때문에 항상 optional 타입의 변수로 선언된다.  
  
다른 optional 값처럼 weak 참조 값이 존재하는지 확인할 수 있고, 더이상 존재하지 않는 잘못된 인스턴스를 참조하지 않을 수 있다.  
  
``` swift
class Person {
    let name: String
    init(name: String) { self.name = name }
    var apartment: Apartment?
    deinit { print("\(name) is being deinitialized") }
}

class Apartment {
    let unit: String
    init(unit: String) { self.unit = unit }
    weak var tenant: Person? // weak 참조로 선언
    deinit { print("Apartment \(unit) is being deinitialized") }
}

var john: Person?
var unit4A: Apartment?

john = Person(name: "John Appleseed")
unit4A = Apartment(unit: "4A")

john!.apartment = unit4A
unit4A!.tenant = john
```
  
![Alt text](https://docs.swift.org/swift-book/_images/weakReference01_2x.png)  
  
Person 인스턴스는 여전히 Apartment 인스턴스에 대해 강한 참조를 하지만, Apartment 인스턴스는 Person 인스턴스에 대해 약한 참조를 한다.  
이제 john 변수에 nil을 지정하여 강한 참조를 중단하려 할 때, Person 인스턴스에는 더이상 강한 참조가 남아있지 않게 된다.  
  
``` swift
john = nil // Prints "John Appleseed is being deinitialized"
```
  
Person 인스턴스에 대한 강한 참조가 더이상 없기 때문에 메모리에서 해제되며 tenant 속성값은 nil이 된다.  
  
![Alt text](https://docs.swift.org/swift-book/_images/weakReference02_2x.png)  
  
변수 unit4A가 갖고있는 Apartment 인스턴스에 대한 강한 참조만 남는다.  
이 강한 참조를 중단하면, Apartment 인스턴스에 대한 강한 참조도 없다.  
  
``` swift
unit4A = nil // Prints "Apartment 4A is being deinitialized"
```
  
Apartment 인스턴스에 대한 강한 참조도 더이상 없기 때문에 이것도 메모리에서 해제된다.  
  
![Alt text](https://docs.swift.org/swift-book/_images/weakReference03_2x.png)  
  
#### Unowned 참조  
weak 참조와 마찬가지로 unowned 참조는 참조하는 인스턴스를 강하게 유지하지 않는다.  
그러나 weak 참조와 달리 unowned 참조는 다른 인스턴스가 동일하거나 더 긴 생명주기를 갖고 있을 때 사용한다.  
속성이나 변수 선언 전에 unowned 키워드를 사용해 unowned 참조를 할 수 있다.  
  
weak 참조와 달리 unowned 참조는 항상 값을 가질 것으로 예상된다.  
따라서 unowned 값은 optional하지 않고, ARC는 unowned 참조값에 nil을 지정하지 않는다.  
  
> unowned 참조는 참조가 *항상* 메모리에서 해제되지 않을 인스턴스를 참조할 때만 사용한다.  
> 인스턴스가 메모리에서 해제된 후 unowned 참조값에 접근하려하면 런타임 에러가 발생한다.  
  
``` swift
class Customer {
    let name: String
    var card: CreditCard?
    init(name: String) {
        self.name = name
    }
    deinit { print("\(name) is being deinitialized") }
}

class CreditCard {
    let number: UInt64
    unowned let customer: Customer
    init(number: UInt64, customer: Customer) {
        self.number = number
        self.customer = customer
    }
    deinit { print("Card #\(number) is being deinitialized") }
}
```
  
CreditCard는 항상 Customer를 갖는다. 그리고 절대 참조하는 Customer보다 생명주기가 길지 않다.  
따라서 강한 참조 순환을 피하기 위해 CreditCard 클래스는 non-optional한 unowned Customer 속성을 갖는다.  
  
> CreditCard 클래스의 number 속성은 Int보다 UInt64 타입으로 선언한다.  
> number 속성의 용량이 32bit와 64bit 시스템 모두에서 16 자리 카드 번호를 저장하기 충분하기 때문이다.  
  
``` swift
var john: Customer?

john = Customer(name: "John Appleseed")
john!.card = CreditCard(number: 1234_5678_9012_3456, customer: john!)
```
  
![Alt text](https://docs.swift.org/swift-book/_images/unownedReference01_2x.png)  
  
unowned한 customer 참조 때문에, 변수 john의 강한 참조를 중단할 때 Customer 인스턴스에 대한 강한 참조는 없어진다.  
  
![Alt text](https://docs.swift.org/swift-book/_images/unownedReference02_2x.png)  
  
Customer 인스턴스에 대한 강한 참조가 더이상 없기 때문에 인스턴스는 메모리에서 해제된다.  
그 후, CreditCard 인스턴스에 대한 강한 참조도 없기 때문에 마찬가지로 메모리에서 해제된다.  
  
``` swift
john = nil
// Prints "John Appleseed is being deinitialized"
// Prints "Card #1234567890123456 is being deinitialized"
```
  
> 위 예제는 안전한 unowned 참조를 어떻게 사용하는지 보여준다.  
> Swift는 성능 등을 이유로 runtime safety check를 비활성화할 경우를 위해 불안전한 unowned 참조도 제공한다.  
> 이런 경우, 안전성을 확인할 책임은 개발자에게 있다.  
> unowned 참조는 unowned(unsafe)를 사용한다.  
> 참조하는 인스턴스가 메모리에서 해제된 후 불안전한 unowned 참조에 접근하면, 프로그램이 인스턴스가 사용하던 메모리 위치에 접근하게 되어서 불안전하게 된다.  
  
#### Unowned Optional 참조  
클래스에 대한 unowned 참조는 optional 할 수 있다.  
ARC 관점에서 unowned optional 참조와 weak 참조는 동일한 상황(same contexts)에서 쓰일 수 있다.  
단지 unowned optional 참조를 사용할 때 개발자는 항상 유효한 객체를 참조하거나 nil을 할당하도록 주의해야 한다.  
  
``` swift
class Department {
    var name: String
    var courses: [Course]
    init(name: String) {
        self.name = name
        self.courses = [] // 강한 참조 
    }
}

class Course {
    var name: String
    unowned var department: Department // Course는 항상 Department를 갖는다.
    unowned var nextCourse: Course? // 다음 Course는 없을 수 있다.
    init(name: String, in department: Department) {
        self.name = name
        self.department = department
        self.nextCourse = nil
    }
}

let department = Department(name: "Horticulture")

let intro = Course(name: "Survey of Plants", in: department)
let intermediate = Course(name: "Growing Common Herbs", in: department)
let advanced = Course(name: "Caring for Tropical Plants", in: department)

intro.nextCourse = intermediate
intermediate.nextCourse = advanced
department.courses = [intro, intermediate, advanced]
```
  
![Alt text](https://docs.swift.org/swift-book/_images/unownedOptionalReference_2x.png)  
  
