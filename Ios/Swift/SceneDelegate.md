## Overview  
어플리케이션 상에서 멀티 윈도우를 지원하기 위해 사용하며, iOS 13 이상, iPad에서 지원한다.  
사용자는 어플리케이션 UI의 여러 인스턴스를 동시에 만들고 관리할 수 있다. 즉, 하나의 앱을 여러 화면에 동시에 띄울 수 있다.  
app switcher를 사용해 UI 인스턴스 간에 전환할 수 있다.  
UI의 각 인스턴스는 서로 다른 컨텐츠를 표시하거나, 동일한 컨텐츠를 서로 다른 방식으로 표시한다.  
이 UI 인스턴스들에 대해 Scene 객체를 사용하여 UI를 화면에 띄우는 윈도우, 뷰 그리고 뷰 컨트롤러를 관리한다.  
  
  
1. iOS 12 & Earlier  
한 쌍의 프로세스와 UI로 되어있다. AppDelegate에서 프로세스 Lifecycle과 UI Lifecycle을 모두 관리한다.  
  
2. After iOS 13  
하나의 프로세스를 공유하는 여러 개의 UI 인스턴스들(scene session)로 되어있다.  

AppDelegate는 프로세스 Lifecycle과 Session Lifecycle을 관리한다.  
새로운 Scene Session이 생성되거나, 기존 Scene Session이 삭제될 때 시스템이 AppDelegate에게 알림을 준다.  

UI Lifecycle은 SceneDelegate가 관리한다.  