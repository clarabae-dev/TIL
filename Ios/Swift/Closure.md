#### 함수형 프로그래밍  
스위프트는 객체지향 언어이자, 함수형 언어이다.  
closure는 함수형 프로그래밍의 특징을 오롯이 지니고 있다.  
함수형 프로그래밍이란,  
1. 대입문없이 프로그래밍하는 것이다.  
> 어떤 값을 할당받고 반환하고 할 필요가 없다.  

- 일반적인 함수  
```swift
func hello() { print("안녕하세요") }  
hello() // 안녕하세요  

// closure expression  
{ (parameters) -> return type in  
    statements  
}

({ ( ) -> Void in  
    print("안녕하세요")  
})() // 안녕하세요  
```
> 함수 이름이 없기 때문에 Anonymous Function, 익명함수라고도 불린다.  

2. 참조투명성을 지킨다.  
메모리 측면에서, 참조투명성을 지킨다는 의미는 일단 값이 할당된 위치에는 새로운 값을 할당하지 않는다는 뜻.  
참조투명성 조건을 만족하는 함수는 수없이 호출하더라도 항상 동일한 값을 반환한다.  
함수형 프로그래밍은 대입문이 없으므로 메모리를 참조하는 것이 아니라 호출, callback 한다.  
closure는 주로 비동기 callback 함수로 쓰인다.  

#### Capture Value  
closrue는 클래스와 같은 참조 타입이다.  
만약 클로저를 변수로 선언하거나 파라미터로 넘긴다면 클로저는 힙 안에 들어갈 것이고, 강한 참조가 생기게 된다.  
클로저 내부에서 self에 접근하게 되면 클로저와 self 사이의 강한 순환 참조가 발생한다.  
이 경우, [unowned self] 또는 [weak self]를 사용해 순환 참조의 고리를 끊을 수 있다.  

#### noescape closure  
함수 파라미터로 closure가 전달될 때, 이 closure는 noescape가 기본이다.  
함수 종료 전에 closure는 사용되고, 함수 종료 후 closure는 필요없기 때문에 메모리에서 사라지게 된다.  
덕분에 retain cycle issue와 같은 메모리 관리에 덜 신경쓸 수 있게 되었다.  
함수 파라미터 closure는 noescape이 기본이지만, escape 하고자 하면 @escaping keyword를 앞에 붙여준다.  
*boilerplate code: 최소한의 변경으로 여러 곳에서 재사용되며, 반복적으로 비슷한 형태를 띄는 코드*  

#### escaping closure  
함수 종료 후 closure가 실행된다.  
- closure 저장: 글로벌 변수에 closure를 저장하여 함수가 종료된 후에 사용되는 경우.  
- 비동기 작업: 네트워크 통신 등에서 함수가 종료되어도 closure를 메모리에 잡아두어 비동기 작업을 수행.  
메모리 관리의 용이성을 위해 클로저는 변수에 할당하기 보다 직접 호출하여 사용한다.  
단, 변수에 할당할 경우, self 키워드를 명시적으로 사용해야 한다.  
함수가 return된 뒤에도 탈출한 클로저가 어떤 객체를 참조하고 있는지 기억하기 위해서이다.  
