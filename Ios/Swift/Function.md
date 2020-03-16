#### 랜덤함수  
- arc4random() -> UInt32  
0 ~ (2^32 - 1) 사이의 난수를 반환  
- arc4random_uniform(UInt32) -> UInt32  
UInt32 타입의 파라미터를 받을 수 있다.  
0 ~ (파라미터로 넣은 UInt32 - 1) 사이의 난수를 반환  
- drand48() -> Double  
0 ~ 1.0 사이의 난수를 반환  
