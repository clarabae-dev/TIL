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
  
  
  
출처:  
https://github.com/yagom/swift_basic/tree/master/contents/03_collection_types  
https://programmingwithswift.com/how-to-sort-a-dictionary-by-value-with-swift/  
