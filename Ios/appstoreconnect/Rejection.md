1. Guideline 2.5.1 - Performance - Software Requirements  
Your app uses the HealthKit or CareKit APIs  
but does not indicate integration with the Health app in your app description  
and clearly identify the HealthKit and CareKit functionality in your app's user interface.  
  
> HealthKit과 같은 사용자 리소스를 사용하는 api를 사용하는 경우, 메타 데이터(앱 설명)에 반드시 사용 목적에 대해 기록해야 한다.  
> HealthKit을 걷어낼 경우, Capability와 Build Phases -> Link Binary with Libraries 모두에서 HealthKit을 제거해야 한다.  
  
2. Guideline 2.3.12 - Performance - Accurate Metadata  
- We noticed you have included nondescript, temporary, or incomplete information in your app’s "What’s New" text.  
Aside from simple bug fixes, security updates, and performance improvements,  
apps must clearly describe new features and product changes in their "What’s New" text.  
  
> 새로 출시할 버전에서 업그레이드한 사항에 대해 자세히 적어야 한다.  
  
We noticed that your app or its metadata includes irrelevant third-party platform information.  
Specifically, your app includes non-iOS status bar images in the app.  
  
> 첨부한 이미지 중 기기의 status bar가 AOS 것이었다.  
  
3. Your app uses the "prefs:root=" non-public URL scheme, which is a private entity.  

> 앱 내에서 위치 권한 등을 이유로 설정창 등 외부로 이동할 때, 그 경로를 직접 지정해주면 안된다.  
> UIApplicationOpenSettingsURLString을 사용한다.  
  
```Objective-C
NSURL *url = [NSURL URLWithString:UIApplicationOpenSettingsURLString];
if (url != nil) {
  [[UIApplication sharedApplication] openURL:url options:[NSDictionary new] completionHandler:nil];
}
```  
  
4. Guideline 2.1 - Information Needed  
4.1 A demo video demonstrating your app's process for registering and verifying new users.  
Please provide details for accessing the video in the "App Review Information" section of App Store Connect.  
Only include footage in the video of your app running on a physical iOS device, and not on a simulator.  
You can use a screen recorder to capture footage of your app in use.  
  
> 본인 인증 절차가 포함되어 있기 때문에 회원가입 절차를 전부 거칠 수 없어 요청이 들어온 것 같다.  
  
- Why does your app require user verification for registration?  

> 회원가입에서 본인 인증이 필요한 이유.  
  
- What personal information does the app collect in the user-verification process?  

> 본인 인증 절차에서 수집하는 개인 정보 항목.  
  
- What personal information is required for registration?  
Please list each type of personal information separately with reasons for why it is required.  

> 회원가입 과정에서 수집하는 개인 정보 항목과 그 이유.  
  
  
4.2 App Tracking Transparency Permission  
분명 권한 허가를 요청하는데 본인이 안된다고 한다. 그래서 스크린샷과 영상을 첨부해서 이의신청을 했고, 바이너리도 새로 제출하였다.
  
  
5. Guideline 1.4.1 - Safety - Physical Harm  
All apps with medical and health information should include links to sources for the information.  
This helps ensure that App Store users are being provided accurate information.  
  
Please include citations in the app of the sources of the recommendations or information and links to those sources.  
The links to the sources should be easy for the user to find.  
  
> 건강 또는 의학 관련 내용은 사용자에게 정확한 정보 전달을 위해 그 출처를 명시해야 한다.  