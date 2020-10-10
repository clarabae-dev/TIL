### Show(e.g. Push)  
1. 새 ViewController는 NavigationController에 추가되어 관리할 수 있다.  
2. 단순 present로는 NavigationController에 추가되지 않는다.  
3. pushViewController, performSegue로 실행되어야 stack에 추가되어 관리할 수 있다.  
  
### Show Detail(e.g. Replace)  
### Present Modally  

### Present as Pop over  
1. NavigationController에 stack으로 추가되지 않는다.  
2. 뒤로가기 버튼과 같은 방식없이 아이템 클릭 후 바로 종료시킬 수 있다.  