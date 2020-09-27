## Basics  
**Observer 패턴의 Observable과 Swift의 Sequence는 둘 다 비동기적으로 element를 받을 수 있으며, 이 점이 RxSwift의 핵심이다.**  
  
Sequence는 Array, List, String과 같이 반복문을 사용하고 각 element에 접근할 수 있는 데이터 타입이다.  

1. Observable(ObservableType)은 Sequence와 같다.  
2. ObservableType.subscribe 메소드는 Sequence.makeIterator 메소드와 같다.  
3. Observer(callback)는 sequence element를 받기 위해 next()를 호출하는 대신  
ObservableType.subscribe 메소드에 전달되어야 한다.  
  
Sequence를 정규 표현으로 나타내면, 다음과 같을 것이다:  

**next* (error | completed)?**  
  
그리고 이 정규 표현식은 다음을 뜻한다.  

1. Sequence는 0 개 이상의 element를 가질 수 있다.  
2. error 또는 completed 이벤트를 받으면, sequence는 더이상 어떤 이벤트도 만들 수 없다.  
  
Rx의 Sequence는 푸시 인터페이스(콜백)로 설명된다.  

```swift
enum Event<Element>  {
    case next(Element)      // next element of a sequence
    case error(Swift.Error) // sequence failed with error
    case completed          // sequence terminated successfully
}

class Observable<Element> {
    func subscribe(_ observer: Observer<Element>) -> Disposable
}

protocol ObserverType {
    func on(_ event: Event<Element>)
}
```
  
**sequence가 completed 또는 error 이벤트를 전송하면 sequence element를 계산하는 모든 내부 리소스가 해제된다.  
sequence element를 만드는 것을 취소하고 리소스를 즉각 해제하기 위해, 반환되는 subscription에서 dispose를 호출한다.**  
  
sequence가 유한한 시간에 종료되는 경우, dipose를 호출하지 않거나 disposed(by: disposeBag)을 사용하지 않더라도,  
그로인해 영구적인 리소스 누수가 생기지 않는다.  
그러나 이 리소스는 element 생산을 완료하거나 오류를 반환하여 sequence가 완료될 때까지 사용될 것이다.  
  
일련의 버튼 탭처럼 sequence가 자체적으로 종료되지 않으면, 수동으로 dispose를 호출하고,  
disposeBag 내부에서 takeUntil과 함께 자동으로 호출되거나 다른 방식을 사용하지 않는 한, 리소스는 영구적으로 할당될 것이다.  
  
**disposeBag이나 takeUntil을 사용하는 것은 리소스가 깨끗이 정리되도록 하는 강력한 방법이다.  
RxSwift에서는 sequence가 유한한 시간에 종료되더라도 disposeBag이나 takeUntil을 사용할 것을 권고한다.**  
  
  
  
## Disposing  
