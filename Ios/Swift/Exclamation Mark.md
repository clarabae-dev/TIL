## !  
swift는 !를 사용하여 optional을 강제로 unwrap하거나 명시적으로 unwrapped optional을 표현한다.  
  
  
### Mean  
1. 강제로 optional을 unwrap 하다.  
*이 optional이 확실히 값을 가지고 있다는 것을 알고 있으니, 직접 사용하겠다.*  
2. 명시적으로 unwrapped optional을 표현하다.  
  
```swift
var viewModel: ViewModel!
```  
  
*이 변수는 처음에 nil이 될 것이고 이후 반드시 값을 가질 것이니, 내가 계속 unwrap하게 만들지 마라.*  
  
### try? vs try!  
try는 do-catch 문을을 사용해 에러 처리를 한다. do 문 내에서 try한 메소드에 에러가 발생하면 앱이 종료되지 않고 catch 문에서 처리한다.  
또는 보다 간편하게 try?나 try!를 사용할 수도 있다.  
  
#### try?  
에러 발생 시 nil을 반환한다. 에러가 발생하지 않으면 리턴된 타입은 optional이다. 리턴 타입이 없어도 사용할 수 있다.  
  
```swift
if let results = try? viewModel.rooms.value() {
    return results
}
```  
  
  
### try!  
에러가 발생할 경우 crash가 발생한다. 리턴 타입이 non-optional이므로 에러가 발생하지 않는다는 것을 보장하고 해당 함수를 호출한다.  
  
  
  
참조:  
https://www.hackingwithswift.com/example-code/language/what-does-an-exclamation-mark-mean  
https://zetal.tistory.com/entry/swift-try-try-try  