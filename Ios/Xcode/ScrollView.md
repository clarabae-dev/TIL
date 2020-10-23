## ScrollView in Xcode 11  
Xcode 11버전 부터 ContentLayoutGuide와 FrameLayoutGuide가 추가되었다.  
두 가이드를 사용해 ScrollView를 추가하는 방법은 다음과 같다.  
  
  
### FrameLayoutGuide and ContentLayoutGuide  
1. FrameLayoutGuide  
기기 화면에서 스크롤뷰가 보여질 영역.  
2. ContentLayoutGuide  
스크롤뷰에 들어갈 컨텐츠의 전체 영역.  

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
  
### 기기별 적용  
작은 사이즈의 기기에서는 스크롤이 가능하도록 && 큰 사이즈의 기기에서는 화면에 딱 맞도록.  
1. 위의 방법대로 스크롤뷰와 하위 뷰들을 추가한다.  
2. ContentView를 FrameLayoutGuide에 Align Bottom을 적용한다. 단, Less Than or Equal로 적용한다.  
이유는 Contents영역은 Frame 영역, 즉 화면에 보여질 영역보다 클 수 있기 때문이다.  
  
모든 사이즈의 기기에서 스크롤 없이 화면에 맞도록 하려면.
1. 위의 방법대로 스크롤뷰와 하위 뷰들을 추가한다.  
2. ContentView를 FrameLayoutGuide에 Align Bottom을 Equal로 적용한다.  
  
  
  
출처: https://kyungmosung.github.io/2019/11/06/xcode-scrollview/  