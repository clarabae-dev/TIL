#### 랜덤함수  
- arc4random() -> UInt32  
0 ~ (2^32 - 1) 사이의 난수를 반환  
- arc4random_uniform(UInt32) -> UInt32  
UInt32 타입의 파라미터를 받을 수 있다.  
0 ~ (파라미터로 넣은 UInt32 - 1) 사이의 난수를 반환  
- drand48() -> Double  
0 ~ 1.0 사이의 난수를 반환  

#### _ underscore  
Swift는 함수 argument마다 name을 붙일 것을 요구한다. 함수를 호출할 때도 argument name을 꼭 명시한다.  
name없이 underscore를 argument 앞에 붙일 경우, 함수 호출에서 argument name을 명시하지 않아도 된다.  
단일 argument나 name을 명시할 필요가 없는 경우 활용하면 좋다.  
  
#### @discardableResult  
결과를 사용하지 않고, 값을 리턴하는 함수 또는 메소드가 호출될때 컴파일러 경고를 표시 하지않을 때 사용한다.  
Result of call to '~~' is unused -> 경고 제거.  
