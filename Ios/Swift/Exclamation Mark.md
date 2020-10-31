## !  
swiftsms 느낌표를 사용하여 optional을 강제로 unwrap하거나 명시적으로 unwrapped optional을 표현한다.  
  
  
### Mean  
1. 강제로 optional을 unwrap 한다.  
*이 optional이 확실히 값을 가지고 있다는 것을 알고 있으니, 직접 사용하겠다.*  
2. 명시적으로 unwrapped optional을 표현하다.  
  
```swift
var viewModel: ViewModel!
```  
  
*이 변수는 처음에 nil이 될 것이고 이후 반드시 값을 가질 것이니, 내가 계속 unwrap하게 만들지 마라.*  
  
  
  
참조: https://www.hackingwithswift.com/example-code/language/what-does-an-exclamation-mark-mean  