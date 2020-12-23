## App Process  
1. main 함수 실행  
2. main 함수는 UIApplicationMain 함수 호출  
3. UIApplicationMain 함수는 UIApplication 객체 생성  
4. Info.plist, nib 파일 등을 읽어들여 그외 필요한 데이터 로드  
5. App Delegate 객체를 만들어 UIApplication 객체와 연결하고 Run Loop를 만드는 등 실행에 필요한 준비를 한다.  
6. 실행 완료 전 UIApplication 객체가 App Delegate에 application:didFinishLaunchingWithOptions: 메세지 발송  
  
  
### Main Function  
Swift는 Objective-C와 달리 main 파일이 존재하지 않지만, 진입점은 필요하기에 다음과 같은 어노테이션으로 대체한다.  

```swift
@UIApplicationMain
```  
  
UIKit 프레임워크가 main 함수를 관리하기 때문에 개발자들이 직접 함수를 작성할 필요가 없다.  
UIKit이 main 함수를 다룰 때 UIApplication 객체가 생성되는데, 이 객체를 활용해 앱 실행에 관여할 수 있다.  
  
### UIApplicationMain Function  
UIApplicationMain 함수는 앱의 라이프 사이클을 시작하는 함수이다.  
UIApplication 인스턴스를 만들고, 앱으로서 기능하기 위한 기반을 만드는 과정을 앱 로딩 프로세스 라 부른다.  
  
### Main Run Loop  
Main Run Loop은 사용자 관련 이벤트들을 받은 순서대로 처리하고, 메인 스레드에서 동작한다.  
UIApplication 객체는 앱이 실행될 때 Main Run Loop를 실행하고, Run Loop대로 이벤트를 처리한다.  
1. 사용자 액션 발생  
2. 시스템은 액션에 해당하는 이벤트를 생성  
3. UIKit에서 생성한 port를 통해 이벤트를 앱에 전달  
4. queue에 보관된 이벤트는 하나씩 Main Run Loop에 전달되어 처리  
  
## App State  
  
![Alt text](https://docs-assets.developer.apple.com/published/74077a8107/ec07a686-2315-4700-9415-6485cc3bcfff.png)  
  
1. Not Running: 실행되지 않았거나, 시스템에 의해 종료된 상태  
2. Inactive: 실행 중이지만 이벤트를 받고 있지 않은 상태이다.  
			 Ex. 앱 실행 중 미리알림 등이 화면에 덮여 앱이 실질적으로 이벤트를 받지 못하는 상태  
3. Active: 앱이 실질적으로 활동하는 상태  
4. Background: 음악 실행과 같이 백그라운드 상태에서 실질적인 동작을 하는 상태이다.  
5. Suspended: 백그라운드 상태에서 동작을 멈춘 상태이다.  
			  빠른 재실행을 위해 메모리에 적재되어 있으며, 메모리가 부족할 때 시스템이 강제 종료한다.  
  
대부분의 상태 전환은 AppDelegate의 메소드 호출을 거친다.  

### ViewWillAppear가 항상 호출되지 않는 이유  
ViewWillAppear 호출되는 경우:  
ViewController에 뷰가 view hierarchy에 추가될 것임을 알려줄 때 호출된다.  
이미 view hierarchy에 추가된 경우, ViewWillAppear가 호출되지 않는다.  

### How to detect app returned to foreground  
```swift
let notificationCenter = NotificationCenter.default
notificationCenter.addObserver(self, selector: #selector(appMoveToForeground), name: Notification.Name.UIApplicationWillEnterForeground, object: nil)
```  
  
