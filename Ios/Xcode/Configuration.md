#### Build Configuration  
- xcconfig files  
A build configuration file is a plain text file that  
defines and overrides the build settings for a particular build configuration  
of a project or target.  

- Default Settings  
Product -> Scheme -> Edit Scheme...   
Run(Debug), Archive(Release)  

- How to add configuration  
Project -> Info -> Configurations  
Click + -> Add 'Duplicate "Debug" Configuration' -> Rename it Development  
Product -> Scheme -> Manage Schemes...  
Click + -> Name new target  
> 여기서 빌드하게 되면 두개의 타겟이 하나의 앱으로 빌드된다. Bundle Identifier가 똑같기 때문  

Project -> Build Settings  
Click + -> Add User-Defined Settings -> Give a name -> Set Bundle Identifier  
info.plist -> Bundle Identifier  
-> Change $(PRODUCT_BUNDLE_IDENTIFIER) to $(Your Identifier Title Name)  

- Access the configuration in code  
let flavorConfig = Bundle.main.object(forInfoDictionaryKey: "FlavorConfiguration")!

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
