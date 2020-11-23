## Custom Tab Bar  
  
### UICollectionViewDelegateFlowLayout  
탭의 개수가 적고, 화면 사이즈에 딱 맞는 탭 뷰를 구현하려면, Cell의 크기를 조정해야 한다.  
  
```swift
extension BaseTeacherProfileViewController: UICollectionViewDelegateFlowLayout {
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
        return CGSize(width: view.frame.width / 3, height: collectionView.bounds.height) // tab 개수 3개일 때
    }
}
```  
  
  
  
  
## UICollectionViewFlowLayout  
collectionview cell을 원하는 형태로 정렬할 수 있도록 해주는 프로토콜이다.  
1. vertical: 좌 > 우 로 셀을 하나씩 채우다가 공간이 모자라면 아래줄로 넘어가 셀을 채운다.  
2. horizontal: 상 > 하 로 셀을 하나씩 채우다가 공간이 모자라면 오른쪽줄로 넘어가 셀을 채운다.  
  
기본적으로 적용되어 있으나, 정렬 방식을 커스텀하고자 한다면 UICollectionViewFlowLayout을 준수하는 객체를 작성한다.  
레이아웃을 조정할 수 있는 다양한 메소드들을 재정의할 수 있다.  
  
  
  
참조: https://k-elon.tistory.com/26  