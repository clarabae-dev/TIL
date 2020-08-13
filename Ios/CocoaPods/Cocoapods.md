*https://www.raywenderlich.com/626-cocoapods-tutorial-for-swift-getting-started*
  
#### Cocoapods  
swift와 objective-c의 dependency manager로 android gradle과 같은 역할을 수행한다.  
1. how to install with xcode  
- sudo gem install cocoapods  
(move to project folder)  
- pod setup  
- pod init (to create podfile)  
- open -e podfile || double click podfile  
platform :ios, '8.0'  
# Comment the next line if you're not using Swift and don't want to use dynamic frameworks  
use_frameworks!  
  
target 'MyApp' do  
  pod 'AFNetworking', '~> 2.6'  
  pod 'ORStackView', '~> 3.0'  
  pod 'SwiftyJSON', '~> 2.3'  
end  
- pod install (to install the dependencies)  
(after install dependencies, add Pods folder in project.  
after install cocoapods, open project with .xcworkspace file not .xcodeproj file.)  
  
2. Use pod install vs pod update  
- Use pod install to install new pods in your project.  
Even if you already have a Podfile and ran pod install before;  
So even if you are just adding/removing pods to a project already using CocoaPods.  
- Use pod update [PODNAME] only when you want to update pods to a newer version.  
  
3. Clear CocoaPods Cache  
pod deintegrate && pod cache clean --all  
