#### 문자열에서 필터링 하기  
let filteredStr = originStr.filter { $0.isNumber } // 숫자 필터링  

#### 정규표현식으로 필터링 하기  
let regex = try? NSRegularExpression(pattern: "[0-9]+,[0-9]+")  
// 11,123 과 같은 형식 필터링  
let results = regex?.matches(in: str, options: [], range: NSRange(location: 0, length: str.count))  
* 정규표현식  
[]: 패턴이 어떤 종류의 값을 갖는지, 값의 범위를 표현  
+: [] 범위에 포함되는 문자들이 하나 이상 존재  
