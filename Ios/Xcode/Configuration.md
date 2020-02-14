#### Build Configuration  
서버 환경에 따라 Build Config 설정하기  
- xcconfig files  
텍스트 형식으로 작성된 build configuration 파일이다.  
프로젝트나 타겟의 특정 build configuration을 위한 build setting을 정의할 수 있다.   

- Default Configuration Settings  
Product -> Scheme -> Edit Scheme...   
Run(Debug), Archive(Release)  

- How to add configuration(Development, Staging, Production)  
Project -> Info -> Configurations  
Click + -> Add 'Duplicate "Debug" Configuration' -> Rename it Debug(Development)  
Repeat this for Staging  

- Default Schemes  
기본적으로 앱의 이름을 딴 scheme이 있으며, 하나의 scheme은 configurations를 정의할 수 있다.  

- How to add schemes(Development, Staging, Production)  
Product -> Scheme -> Manage Schemes...  
Click the current scheme  
At the bottom, click the cog, select Duplicate  
Rename it AppName(Development)  
Make sure all are marked as Shared  
> Shared에 체크하지 않으면 로컬 환경에서만 적용이 된다.  

Repeat this for Staging  
> 여기서 빌드하게 되면 두개의 타겟이 하나의 앱으로 빌드된다. Bundle Identifier가 똑같기 때문  

Project -> Build Settings  
Click + -> Add User-Defined Settings -> Give a name -> Set Bundle Identifier  
info.plist -> Bundle Identifier  
-> Change $(PRODUCT_BUNDLE_IDENTIFIER) to $(Your Identifier Title Name)  

- Access the configuration in code  
let flavorConfig = Bundle.main.object(forInfoDictionaryKey: "FlavorConfiguration")!

#### Environment  
- Development  
개발 전용 로컬 환경으로, 실제 유저의 사용에 전혀 영향을 미치지 않는다.  
- Staging  
최대한 실제 서비스 환경과 유사하게 만든 환경이다.  
실서비스(Production) 환경에 영향을 주지 않으면서 많은 서비스(Service) 영역과 통신할 수 있다.  
DB migration, major update 등을 테스트할 때 활용한다.  
클라이언트에 데모 서비스를 제공할 때, Staging 환경을 기반으로 제공할 수 있다.  
실서비스에 배포하기 이전에 최종 확인을 할 수 있는 환경이다.  
- Production  
실제 유저에게 제공되는 서비스 환경이다.  

#### HTTP  
> App Transport Security has blocked a cleartext HTTP (http://) resource load  
since it is insecure...  

앱 자체의 보안을 위해 App Transport Security 정책을 통해 HTTPS 통신을 하도록 유도한다.  
HTTP 통신을 하기 위해 info.plist에서 ATS 설정을 추가해야 한다.  
<dict>  
  <key>NSAppTransportSecurity</key>  
  <dict>  
    <key>NSAllowsArbitraryLoads</key>  
    <true/>  
  </dict>  
</dict>  

- App Transport Security, ATS  
ios 9 이후부터 적용된 개인정보 보호 기능으로 XCode7 부터 앱 생성시 기본적으로 적용되는 보안 정책.  
