1. CI  
Continuous Integration, 지속적 통합.  
Build, Test를 실시하는 통합 프로세스를 의미하며, 이러한 통합 프로세스를 상시적으로 수행하는 것.  
Build, Test and Archive the app.  
iOS CI: Xcode Server, Jenkins, Travis, Fastlane  
  
2. Xcode Server  
A CI server created by Apple in order to assist iOS developers with their CI needs.  
Xcode Server(XCS) calls them bots, Jenkins calls them jobs but they are the same thing, scheduled tasks.  
  
- Pros  
	Integrates very well with Xcode.  
	Has a web dashboard for monitoring your bots.  
	Can create installable ipa's and you can install them in the web dashboard.  
- Cons  
	Has issues with the most basic tasks like checking out source code when you have submodules.  
	Can't add multiple builder nodes and bots are slow to run, impossible to scale up.  
	Too focused around XCode specific tasks, doesn't allow for other kinds of jobs.  
	Almost non-existant third-party integrations.  
	Impossible to debug build issues.  
	Only good for unit and ui testing.  
  
3. Travis CI  
Github CI server.  
  
- Pros  
	Easy to setup.  
	Configurable, Xcode and tooling is maintained for you.  
	Great integration with Github.  
	Well documented and widely adopted in open source community.  
	Nice user interface.  
- Cons  
	Doesn't work if your code isn't on Github.  
	Pricey or limited build capacity for paid plans.  
	A lot less configurations and plugins compared to Jenkins.  
  
4. Jenkins + Fastlane  
Fastlane is a set of command line tools, that allows a developer to build his app:  
fastlane gym --scheme YourSchemeName  
  
Or to run unit tests:  
fastlane scan --scheme YourSchemeName  
  
To run UI Tests on a specific device  
fastlane scan --scheme UITestsScheme --devices 'iPhone 5s'  
  
Or even to upload his app test flight:  
fastlane pilot upload --ipa PathToIpa  
