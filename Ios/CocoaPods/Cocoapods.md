## Cocoapods  
Swift와 Objective-C의 dependency manager로 Android gradle과 같은 역할을 수행한다.  
  
  
### how to install with xcode  
1. sudo gem install cocoapods  
2. move to project folder  
3. pod setup  
4. pod init (to create podfile)  
5. open -e podfile || double click podfile  
6. complete the podfile as below.  

```
platform :ios, '8.0'  
# Comment the next line if you're not using Swift and don't want to use dynamic frameworks use_frameworks!  
  
target 'MyApp' do  
  pod 'AFNetworking', '~> 2.6'  
  pod 'ORStackView', '~> 3.0'  
  pod 'SwiftyJSON', '~> 2.3'  
end  
```

7. pod install (to install the dependencies)  
After install dependencies, add Pods folder in project.  
8. Open project with .xcworkspace file not .xcodeproj file.  
  
### Use pod install vs pod update  
1. Use pod install to install new pods in your project.  
Even if you already have a Podfile and ran pod install before;  
So even if you are just adding/removing pods to a project already using CocoaPods.  
2. Use pod update [PODNAME] only when you want to update pods to a newer version.  
  
### Clear CocoaPods Cache  
pod deintegrate && pod cache clean --all  
  
  
  
출처: https://www.raywenderlich.com/626-cocoapods-tutorial-for-swift-getting-started  