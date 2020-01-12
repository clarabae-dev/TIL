#### Build Configuration  
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
