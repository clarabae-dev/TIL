1. Set  
- 순서 상관없이, 중복을 허용하지 않는 collection.  
*A set stores distinct values of the same type in a collection with no defined ordering.*  
- 성능이 중요하거나 대량의 데이터 입력이 예상될 때 활용하면 좋다.  
이 때, Set을 성능에 최적화시키는 Hashable 프로토콜을 준수하는 것이 좋다.  
collection의 크기와 상관없이 요소를 조회하는데 동일한 시간이 소요된다.  