1. Old #if DEBUG pattern  
It’s not secured because it contains secret data such as passwords and keys right inside your repository.  
This makes it kind of a mess when you need to distinguish between environments.  
Additionally, it doesn’t support other types of values such as app name or icon.  
  
2. XCConfig  
Xcode Configuration File. A text file containing key and value pairs.  
When attaching a configuration file to a build configuration, it can override or modify certain variables in the build and even add new ones.  
Consequently, this provides flexibility when configuring your app to different environments.  
  
3. Schemes  
Schemes are created by default for each target of your project, where the target can be either executable or a framework.  
For every scheme, you can define the configuration for running, archives, or testing.  
  
4. Configuration  
The configuration is a set of values that you attach to a scheme and an action.  
ex. You can define different configurations for different endpoint servers.  
You can configure your app in a way that your Production Scheme will archive your project to the production server,  
but the tests will work with development server.  
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
- How to edit configuration?  
	Project -> Info -> Configurations  
	As a default, you have Debug and Release configurations.  
  
5. How to set XCConfig?  
- Add XCConfig file  
	New File -> Configuration Settings File  
- Attach a configuration file  
	Project -> Info -> Configurations  
	Now you can attach a configuration file for each configuration you defined, and even for each target.  
*Note: If you’re using Cocoapods, you’ll have to delete your workspace and your Podfile.lock files, and run Poddfile install again.*  
  
6. Edit XCConfig  
Xcode treats “//“ as a comment, even if it’s part of a URL, so take this into account.  
You can work around this by putting another symbol in place of “//“ and replace it in your code afterward.  
Each value in the config file is translated to a string afterward, so no need to wrap it with quotation marks.  
*configuration settings file format documentation: https://help.apple.com/xcode/#/dev745c5c974*  
  
7. Inheritance  
Use #include to other XCConfig files and add $(inherited) keyword.  
  
8. Accessing Value From Code  
In info.plist: $(variable name)  
ex. $(APP_NAME)  
In code:  
func getValue(forKey key : String) -> String? {  
	Bundle.main.infoDictionary?[key] as? String  
}  
