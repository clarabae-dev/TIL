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
  
