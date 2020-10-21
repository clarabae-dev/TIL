#### Set Horizontal CollectionView End Margin  
Section Insets -> set right value  

#### Set Cell Center in Horizontal CollectionView  
셀의 너비가 화면과 딱 맞지 않은 경우, paging enabled = true를 설정해두면 2번째부터 셀의 위치가 애매해진다.  
paging enabled = false로 설정하고, 아이템 너비와 여백을 포함한 아이템 너비를 계산하여 셀이 위치할 Index 값을 구한다.  
```swift
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
```

#### Error: Launch screens may not set custom classnames  
특정 ViewController와 LaunchScreen.storyboard의 Launch View를 연결할 경우, 발생하는 오류이다.  
Launch View의 File Inspector -> Use as Launch Screen 해제