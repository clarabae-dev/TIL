## ScrollView in Xcode 11  
Xcode 11버전 부터 ContentLayoutGuide와 FrameLayoutGuide가 추가되었다.  
두 가이드를 사용해 ScrollView를 추가하는 방법은 다음과 같다.  
  
  
### ScrollView 추가  

### ScrollView의 Constraint 설정  
ScrollView를 Safe Area를 기준으로 맞춘다.  

### ContentView의 Constraint 설정  
1. ScollView에 컨텐츠를 위한 최상위 View를 추가한다.  
2. View의 Constraint를 ContentLayoutGuide를 기준으로 맞춘다.  
이전에는 상위 View인 ScrollView를 기준으로 맞추었다.  
3. 스크롤 방향에 따라 FrameLayoutGuide에 Equal Widths 또는 Equal Heights Constraint를 추가한다.  
이전에는 최상위 View를 기준으로 맞추었다.  
- Equal Widths: 가로 길이를 FrameLayoutGuide에 고정시켜 세로 스크롤이 되도록 한다.  
- Equal Heights: 세로 길이를 FrameLayoutGuide에 고정시켜 가로 스크롤이 되도록 한다.  

**parent와 child 간, child끼리의 top, bottom에 상호간의 constraint 설정이 있어야 한다.**  
  
  
  
출처: https://kyungmosung.github.io/2019/11/06/xcode-scrollview/  