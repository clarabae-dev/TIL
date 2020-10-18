## KVC  
KVC, Key-Value Coding은 프로퍼티명인 문자열을 사용해 프로퍼티에 접근할 수 있게 해준다.  
프로퍼티 접근자를 사용하거나 변수에 직접 접근하지 않아 객체 간 의존성을 낮추고 결합도가 낮은 개발이 가능하다.  
이 매커니즘이 가능하기 위해서는 클래스들이 NSKeyValueCoding protocol을 준수해야 한다.  
    
  
### NSKeyValueCoding Protocol  
모든 클래스들은 KVC & KVO를 사용하기 위해 반드시 NSKeyValueCoding 프로토콜을 준수해야 한다.  
NSObject는 이 프로토콜을 준수한다. 따라서 Foundation 프레임워크에서 정의하고 NSObject를 상속하는 모든 클래스들은 이 프로토콜을 준수한다.  
  
### Key & KeyPath  
1. Key  
값을 할당하거나 값을 가져오려는 하나의 프로퍼티를 가리키기 때문에 Key의 이름은 프로퍼티의 이름과 같다.  
2. KeyPath  
dot-syntax 형태로 되어있어서 하나의 단어나 문장이 아니다.  
Key-path는 원하는 값/프로퍼티에 도달할 때까지 나타나는 객체의 모든 프로퍼티들을 나타낸다.  
  
### Logic  
1. key와 일치하는 프로퍼티를 찾는다.  
2. 일치하는 프로퍼티가 없을 경우, key와 일치하는 인스턴스 변수를 찾는다.  
3. 일치하는 프로퍼티나 인스턴스 변수가 있으면 이를 적용한다. 없으면 valueForUndefinedKey: 또는 setValue:forUndefinedKey:를 호출한다.  
  
런타임에 접근하기 때문에 key가 일치하지 않으면 crash가 발생하기도 한다.  
  
### Dynamic Dispatch  
Objective-C에서 런타임 때 특정 방법이나 기능의 구현을 호출해야할지 결정하는 것을 가리켜 Dynamic Dispatch 라 부른다.  
서브클래스가 슈퍼클래스의 메소드를 오버라이드 할 때, dynamic dispatch는 하위 클래스와 상위 클래스의 구현 중 어떤 방법을 실행해야 하는지 파악한다.  
  
Swift는 가능한한 Swift 런타임을 사용한다.  
Objective-C는 dynamic dispatch에만 의존하지만, Swift는 다른 선택의 여지가 없는 경우에만 dynamic dispatch를 선택한다.  
컴파일러가 컴파일 시간에 어떤 방법을 구현해야할지 알아낼 수 있다면 dynamic dispatch를 선택하지 않을 수 있다.  
Core Data나 KVO 등은 dynamic dispatch를 사용하는 Objective-C 런타임에만 가능하다.  
  
클래스의 멤버에 'dynamic' 키워드를 적용하면, 해당 멤버에 액세스하기 위해서는 dynamic dispatch를 사용해야 한다고 컴파일러에게 알릴 수 있다.  
  
'dynamic' 키워드를 접두사로 붙임으로써 멤버 선언에는 objc 속성이 암시적으로 표시된다.  
objc 속성은 해당 요소를 Objective-C에서 사용할 수 있게 하며, Objective-C 런타임 때 접근할 수 있다.  
  
'dynamic' 키워드는 클래스 멤버에만 사용할 수 있다.  
structure와 enum은 상속을 허용하지 않으므로 어떤 구현을 사용해야 하는지 런타임이 알 필요가 없다.  
  
따라서 Swift에서 KVC, KVO를 사용하기 위해서는 observe하기 원하는 속성들을 @objc dynamic 키워드와 함께 선언해야 한다.  
  
```swift
@objc class Book: NSObject {
	@objc dynamic var title = "What"
}

self.book.setValue("Harry Potter", forKey: "title")
let bookTitle = self.book.value(forKey: "title") as! String
```  
  
1. 속성에 값을 할당할 때 속성명과 동일한 키를 사용한다. setValue:forKey:  
2. 속성에서 값을 가져올 때 속성명과 동일한 키를 사용한다. valueForKey:  
  
속성명과 다른 키를 사용하면 앱은 강제종료될 것이며, **속성명과 동일한 키**를 사용하는 것이 매우 중요하다.  
  
  
  
## KVO  
KVO, Key-Value Observing은 속성의 변화를 추적하고자 할 때 사용하는 코딩의 한 형태이다.  
willSet, didSet 등과 달리 소스를 마음대로 변경할 수 없는 외부 라이브러리 프로퍼티를 관찰할 때 KVO 방식을 쓸 수 있다.  
즉, 상속이나 코드 변경없이 관찰할 수 있는 방법이다.  
  
1. 내부 속성을 관찰하려는 클래스는 KVO와 호환되어야 한다. 즉, 다음을 준수해야 한다.  
- 클래스는 반드시 KVC와 호환되어야 한다.  
- 클래스는 자동 또는 수동으로 알림을 보낼 수 있어야 한다.  
2. 다른 클래스의 속성을 관찰하기 위해 사용될 클래스는 observer로 설정해야 한다.  
3. 다음 메소드는 관찰 대상인 클래스에 구현되어야 한다. observeValueForKeyPath:ofObject:change:context:  
  
  
### Make Class Observe  
속성의 변화를 관찰하기 위해 가장 중요한 점은 클래스가 이 변화들을 관찰하게 하는 것이다.  
NSNotifications으로도 어느 정도 관찰은 가능하지만, addObserver 메소드를 사용한다.  
  
```swift
override func viewWillAppear(_ animated: Bool) {
	super.viewWillAppear(animated)

	self.book.addObserver(self, forKeyPath: "title", options:[.new, .old], context: bookContext)
}
```  
  
1. addObserver: 속성을 관찰할 클래스로 보통 속성을 선언한 클래스 자기 자신, self 이다.  
2. forKeyPath: 관찰하려는 속성에 맞는 키 또는 key path이다. 하나의 키 또는 key path만 명시해야 한다.  
3. options: NSKeyValueObservingOptions.  
4. context: 관찰하려는 속성의 변경에 대한 고유 식별자로 사용할 수 있는 포인터다. 보통은 nil 또는 NULL을 할당한다.  
  
addObserver 메소드로 클래스가 속성을 관찰하게 만든 뒤 observeValueForKeyPath:ofObject:change:context:를 구현한다.  
observeValueForKeyPath:ofObject:change:context: 메소드는 속성 값이 변경될 때마다 호출된다.  
KVO는 observeValue 위 메소드 내에 관찰하려는 속성 갯수만큼 if문이 생긴다는 단점이 있지만 그를 상쇄하는 이점이 있다.  
바로 속성이 변경되었다는 알림을 받는 것이 매우 쉽다는 점이다.  
  
addObserver 메소드의 context: UnsafeMutableRawPointer 매개변수를 활용하여 어느 속성이 변경되었는지 명확한 알림을 받을 수 있다.  
context에 nil 대신 속성마다 context를 각각 할당하면 된다.  
이 때 글로벌 변수로 선언하여 observeValueForKeyPath.. 메소드에서도 사용할 수 있도록 한다.  
  
```swift
override func observeValue(forKeyPath keyPath: String?, of object: Any?, change: [NSKeyValueChangeKey : Any]?, context: UnsafeMutableRawPointer?) {
	if context == bookContext {
		if keyPath == "title" {
			print(change![NSKeyValueChangeKey.newKey] as! String)
			print(change![NSKeyValueChangeKey.oldKey] as! String)
		}
	}
}
```  
  
또한, 추가한 observer는 잊지않고 제거해주어야 한다. 적절한 곳에 removeObserver 메소드를 추가한다.  
  
```swift
override func viewWillDisappear(_ animated: Bool) {
	super.viewWillDisappear(animated)

	self.book.removeObserver(self, forKeyPath: "title", context: bookContext)
}
```  
  
  
  
출처: https://medium.com/hackernoon/kvo-kvc-in-swift-12f77300c387  