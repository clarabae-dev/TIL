### AutoLayout  
다양한 사이즈와 화면 비율에 구애받지 않고 시각적으로 동일한 화면을 구현하기 위한 방법이다.  
뷰의 constraint를 기반으로 모든 뷰의 크기와 위치를 동적으로 계산한다.  

### Frame and Bounds  
1. Frame  
뷰의 위치와 크기를 상위 뷰의 좌표(0,0)를 기준으로 나타내준다.  
2. Bounds  
뷰의 위치와 크기를 뷰 자신의 좌표(0,0)를 기준으로 나타낸다.  
  
### UIStackView  
여러 뷰를 가로 또는 세로 방향으로 배치할 때, 복잡한 설정 없이 구현할 수 있다.  
arrangedSubView로 하위 뷰들을 관리하며, 하위 뷰들 간 가로/세로 방향, 정렬, 뷰 간 간격을 적용할 수 있다.  
  
### Priority  
1. Autolayout Constraint Priority  
Constraint 간 우선순위이다. Constraint 간 충돌이 발생 할 때, 우선순위를 둠으로써 해결할 수 있다.  
2. Content Hugging Priority  
UI Framework의 일부 뷰에는 Contrisic content size, 컨텐츠 고유 사이즈가 있다.  
이 뷰들은 다른 뷰들과의 constraint 때문에 컨텐츠 고유 사이즈보다 더 늘어나거나 줄어들 수 있다.  
- Content Hugging: 더 늘어나는 것에 대해 저항하는 constraint.  
- Content Compression Resistance: 더 줄어드는 것에 대해 저항하는 constraint.  
  
컨텐츠 고유 사이즈 constraint는 우선순위가 있는데 Autolayout Constraint Prioriry 보다 우선순위가 낮다.  
  
### UICollectionViewLayout  
1. prepare  
레이아웃과 관련된 연산이 발생할 때마다 가장 먼저 호출된다. 여기서 셀의 위치/크기 등을 계산하는 사전처리를 할 수 있다.  
  
### UITableView  
1. Dynamic Height  
- TableViewDelegate를 직접 extension하여 활용할 경우  

```swift
func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) {
	return UITableView.automaticDimension
}
```  
  
테이블 뷰 셀은 셀 내부 서브 뷰들 간의 constraint로 셀의 크기가 결정되도록 구현한다.  