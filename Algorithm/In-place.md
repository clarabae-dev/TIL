## Inplace algorithm  
추가적인 메모리 공간을 전혀 필요로 하지 않거나, 적게 필요로 하는 알고리즘을 의미한다.  
계산을 보조하기 위한 추가적인 데이터 구조없이, 입력값을 변환한다.  
공간 복잡도는 O(log n)이고 O(n)이 될 때도 있다.  
길이가 n인 배열에 대해 배열을 정렬할 때 추가로 메모리 공간을 할당하지 않아도 정렬이 된다면 Inplace 알고리즘이 된다.  
Inplace algorithm이 되지 않는 알고리즘은 공간 복잡도가 높아진다.  
  
  
### Rotate Array  
Given an array, rotate the array to the right by k steps, where k is non-negative.  
Input: nums = [1,2,3,4,5,6,7], k = 3  
Output: [5,6,7,1,2,3,4]  
  
```swift
func rotate(_ nums: inout [Int], _ k: Int) {
	for i in 0..<k {
        let l = nums.count - 1
        nums.insert(nums[l], at: 0)
        nums.remove(at: l + 1)
    }
}
```  
  