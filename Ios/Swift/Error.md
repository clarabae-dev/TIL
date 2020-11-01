## Error  
  
  
### Modifications to the layout engine must not be performed from a background thread after it has been accessed from the main thread.  
  
#### background  
Main Thread가 아닌 곳에서 UI를 수정하는 경우 발생하였다.  
  
#### solution  
해당하는 곳을 찾아서 DispatchQueue.main.async{} 등으로 감싸준다.  


### TableView Cell Reuse Problem  
  
#### solution  
Cell 내부에 prepareForReuse()를 오버라이드한 후, Cell을 초기화해준다.  
  
  
### Assertion failed: This is a feature to warn you that there is already a delegate (or data source) set somewhere previously.  
  
#### background  
rx tableview 내부에 rx collectionview를 적용하는데, tableview의 cell type별로 collectionview를 바인드할 때 발생하였다.  
첫 데이터 로드는 성공하나 스크롤할 때 해당 오류가 발생한다.  
  
#### solution  
cell type별 코드 내부에서 collectionview를 rx로 바인드하기 전에 delegate와 datasource를 각각 nil처리 해주어야 한다.  
cell type별로 번갈아가면서 뿌려주므로 바인딩을 다시 해주게 된다.  
nil을 호출하지 않으면 직전에 바인딩된 delegate와 datasource 때문에 오류가 발생한다.  
  
  
  
참조: https://khstar.tistory.com/entry/RxSwift에서-UIPickerView-사용-및-데이터-변경하기  