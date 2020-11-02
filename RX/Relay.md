## Relay  
RxCocoa 클래스로 RxCocoa 4에서 구현되었다.  
  
  
  
### PublishRelay  
PublishSubject의 Wrapper 클래스이다. PublishSubject처럼 subscribe 이후 배출되는 항목들만 알 수 있다.  
  
### BehaviorRelay  
BehaviorSubject의 Wrapper 클래스이다. .value를 통해서 현재 값을 가져온다.  
subject의 value()와 달리 에러를 발생시키지 않고 발생하더라도 dispose 시킨다.  

```swift
/// Current value of behavior subject
public var value: Element {
    // this try! is ok because subject can't error out or be disposed
    return try! self.subject.value()
}
```  
  
  
### Subject vs Relay  
relay는 .completed, .error를 발생시키지 않고 dispose되기 전까지 계속 동작하므로 UI event에서 사용하기 적절하다.  
subject는 .completed, .error를 발생시키고, 해당 이벤트들이 발생하면 subscribe가 종료된다.  
  
  
  
참조: https://jinshine.github.io/2019/01/05/RxSwift/3.Subject%EB%9E%80/  