## MVC  
  
![Alt text](https://camo.githubusercontent.com/d593bbb12f4ff4f83141ffafe495ec7cd395f578/68747470733a2f2f63646e2d696d616765732d312e6d656469756d2e636f6d2f6d61782f323030302f312a45394135664f7253723079566d63374b6c79354336412e706e67)  
  
Model-View-Controller 패턴의 동작 과정은 다음과 같다.  
1. View는 사용자 액션을 Controller에 전달한다.  
2. Controller는 그에 따른 데이터 갱신을 Model에 요청한다.  
3. Model에서 데이터 갱신이 일어나고 Model은 상태 변화를 View에 전달한다.  
4. 그에 따라 View도 갱신된다.  
  
  
### 특징  
1. MVC 패턴은 3요소가 서로 강하게 결합되어 있어 재사용성이 낮다.  
2. Model은 데이터가 갱신되었음을 View에 직접 알린다.  
2. Controller와 View가 1:n 관계이다.  
  
  
  
## MVP  
  
![Alt text](https://camo.githubusercontent.com/a40d6ec616e04dee42b7107a94f77f533a700b11/68747470733a2f2f63646e2d696d616765732d312e6d656469756d2e636f6d2f6d61782f313630302f312a684b5543504548673654447a3667744f6c6e465977512e706e67)  
  
Model-View-Presenter 패턴의 동작 과정은 다음과 같다.  
1. View는 사용자 액션을 Presenter에 요청한다.  
2. Presenter는 Model로부터 데이터를 받는다.  
3. Presenter는 View에 데이터를 전달한다.  
4. 그에 따라 View도 갱신된다.  
  
  
### 특징  
1. Presenter는 Model과 View 사이를 연결한다. Presenter는 Model로부터 갱신된 데이터를 받아와 View를 갱신한다.  
2. Presenter와 View가 1:1 관계로 상호 간 의존도가 높다.  
  
  
  
## MVVM  
  
![Alt text](https://camo.githubusercontent.com/637cafae211bed88b9a6c6019aad3823c2126870/68747470733a2f2f63646e2d696d616765732d312e6d656469756d2e636f6d2f6d61782f3830302f312a384d694e555a52714d315844746a74696678545371412e706e67)  
  
Model-View-ViewModel 패턴의 동작 과정은 다음과 같다.  
1. ViewModel은 View로부터 사용자 액션을 받고 Model로부터 데이터를 받는다.  
2. ViewModel은 받아온 데이터를 가공하여 값을 갱신한다.  
3. View는 이를 observing하다가 값이 갱신되면 이에 맞춰 View를 갱신한다.  


### 특징
1. View는 오직 시각적인 요소만 담는다. 비즈니스 로직이나 어플리케이션 로직에 접근할 수 없다.  
2. ViewModel은 Model과 View 사이를 연결한다.  
3. ViewModel은 View의 각 컴포넌트에 대해 인터페이스를 제공하고, 이 인터페이스와 각 컴포넌트를 연결하는 것을 Binding 이라 한다.  
4. ViewModel과 View가 1:n 관계이다.  
  
  
  
출처:  
https://laptrinhx.com/ios-architecture-mvc-mvp-mvvm-viper-796515689/  
https://magi82.github.io/android-mvc-mvp-mvvm/  