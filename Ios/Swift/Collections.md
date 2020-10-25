### Set  
- 순서 상관없이, 중복을 허용하지 않는 collection type.  
- insert: 동일한 값이 있으면, 값이 set에 들어가지 않는다. Set에 추가를 시도한 값이 반환되며, 만약 값이 들어가면 nil이 반환된다.  
- contains: 값 포함 여부 확인.  
- update: 동일한 값이 있어도 값이 Set에 들어간다. 대신 기존에 있던 값이 반환되며, 동일한 값이 없었다면, nil을 반환한다.  
- remove, removeFirst(): 값을 삭제한다. 값이 삭제된다면 삭제된 값을 반환하며, 값이 없으면 nil을 반환한다.  
- union: Set은 집합 연산에 많이 활용된다.  

```swift
let setA: Set<Int> = [1, 2, 3, 4, 5]
let setB: Set<Int> = [3, 4, 5, 6, 7]

let union: Set<Int> = setA.union(setB) // 합집합
let sortedUnion: [Int] = union.sorted() // 합집합 오름차순 정렬
let intersection: Set<Int> = setA.intersection(setB) // 교집합
let subtracting: Set<Int> = setA.subtracting(setB) // 차집합
```  
  
- Hashable한 값만 들어갈 수 있기 때문에 중복을 허용하지 않는다. 유니크한 값인지 따질 수 있는 타입이어야 한다.  
  
### Array  
- 순서가 있는 List 형태의 collection type.  
- let을 사용해 Array를 선언하면 immutable array가 된다. 아이템을 추가 또는 삭제할 수 없다.  
  
```swift
var integers: Array<Int> = Array<Int>()
var integers: Array<Int> = [Int]()
var integers: Array<Int> = []
var integers: [Int] = Array<Int>()
var integers: [Int] = [Int]()
var integers: [Int] = []
var integers = [Int]()
```  
  
- append: Array에 아이템 추가.  
- contains(i): Array에 i 아이템 포함 여부 확인. Bool 반환.  
- remove(at: index), removeLast(), removeAll: 아이템 삭제.  
- count: 아이템 수 확인.  
  
### Dictionary  
- key, value 쌍으로 이루어진 collection type.  
  
```swift
var anyDictionary: Dictionary<String, Any> = [String: Any]()
var anyDictionary: Dictionary <String, Any> = Dictionary<String, Any>()
var anyDictionary: Dictionary <String, Any> = [:]
var anyDictionary: [String: Any] = Dictionary<String, Any>()
var anyDictionary: [String: Any] = [String: Any]()
var anyDictionary: [String: Any] = [:]
var anyDictionary = [String: Any]()
```  
  
- 키에 값을 할당하여 아이템을 추가 또는 변경할 수 있다.  
- 키 값 제거: removeValue(forKey: "someKey"), anyDictionary["someKey"] = nil  
- let으로 Dictionary를 선언하면 immutable dictionary가 된다. 값을 변경할 수 없다.  
- key가 Hashable 해야한다. 유니크한 값인지 따질 수 있는 타입이어야 한다.  
  
### Sort  
1. sort(): collection을 오름 및 내림차순으로 정렬한다.  
  
```swift
array.sort() // 기본 오름차순 정렬
array.sort(by: <) // 오름차순 정렬
array.sort(by: >) // 내림차순 정렬
```  
  
2. sorted(): 오름 및 내림차순으로 정렬한 collection을 반환한다.  
  
```swift
var sortedArray = array.sorted()
```  
  
3. dictionary 타입의 경우, 정렬 방법은 다음과 같다.  
- key만 정렬: dictionary.keys.sorted()  
- value만 정렬: dictionary.values.sorted()  
- key와 value를 한번에 정렬할 수는 없다. 기본적으로 dictionary.sorted()를 하면 key를 기준으로 정렬된다.  
- value를 기준으로 dictionary 정렬:  
```swift
let sortedOne = dictionary.sorted { (first, second) -> Bool in
    return first.value > second.value
}
// closrue를 활용해 key 또는 value를 기준으로 정렬할 수 있다.

let sortedOne = dictionary.sorted {
	return $0.value > $1.value
}
// closure 매개변수를 명명하는 대신 $0, $1 사용하기

let sortedOne = dictionary.sorted {
	return $0.1 > $1.1
}
// dictionary 아이템 element 명을 사용하는 대신 position 값으로 대체할 수 있다.
```  
  
  
### Hashable  
정수 Hash 값을 제공하는 프로토콜로, Set 또는 Dictionary의 Key로 Hashable을 준수하는 모든 타입을 사용할 수 있다.  
Swift의 기본 타입들과 Enum은 기본적으로 hashable한 타입들로 Dictionary Key로 사용할 수 있다.  

타입의 hashValue 프로퍼티가 제공하는 hash 값은 해당 타입의 임의의 두 인스턴스에 대해 동일한 정수값이다.  
즉, 동일한 타입의 인스턴스 A, B가 있을 때, A == B 이면 A.hashVluae == B.hashValue 이다.  
그러나 반대로 hash 값이 같다하여 두 인스턴스가 동일할 필요는 없다.  
  
**Hash 값은 프로그램 실행에 따라 동일하지 않을 수 있으므로, 다음 실행에서 이전 실행의 Hash 값을 사용해서는 안된다.**  
  
### swapAt  
Swift 4 이후로, Array의 값을 서로 바꿔야 할 때 swap 대신 swapAt을 사용한다.  
swap이 Law of Exclusivity를 위반하기 때문이다.  
  
> Law of Exclusivity: 변수 접근은 독점적으로 이루어져야 한다.  
  
즉, 배열이라는 변수에 대해 두 element의 접근이 겹쳐서 swap을 사용할 수 없다. 대신 swapAt(index, index)을 사용한다.  
swapAt은 배열 범위를 벗어나면 Fatal error가 발생하며 복잡도는 O(1)이다.  
또한, 동일한 index에 대해 swapAt을 호출할 경우에는 아무런 영향이 없다.  
  
### stride  
감소하는 반복문을 만들 때 주로 활용하는 stride는 다음 두 가지 경우가 있다.  
1. stride(from: to: by): from 부터 to 사이의 값들을 by 간격으로 리턴한다. 다만 to에 명시한 값은 포함하지 않는다.  
2. stride(from: through: by:): from 부터 through 사이의 값들을 by 간격으로 리턴한다. through에 명시한 값도 포함한다.  
  
```swift
for i in stride(from: 5, to: 1, by: -1) {
	print("\(i)") // 5, 4, 3, 2
}

for i in stride(from: 5, through: 1, by -1) {
	print("\(i)") // 5, 4, 3, 2, 1
}
```  
  
### reverse() vs reversed()  
1. reverse()  
  
```swift
mutating func reverse()
```  

공식 문서에 따르면 collection을 역순으로 바꿔주며. 그 공간 내에서 수행하기 때문에 새로운 공간을 할당할 필요가 없다.  
  
```swift
var characters: [Character] = ["C", "a", "f", "é"]
characters.reverse()
print(characters) // "["é", "f", "a", "C"]
```  
  
복잡도는 O(n)이며, n은 collection의 크기이다.  

2. reversed()  
  
```swift
func reversed() -> ReversedCollection<Array<Element>>
```  
  
공식 문서에 따르면 collection element를 역순으로 나타내는 뷰를 반환한다.  
역순으로 바뀐 collection을 반환하는 것이 아니며, 새로운 공간을 할당하지 않는다.  
ReversedCollection은 기존 collection을 감싸 각 element에 역순으로 접근할 수 있도록 해준다.  
  
```swift
let reversedWord = String(word.reversed())
print(reversedWord) // "sdrawkcaB"
```  

  
  
  
출처:  
https://github.com/yagom/swift_basic/tree/master/contents/03_collection_types  
https://programmingwithswift.com/how-to-sort-a-dictionary-by-value-with-swift/  
https://zeddios.tistory.com/354  
https://zeddios.tistory.com/73  
https://developer.apple.com/documentation/swift/array/2943836-reverse  
https://developer.apple.com/documentation/swift/array/1690025-reversed  