1. How to get subarray from array using index  
let array = [1, 5, 2, 6, 3, 7, 4]  
var subarray = array[a...b] # a와 b는 각각 배열의 index를 가리킨다.  
var subarray = array[1...3] # both-side range  
// Results: subarray = [5, 2, 6]  
var subarray = array[3...] # one-side range  
// Results: subarray = [6, 3, 7, 4]  
var subarray = array[...2] # one-side range  
// Results: subarray = [1, 5, 2]  
  
2. Sorting  
- sorted()  
  기존 배열로부터 순차 정렬된 새 배열 만들기  
  let sortedArray = array.sorted()  
  
3. Finding an Array's Max or Min  
- max(), min()  
  결과는 optional이다. optional 결과 처리를 해주어야 한다.  
  let maximum = array.max() ?? 0  
  복잡도는 배열의 길이 n만큼인 O(n)이다.  