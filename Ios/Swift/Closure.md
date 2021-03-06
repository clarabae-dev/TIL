## Closure  
closure는 코드의 블럭이다. 함수는 closure의 일종으로 이름이 있는 closure 라고 볼 수 있다.  
일급 객체로 전달인자, 변수, 상수 등으로 저장 또는 전달이 가능하다.  
  
  
### 함수형 프로그래밍  
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
  
### noescape closure  
함수 파라미터로 closure가 전달될 때, 이 closure는 noescape가 기본이다.  
함수 종료 전에 closure는 사용되고, 함수 종료 후 closure는 필요없기 때문에 메모리에서 사라지게 된다.  
덕분에 retain cycle issue와 같은 메모리 관리에 덜 신경쓸 수 있게 되었다.  
함수 파라미터 closure는 noescape이 기본이지만, escape 하고자 하면 @escaping keyword를 앞에 붙여준다.  
*boilerplate code: 최소한의 변경으로 여러 곳에서 재사용되며, 반복적으로 비슷한 형태를 띄는 코드*  
  
### escaping closure  
함수 종료 후 closure가 실행된다.  
- closure 저장: 글로벌 변수에 closure를 저장하여 함수가 종료된 후에 사용되는 경우.  
- 비동기 작업: 네트워크 통신 등에서 함수가 종료되어도 closure를 메모리에 잡아두어 비동기 작업을 수행.  
메모리 관리의 용이성을 위해 클로저는 변수에 할당하기 보다 직접 호출하여 사용한다.  
단, 변수에 할당할 경우, self 키워드를 명시적으로 사용해야 한다.  
함수가 return된 뒤에도 탈출한 클로저가 어떤 객체를 참조하고 있는지 기억하기 위해서이다.  
  
#### Implicit capturing of self in Swift 5.3  
Swift 5.3 이전 버전에서는 escaping closure 내부에서 인스턴스 메소드나 프로퍼티에 접근할 때 명시적으로 self를 사용해야 했다.  
  
```swift
struct ListView: View {
    @ObservedObject var viewModel: ListViewModel

    var body: some View {
        List {
            ForEach(viewModel.items) { item in
                Text(item.text)
            }
            .onDelete {
                self.viewModel.deleteItems(at: $0)
            }

            Button("Delete all items") {
                self.viewModel.deleteAllItems()
            }
            .foregroundColor(.red)
        }
    }
}
```  
  
Swift 5.3에서는 그러나 위와 같이 강한 참조가 형성되지 않을 경우에는 self가 필요없어졌다.  
SwiftUI view는 가벼운 struct이므로 subview들에 대해 강한 참조를 형성하지 않는다.  
  
```swift
struct ListView: View {
    @ObservedObject var viewModel: ListViewModel

    var body: some View {
        List {
            ForEach(viewModel.items) { item in
                Text(item.text)
            }
            .onDelete {
                viewModel.deleteItems(at: $0)
            }

            Button("Delete all items") {
                viewModel.deleteAllItems()
            }
            .foregroundColor(.red)
        }
    }
}
```  
  
  
  
  
## Capture Value  
Closure Capture란, closure가 매개변수나 지역변수가 아닌 주변 외부의 context를 참조하는 것을 뜻한다.  
capture를 해두어야 외부 context가 없어져도 closure가 해당 context를 사용할 수 있다.  
  
  
### Explicit Capture  
  
```swift
viewModel.includeStudio.asDriver()
            .drive {
                if $0 {
                    self.studioButton.setIncludedButton()
                    self.viewModel.removeRoomFilter(type: RoomType.studio)
                } else {
                    self.studioButton.setExcludedButton()
                    self.viewModel.appendRoomFilter(type: RoomType.studio)
                }
                self?.viewModel.fetchRooms()
            }.disposed(by: disposeBag)
```  
  
위 예시에서 외부의 UI 컴포넌트들을 참조하기 위해 VC의 self를 참조하였다.  
참조한 순간, closure는 인스턴스를 capture하고 실제 closure가 메모리에서 해제되기 전까지 참조한 인스턴스를 메모리에서 해제하지 않는다.  
  
### Capture Lists  
앞 예시의 경우 클로저와 self 사이에 상호간 강한 참조가 형성되어 강한 순환 참조가 발생할 수 있다.  
이를 방지하기 위해 capture list를 활용하여 약한 참조로 변경할 수 있다.  
  
```swift
viewModel.includeStudio.asDriver()
            .drive { [weak self] in
                if $0 {
                    self?.studioButton.setIncludedButton()
                    self?.viewModel.removeRoomFilter(type: RoomType.studio)
                } else {
                    self?.studioButton.setExcludedButton()
                    self?.viewModel.appendRoomFilter(type: RoomType.studio)
                }
                self?.viewModel.fetchRooms()
            }.disposed(by: disposeBag)
```  
  
  
  
  
참조:  
https://www.swiftbysundell.com/tips/implicit-capturing-of-self/  
https://www.swiftbysundell.com/articles/swifts-closure-capturing-mechanics/  