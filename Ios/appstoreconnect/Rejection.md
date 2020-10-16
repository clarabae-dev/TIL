1. Guideline 2.5.1 - Performance - Software Requirements  
Your app uses the HealthKit or CareKit APIs  
but does not indicate integration with the Health app in your app description  
and clearly identify the HealthKit and CareKit functionality in your app's user interface.  
  
- HealthKit과 같은 사용자 리소스를 사용하는 api를 사용하는 경우, 메타 데이터(앱 설명)에 반드시 사용 목적에 대해 기록해야 한다.  
- HealthKit을 걷어낼 경우, Capability와 Build Phases -> Link Binary with Libraries 모두에서 HealthKit을 제거해야 한다.  
  
2. Guideline 2.3.12 - Performance - Accurate Metadata  
We noticed you have included nondescript, temporary, or incomplete information in your app’s "What’s New" text.  
Aside from simple bug fixes, security updates, and performance improvements,  
apps must clearly describe new features and product changes in their "What’s New" text.  
  
- 새로 출시할 버전에서 업그레이드한 사항에 대해 자세히 적어야 한다.  

3. Your app uses the "prefs:root=" non-public URL scheme, which is a private entity.  

- 앱 내에서 위치 권한 등을 이유로 설정창 등 외부로 이동할 때, 그 경로를 직접 지정해주면 안된다.  
- UIApplicationOpenSettingsURLString을 사용한다.  

```Objective-C
NSURL *url = [NSURL URLWithString:UIApplicationOpenSettingsURLString];
if (url != nil) {
  [[UIApplication sharedApplication] openURL:url options:[NSDictionary new] completionHandler:nil];
}
```  
  