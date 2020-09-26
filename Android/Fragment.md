## Lifecycle  
  
  
### 생성  
1. Fragment is Added  
2. onAttach()  
3. onCreate()  
4. onCreateView(): 프레그먼트가 back stack에서 layout 위로 드러나면 호출되는 곳.  
5. onViewCreated()  
6. onStart()  
7. onResume()  

### 종료  
1. onPause()  
2. onStop()  
3. onDestroyView()  
4. onDestroy()  
5. onDetach()  
  
  
  
## Adapter  
  
  
### FragmentPagerAdapter  
프레그먼트 개수가 고정적인 화면에서 사용 권장.  
FragmentManager가 생성된 프레그먼트 인스턴스는 제거하지 않고, 뷰 연결만 제거한다.  
처음 프레그먼트가 생성되면 onCreate - onCreateView가 실행된다.  
화면 이동으로 뷰가 제거되면 onDestroyView만 실행되고, onDestroy - onDetach는 실행되지 않는다.  
  
### FragmentStatePagerAdapter  
프레그먼트 개수가 유동적인 화면에서 사용 권장.  
FragmentManager가 생성된 프레그먼트 인스턴스를 완전히 제거해, 메모리 누수에 대응한다.  
onCreate - onDetach 모두 실행된다.  
  
  
  
## ViewPager  
- 좌우 화면을 미리 생성하고 다른 화면으로 넘어가면 지난 화면을 제거한다.  
Ex. A, B, C 화면이 있을 때, B -> C로 스와이프하면, D가 생성되면서 A가 제거된다.  
