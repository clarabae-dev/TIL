> RxSwift github의 해당 내용을 번역 및 추가한 내용입니다.
  
## Why use Rx?  
Rx는 선언적 방식으로 앱을 작성할 수 있도록 해준다.  
  
  
### Bindings  
  
```swift
Observable.combineLatest(firstName.rx.text, lastName.rx.text) { $0 + " " + $1 }
	.map { "Greetings, \($0)" }
	.bind(to: greetingLabel.rx.text)
```  
  
UITableView와 UICollectionView에도 적용할 수 있다.  
  
```swift
viewModel.rows
	.bind(to: resultsTableView.rx.items(cellIdentifier: "WikipediaSearchCell", cellType: WikipediaSearchCell.self)) { (_, viewModel, cell) in
		cell.title = viewModel.title
		cell.url = viewModel.url
	}.disposed(by: disposeBag)
```  
  
.disposed(by: disposeBag)은 간단한 바인딩이라 꼭 필요하지 않더라도 항상 사용할 것을 권장한다.  
  
### Retries  
  
```swift
func doSomethingIncredible(forWho: String) throws -> IncredibleThing
```  
  
위와 같은 함수를 사용할 때, 만약 실패한다면 재시도하기가 매우 힘들다. Rx를 활용하면 다음과 같이 재시도할 수 있다.  
  
```swift
doSomethingIncredible("me").retry(3)
```  
  
  
### Delegates  
지루하고 비표현적인 코드를:  
  
```swift
public func scrollViewDidScroll(scrollView: UIScrollView) { [weak self]
	self?.leftPositionConstraint.constant = scrollView.contentOffset.x
}
```  
  
다음과 같이 작성할 수 있다.  
  
```swift
self.resultsTableView
	.rx.contentOffset
	.map { $0.x }
	.bind(to: self.leftPositionConstraint.rx.constant)
```  
  
  
### KVO  
  
```swift
'TickTock'은 KVO가 등록되어 있는 동안 메모리에서 해제되었다. 관찰 정보가 누수되었고, 다른 객체에 잘못 연결되었을 수 있다.  

-(void)observeValueForKeyPath: (NSString *)keyPath
					 ofObject: (id)object
					   change: (NSDictionary *)change
					  context: (void *)context
```  
  
위 내용 대신 rx.observe와 rx.observeWeakly를 사용할 수 있다.  
  
```swift
view.rx.observe(CGRect.self, "frame")
	.subscribe(onNext: { frame in
			print("Got new frame \(frame)")
		}).disposed(by: disposeBag)

someSuspiciousViewController
	.rx.observeWeakly(Bool.self, "behavingOk")
	.subscribe(onNext: { behavingOk in
			print("Cats can purr? \(behavingOk)")
		}).disposed(by: disposeBag)
```  
  
  
### Notifications  
  
```swift
@available(iOS 4.0, *)
public func addObserverForName(name: String?, object obj: AnyObject?, queue: NSOperationQueue?, usingBlock block: (NSNotification) -> Void) -> NSObjectProtocol
```  
  
위와 같이 사용하는 대신 다음과 같이 쓸 수 있다.  
  
```swift
NotificationCenter.default
	.rx.notification(NSNotification.Name.UITextViewTextDidBeginEditing, object: myTextView)
	.map { /*do someghing with data*/}
```  
  
  
### Transient state  
비동기 프로그램을 작성할 때 일시적인 상태에 대한 수많은 문제들이 있다. 그 일례로 검색창의 자동완성이 있다.  

Rx 없이 자동완성 코드를 작성한다면, 첫번째 문제는 abc에서 c의 입력 시점을 알아야한다는 것이다. ab에 대한 대기 중인 요청이 있고, 이 대기 요청은 취소될 것이다.  
이를 해결하기 위해 쉽게 대기 요청을 참조할 추가적인 변수를 만들 수도 있다.  
  
다음 문제는 요청이 실패하였을 때, 매우 지저분한 retry 로직을 작성해야 한다는 점이다. 물론 몇 개의 필드를 더 추가해 retry 횟수를 파악할 수도 있다.  
  
유저가 오래 입력하고 있을 경우 등을 대비해 서버에 요청하기 전 프로그램이 얼마간 대기할 수 있다면 매우 좋을 것이다. 추가적인 타이머가 더 필요할지도 모른다.  
  
검색을 수행할 동안 화면에 무엇을 보여주어야 할지도 궁금할 것이고, 모든 재시도가 실패한 후에 무엇을 보여주어야 할지도 궁금할 것이다.  
  
이 모든 것을 작성하고 적절하게 테스트하는 것은 매우 지루할 것이다. 동일한 로직을 Rx로 작성하면 다음과 같다.  
  
```swift
searchTextField.rx.text
	.throttle(.milliseconds(300), scheduler: MainScheduler.instance)
	.distinctUntilChanged()
	.flatMapLatest { query in
		API.getSearchResults(query)
			.retry(3)
			.startWith([]) // clears results on new search term
			.catchErrorJustReturn([])
	}
	.subscribe(onNext: { results in
		// bind to ui
	}).disposed(by: disposeBag)
```  
  
어떤 추가적인 flag나 field도 더 필요하지 않다.  
  
### Compositional disposal  
blur 처리된 이미지들을 보여주는 테이블뷰가 있다. 이미지들은 먼저 URL에서 fetch된 다음, 디코딩되어 blur 처리될 것이다.  
  
blur 작업 비용이 비싸기 때문에 셀이 테이블뷰가 보여지는 영역을 벗어난 경우, 전체 프로세스가 취소된다면 좋을 것이다.  
  
또한, cell이 보여지는 영역에 진입한 후 이미지를 곧바로 fetch하지 않아야 좋을 것이다. 유저가 매우 빠르게 스와이프하면, 수많은 요청이 발생했다가 취소될 것이다.  
  
blur 작업 비용이 비싸기 때문에 동시에 처리할 이미지 개수도 제한하는 것이 좋을 것이다.  
  
이를 Rx로 작업하면 다음과 같다.  
  
```swift
let imageSubscription = imageURLs
							.throttle(.milliseconds(200), scheduler: MainScheduler.instance)
							.flatMapLatest { imageURL in
								API.fetchImage(imageURL)
							}
							.observeOn(operationScheduler)
							.map { imageData in
								return decodeAndBlurImage(imageData)
							}
							.observeOn(MainScheduler.instance)
							.subscribe(onNext: { blurredImage in
								imageView.image = blurredImage
							}).disposed(by: disposeBag)
```  
  
위 코드는 모든 내용을 수행하고, imageSubscription이 dispose 될 때, 모든 비동기 operation을 취소하여 이상한 이미지가 UI에 바인딩되지 않도록 할 것이다.  
  
### Aggregating network requests  
두가지 요청을 해야하고 반환된 각 결과를 합쳐야 한다면 어떻게 해야할까? 다음처럼 zip operator를 활용할 수 있다.  
  
```swift
let userRequest: Observable<User> = API.getUser("me")
let friendRequest: Observable<[Friend]> = API.getFriends("me")

Observable.zip(userRequest, friendRequest) { user, friends in
	return (user, friends)
}
.subscribe(onNext: { user, friends in
	// bind them to the user interface
}).disposed(by: disposeBag)
```  
  
백그라운드 스레드에서 API가 결과를 리턴하고, 메인 UI 스레드에서 결과를 바인딩해야할 때는 어떻게 해야 할까? 다음처럼 observeOn을 활용할 수 있다.  
  
```swift
let userRequest: Observable<User> = API.getUser("me")
let friendRequest: Observable<[Friend]> = API.getFriends("me")

Observable.zip(userRequest, friendRequest) { user, friends in
	return (user, friends)
}
.observeOn(MainScheduler.instance)
.subscribe(onNext: { user, friends in
	// bind them to the user interface
}).disposed(by: disposeBag)
```  
  
  
### State  
mutation, 변화를 허락하는 언어는 전역 상태에 접근하기 쉽고 변경할 수 있게 해준다. 
공유되는 전역 상태 변경을 제어하지 않으면 Combinatorial explosion을 일으킬 수 있다.  
> < 위키백과 >  
> Combinatorial explosion  
> 수학에서 조합 폭박은 문제의 조합이 문제의 입력, 제약 및 경계에 의해 어떻게 영향을 받는지에 따라 문제의 복잡성이 급격히 증가하는 것을 뜻한다.

*전역 상태를 마구잡이로 변경하면 복잡성이 매우 증가할 수 있다는 뜻인 듯 하다.*  
  
그러나 반면, 명령어를 똑똑하게 사용할 경우, 더 효율적인 코드를 작성할 수 있다.  
Combinatorial explosion에 대항하는 방법은 상태를 가능한한 최대한 간단하게 유지하고, 단방향 데이터 흐름에 따라 파생된 데이터를 모델링하는 것이다.  
  
*RX를 사용하면, 상태의 영향을 적게 받도록하여 복잡성을 낮출 수 있다는 뜻인 것 같다.*  
  
### Benefits  
1. Composable, 구성할 수 있다. 여러 요소들을 조립할 수 있다. Rx는 composition의 별명이다.  
2. Reusable, 재사용할 수 있다. 여러 요소들을 조립할 수 있기 때문이다.  
3. Declarative, 선언적이다. 정의 자체는 변하지 않고 데이터만이 변화한다.  
4. Understandable and concise, 이해하기 쉽고 간결하다. 추상화 수준을 높이고, 임시적인/일시적인 상태들을 제거한다.  
5. Stable, 안정적이다. Rx 코드는 철저히 unit test를 거치기 때문이다.  
6. Less stateful, 상태의 영향을 적게 받는다. 단방향 데이터 흐름에 따라 앱을 모델링하기 때문이다.  
7. Without leaks, 누수가 없다. 리소스 관리가 쉽기 때문이다.  
  
  
  
참조: https://github.com/ReactiveX/RxSwift/blob/main/Documentation/Why.md  