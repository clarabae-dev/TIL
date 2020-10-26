#### 문자열에서 필터링 하기  
```swift
let filteredStr = originStr.filter { $0.isNumber } // 숫자 필터링  
```
  
#### 정규표현식으로 필터링 하기  
```swift
let regex = try? NSRegularExpression(pattern: "[0-9]+,[0-9]+")  
// 11,123 과 같은 형식 필터링  
let results = regex?.matches(in: str, options: [], range: NSRange(location: 0, length: str.count))  
```
  
* 정규표현식  
[]: 패턴이 어떤 종류의 값을 갖는지, 값의 범위를 표현  
+: [] 범위에 포함되는 문자들이 하나 이상 존재  

#### 문자열에서 개별 문자 접근하기  
String 문자에 접근하기 위해서는 index를 활용할 수 있다. 이 경우, index는 String.Index 타입이다.  
빈 문자열은 startIndex와 endIndex가 동일하다.  
ex. str.index(str.startIndex, offsetBy: 3)  
또는 String 자체가 배열과 같으므로 Array(str)로 감싸 접근도 가능하다.  
위와 같은 과정으로 추출한 개별 문자의 경우 String 타입이 아닌 char 타입이므로 String으로 반환해야할 경우 String(char)으로 감싸준다.  

#### Value Type  
Swift에서 String type은 참조형태가 아닌 값 형태이다.  
  
#### utf16Offset(in:)  
String.Index를 통해 String element에 접근할 수 있는데, 반환값이 Int가 아닌 Index이다.  
Index 값에 직접 접근하고자 할 때, 다음과 같이 수행할 수 있다.  
1. Swift 5 이전: firstIndex(of: char)?.encodedOffset  
2. Swift 5 이후: firstIndex(of: char)?.utf16Offset(in: s)  