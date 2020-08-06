#### Add ScrollView  
1. ScrollView 내부에 Container View 용도의 UIView 추가  
2. constraint 추가  
- ScrollView의 constraint는 SafeArea를 기준으로 Top, Bottom, Leading, Trailing을  
  0으로 맞춘다.  
- 내부 Container View의 constraint는 ScrollView를 기준으로 Top, Bottom, Leading,  
  Trailing을 0으로 맞춘다.  
- 내부 Container View를 가장 바깥 View와 Equal Width, Equal Height를 맞춘다.  
- 내부 Container View의 Equal Height constraint의 priority를 250으로 맞춘다.  
- parent와 child 간, child끼리의 top, bottom 간격이 서로 관련이 있어야 한다.  

#### Set Horizontal CollectionView End Margin  
Section Insets -> set right value  

#### Set Cell Center in Horizontal CollectionView  
셀의 너비가 화면과 딱 맞지 않은 경우, paging enabled = true를 설정해두면 2번째부터 셀의 위치가 애매해진다.  
paging enabled = false로 설정하고, 아이템 너비와 여백을 포함한 아이템 너비를 계산하여 셀이 위치할 Index 값을 구한다.  
for i in 0..< self.characterCollectionView.numberOfItems(inSection: 0) {  
  let layout = self.characterCollectionView.collectionViewLayout as! UICollectionViewFlowLayout  
  let itemWithSpaceWidth = layout.itemSize.width + layout.minimumLineSpacing  
  let itemWidth = layout.itemSize.width  

  if self.characterCollectionView.contentOffset.x <= CGFloat(i) * itemWithSpaceWidth + itemWidth / 2 {  
    let indexPath = IndexPath(item: i, section: 0)  
    self.characterCollectionView.scrollToItem(at: indexPath, at: .centeredHorizontally, animated: true)  
    break  
  }  
}  

#### Error: Launch screens may not set custom classnames  
특정 ViewController와 LaunchScreen.storyboard의 Launch View를 연결할 경우, 발생하는 오류이다.  
Launch View의 File Inspector -> Use as Launch Screen 해제