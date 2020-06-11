*출처: https://developer.apple.com/library/archive/featuredarticles/XcodeConcepts/Concept-Targets.html*  
1. Target  
A target specifies a product to build and contains the instructions for building the product from a set of files in a project or workspace.  
타겟은 빌드의 결과로 만들어진 프로덕트이다. 그리고 타겟은 프로덕트를 빌드하기 위한 일련의 명령어 집합이 있는 단일 프로젝트 또는 워크스페이스의 파일모음들을 포함한다.  
Projects can contain one or more targets, each of which produces one product.  
프로젝트는 하나 이상의 타겟을 포함할 수 있으며, 타겟들은 각각 하나의 프로덕트를 만든다.  
The instructions for building a product take the form of build settings and build phases, which you can examine and edit in the Xcode project editor.  
프로덕트를 빌드하는 일련의 명령어 집합은 빌드 설정과 빌드 단계의 형태를 취하며, Xcode 프로젝트 편집기에서 이를 검토하고 편집할 수 있다.  
-> 즉, Target -> Build Phases, Build Settings에 나열된 항목들이 모두 instructions 이다.  
A target inherits the project build settings, but you can override any of the project settings by specifying different settings at the target level.  
타겟은 프로젝트 빌드 설정을 상속하지만, 타겟 레벨에서 다른 설정을 지정하여 프로젝트 설정을 재정의할 수 있다.  
There can be only one active target at a time; the Xcode scheme specifies the active target.  
한 번에 하나의 타겟만 활성화될 수 있으며, Xcode scheme이 활성화될 타겟을 지정한다.  
	
A target and the product it creates can be related to another target.  
타겟과 타겟이 생성한 프로덕트는 다른 타겟과 연관될 수 있다.  
If a target requires the output of another target in order to build, the first target is said to depend upon the second.  
만약 하나의 타겟이 빌드하기 위해 다른 타겟의 아웃풋을 필요로 한다면, 첫번째 타겟은 두번째 타겟에 의존한다고 말할 수 있다.  
If both targets are in the same workspace, Xcode can discover the dependency, in which case it builds the products in the required order.  
두 타겟이 같은 워크스페이스에 있고, Xcode가 그 종속성을 찾게 되면, 필요한 순서대로 프로덕트를 빌드한다.  
Such a relationship is referred to as an implicit dependency.  
이러한 관계를 암묵적 종속성이라 한다.  
You can also specify explicit target dependencies in your build settings,  
빌드 설정에서 명시적으로 타겟 종속성을 지정할 수도 있으며,  
and you can specify that two targets that Xcode might expect to have an implicit dependency are actually not dependent.  
Xcode가 암묵적 종속성을 가질 것으로 예상할 수 있는 두 타겟이 실제로 종속되지 않는다고 지정할 수도 있다.  
For example, you might build both a library and an application that links against that library in the same workspace.  
예를 들어, 같은 워크스페이스에서 라이브러리와 라이브러리와 연결할 응용프로그램을 모두 작성할 수 있다.  
Xcode can discover this relationship and automatically build the library first.  
Xcode는 이러한 관계를 발견하고 먼저 자동으로 라이브러리를 빌드할 수 있다.  
However, if you actually want to link against a version of the library other than the one built in the workspace,  
그러나 워크스페이스에 빌드된 라이브러리가 아닌 다른 버전의 라이브러리와 연결하려는 경우,  
you can create an explicit dependency in your build settings, which overrides this implicit dependency.  
빌드 설정에 명시적인 종속성을 만들 수 있으며, 이 종속성은 암묵적 종속성을 재정의한다.  