*출처: https://developer.apple.com/library/archive/featuredarticles/XcodeConcepts/Concept-Targets.html*  
1. Target  
A target specifies a product to build and contains the instructions for building the product from a set of files in a project or workspace.  
타겟은 빌드의 결과로 만들어진 프로덕트이다. 그리고 타겟은 프로덕트를 빌드하기 위한 일련의 명령어 집합이 있는 단일 프로젝트 또는 워크스페이스의 파일모음들을 포함한다.  
Projects can contain one or more targets, each of which produces one product.  
프로젝트는 하나 이상의 타겟을 포함할 수 있으며, 타겟들은 각각 하나의 프로덕트를 만든다.  
The instructions for building a product take the form of build settings and build phases, which you can examine and edit in the Xcode project editor.  
프로덕트를 빌드하는 일련의 명령어 집합은 빌드 설정과 빌드 단계의 형태를 취하며, Xcode 프로젝트 편집기에서 이를 검토하고 편집할 수 있다.  
*-> 즉, Target -> Build Phases, Build Settings에 나열된 항목들이 모두 instructions 이다.*  
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
  	
2. Project  
An Xcode project is a repository for all the files, resources, and information required to build one or more software products.  
Xcode 프로젝트란 하나 이상의 소프트웨어 프로덕트를 빌드하는데 필요한 모든 파일, 리소스, 정보들의 저장소이다.  
A project contains all the elements used to build your products and maintains the relationships between those elements.  
하나의 프로젝트는 프로덕트를 빌드하는데 필요한 모든 요소들을 가지며, 이 요소들 간의 관계성을 유지한다.  
It contains one or more targets, which specify how to build products.  
프로젝트는 어떻게 프로덕트를 빌드할지 명시해놓은 하나 이상의 타겟을 가진다.  
A project defines default build settings for all the targets in the project.  
프로젝트는 프로젝트 내의 모든 타겟들에 적용되는 기본 빌드 설정을 정의한다.  
(each target can also specify its own build settings, which override the project build settings.)  
(각각의 타겟은 고유의 빌드 설정도 지정할 수 있으며, 타겟 고유의 빌드 설정은 프로젝트 단위의 빌드 설정을 재정의한다.)  
  
An Xcode project file contains the following information: Xcode 프로젝트는 다음의 정보들을 포함한다.  
- References to source files: 소스 파일에 대한 참조  
	Source code, including header files and implementation files: 헤더 파일 및 구현 파일을 포함한 소스코드  
	Libraries and frameworks, internal and external  
	Resource files  
	Image files  
	Interface Builder (nib) files  
- Groups used to organize the source files in the structure navigator: structure navigator에서 소스파일을 구성하는데 사용되는 그룹  
- Project-level build configurations. You can specify more than one build configuration for a project; for example, you might have debug and release build settings for a project.  
  프로젝트 레벨의 빌드 구성. 하나의 프로젝트에 대해 둘 이상의 빌드 구성을 지정할 수 있다; 예를 들어, 하나의 프로젝트에 debug와 release 빌드 설정을 구성할 수 있다.  
- Targets, where each target specifies: 타겟들. 각각의 타겟들은 다음을 지정할 수 있다.  
	A reference to one product built by the project: 프로젝트로 인해 빌드된 하나의 프로덕트에 대한 참조.  
	References to the source files needed to build that product: 위 프로덕트를 빌드하는데 필요한 소스파일에 대한 참조.  
	The build configurations that can be used to build that product, including dependencies on other targets and other settings;  
	빌드 구성. 빌드 구성은 다른 타겟들과 다른 설정에 대한 의존성을 포함해 위 프로덕트를 빌드하는데 쓰일 수 있다.  
	the project-level build settings are used when the targets’ build configurations do not override them.  
	프로젝트 레벨의 빌드 설정은 타겟의 빌드 구성이 자신을 재정의하지 않을 때 사용된다.  
- The executable environments that can be used to debug or test the program, where each executable environment specifies:  
  실행 가능한 환경. 실행 가능한 환경은 프로그램을 디버깅하거나 테스트할 때 쓰일 수 있다. 각 실행가능한 환경은 다음을 지정한다.  
	What executable to launch when you run or debug from Xcode  
	Xcode에서 실행하거나 디버깅할 때 실행할 실행 파일.  
	Command-line arguments to be passed to the executable, if any  
	실행 파일에 전달할 명령줄 매개변수(존재하는 경우에만).  
	Environmental variables to be set when the program runs, if any  
	프로그램이 실행될 때 할당되는 환경 변수(존재하는 경우에만).  
  
A project can stand alone or can be included in a workspace.  
프로젝트는 독립적일 수도 있고 하나의 워크스페이스에 포함될 수도 있다.  
You use Xcode schemes to specify which target, build configuration, and executable configuration is active at a given time.  
Xcode scheme을 활용해 어떤 타겟, 빌드 구성, 실행 구성을 활성화 시킬 것인지 지정할 수 있다.  
  
3. Build Settings  
A build setting is a variable that contains information about how a particular aspect of a product’s build process should be performed.  
빌드 설정은 프로덕트의 빌드 프로세스의 특정 부분들이 어떻게 수행되어야 할지에 대한 정보들을 가지고 있는 변수이다.  
For example, the information in a build setting can specify which options Xcode passes to the compiler.  
예를 들어, 빌드 구성의 정보는 Xcode가 컴파일러에 전달할 옵션들을 지정한다.  
You can specify build settings at the project or target level.  
프로젝트나 타겟 레벨에서 빌드 구성을 지정할 수 있다.  
Each project-level build setting applies to all targets in the project unless explicitly overridden by the build settings for a specific target.  
각 프로젝트 레벨의 빌드 설정은 프로젝트 내의 모든 타겟들에 적용된다. 단, 특정 타겟에 대해 명시적으로 빌드 설정이 재정의된 경우에는 프로젝트 레벨의 빌드 설정은 타겟에 적용되지 않는다.  
Each target organizes the source files needed to build one product.  
각 타겟은 하나의 프로덕트를 빌드하는데 필요한 소스파일들을 구조화한다.  
A build configuration specifies a set of build settings used to build a target's product in a particular way.  
빌드 구성은 특정 방식으로 타겟의 프로덕트를 빌드하는데 사용할 빌드 설정들의 집합을 지정한다.  
-> 빌드 구성에서 어떤 종류의 최종 프로덕트를 빌드할 것인지를 지정할 수 있다는 의미. 어떤 종류의 프로덕트가 빌드될 것인지는 빌드 설정에 따라 달라질 것이다.  
For example, it is common to have separate build configurations for debug and release builds of a product.  
예를 들어, 일반적으로 프로덕트의 debug와 release 빌드는 각각 별도의 빌드 구성을 갖는다.  
  
A build setting in Xcode has two parts: the setting title and the definition.  
Xcode의 빌드 설정은 설정 title과 definition으로 구성된다.  
The build setting title identifies the build setting and can be used within other settings.  
빌드 설정 title은 빌드 설정을 식별하고 다른 설정에서 사용될 수도 있다.  
The build setting definition is a constant or a formula Xcode uses to determine the value of the build setting at build time.  
빌드 설정 definition은 상수이거나 Xcode가 빌드할 때, 빌드 설정의 값을 결정하는데 사용하는 수식이다.  
A build setting may also have a display name, which is used to display the build setting in the Xcode user interface.  
빌드 설정은 Xcode UI에서 빌드 설정을 보여주는데 사용될 display name도 포함될 수 있다.  
In addition to the default build settings provided by Xcode when you create a new project from a project template,  
프로젝트 템플릿에 새 프로젝트를 만들 때, Xcode가 제공하는 기본 빌드 설정 외에도  
you can create user-defined build settings for your project or for a particular target.  
프로젝트 또는 특정 타겟에 대해 사용자 정의 빌드 구성을 만들 수 있다.  
You can also specify conditional build settings.  
또 조건부 빌드 설정을 지정할 수도 있다.  
The value of a conditional build setting depends on whether one or more prerequisites are met.  
조건부 빌드 설정의 값은 하나 이상의 선행 조건이 충족되었는지에 따라 달라진다.  
This mechanism allows you to, for example, specify the SDK to use to build a product based on the targeted architecture.  
예를 들어, 이 매커니즘을 활용해 타겟 아키텍쳐를 기반으로 프로덕트를 빌드하는데 사용할 SDK를 지정할 수도 있다.  
  
4. Workspace  
A workspace is an Xcode document that groups projects and other documents so you can work on them together.  
워크스페이스는 프로젝트 및 기타 문서를 그룹화하여 함께 작업할 수 있도록 하는 Xcode 문서이다.  
A workspace can contain any number of Xcode projects, plus any other files you want to include.  
워크스페이스는 원하는 수만큼의 Xcode 프로젝트와 다른 파일을 포함할 수 있다.  
In addition to organizing all the files in each Xcode project, a workspace provides implicit and explicit relationships among the included projects and their targets.  
각 Xcode 프로젝트의 모든 파일을 정리하는 것 외에도, 워크스페이스는 포함된 프로젝트와 그 타겟들 사이의 암묵적이고 명시적인 관계를 제공한다.  

- Workspaces Extend the Scope of Your Workflow  
  워크스페이스는 작업 흐름의 범위를 확장한다.  
	A project file contains pointers to all the files in the project, along with build configurations and other project information.  
	프로젝트 파일에는 빌드 구성 및 기타 프로젝트 정보와 함께 프로젝트의 모든 파일에 대한 포인터가 포함되어 있다.  
	In Xcode 3 and earlier, the project file is always the root of the group and file structure hierarchy.  
	Xcode 3 이하에서는 프로젝트 파일이 항상 그룹과 파일 구조 계층의 최상위 레벨이었다.  
	Although a project can contain references to other projects, working on interrelated projects in Xcode 3 is complicated; most workflows are confined to a single project.  
	프로젝트가 다른 프로젝트에 대한 참조를 포함할 수 있지만, Xcode 3에서 서로 연관된 프로젝트들에 대한 작업은 복잡하다. 대부분의 작업 흐름은 단일 프로젝트에 국한된다.  
	In Xcode 4 and later, you have the option of creating a workspace to hold one or more projects, plus any other files you wish to include.  
	Xcode 4 이상에서는 하나 이상의 프로젝트와 포함하려는 다른 파일을 추가해 워크스페이스를 생성할 수 있다.  
  
	In addition to providing access to all the files in each included Xcode project, a workspace extends the scope for many important Xcode workflows.  
	워크스페이스는 내부에 포함된 각 Xcode 프로젝트에 있는 모든 파일에 대한 접근성을 제공하는 것 외에도, 많은 중요한 Xcode 작업 흐름의 범위를 확장한다.  
	For example, because indexing is done across the whole workspace,  
	예를 들어 인덱싱은 전체 워크스페이스에서 수행되기 때문에  
	code completion, Jump to Definition, and all other content-aware features work seamlessly through all projects in the workspace.  
	코드 완성, Definition으로의 이동 및 기타 모든 컨텐츠 인식 기능이 워크스페이스 내의 모든 프로젝트를 통해 원활하게 작동한다.  
	*-> 코드 자동 완성, 정의 보기 등의 기능이 하나의 워크스페이스 내에 있는 모든 프로젝트끼리는 원활하게 동작한다.*  
	Because refactoring operations act across all the content of the workspace,  
	리팩터링 연산은 워크스페이스의 모든 내용에 걸쳐 작용되기 때문에,  
	you can refactor the API in a framework project and in several application projects that use that framework all in one operation.  
	당신은 프레임워크 프로젝트와 그 프레임워크를 한 번의 연산으로 사용하는 여러 애플리케이션 프로젝트에서 API를 리팩터링할 수 있다.  
	*-> 그래서, 라이브러리 내부 코드를 자유롭게 리펙토링이 가능한 것 같다.*  
	When building, one project can make use of the products of other projects in the workspace.  
	빌드할 때, 하나의 프로젝트는 워크스페이스에 있는 다른 프로젝트의 프로덕트를 사용할 수 있다.  
	*-> 라이브러리, 프레임워크를 자유롭게 활용할 수 있는 이유.*  

	The workspace document contains pointers to the included projects and other files, but no other data.  
	워크스페이스 문서에는 내부에 포함된 프로젝트 및 기타 파일에 대한 포인터가 포함되지만 다른 데이터는 포함되지 않는다.  
	A project can belong to more than one workspace.  
	프로젝트는 둘 이상의 워크스페이스에 속할 수 있다.  
  
- Projects in a Workspace Share a Build Directory  
  하나의 워크스페이스에 있는 프로젝트들은 빌드 디렉토리를 공유한다.  
  	By default, all the Xcode projects in a workspace are built in the same directory, referred to as the workspace build directory.  
  	기본적으로 워크스페이스의 모든 Xcode 프로젝트는 워크스페이스 빌드 디렉토리라고 하는 동일한 디렉토리에 구축된다.  
  	Each workspace has its own build directory.  
  	각 워크스페이스는 고유한 빌드 디렉토리를 가지고 있다.  
  	Because all of the files in all of the projects in a workspace are in the same build directory, all of these files are visible to each project.  
  	워크스페이스의 모든 프로젝트에 있는 모든 파일이 동일한 빌드 디렉터리에 있기 때문에 이 모든 파일들은 각 프로젝트에서 볼 수 있다.  
  	Therefore, if two or more projects use the same libraries, you don’t need to copy them into each project folder separately.  
  	따라서 둘 이상의 프로젝트가 동일한 라이브러리를 사용하는 경우, 각 프로젝트 폴더에 별도로 라이브러리를 복사하지 않아도 된다.  

  	Xcode examines the files in the build directory to discover implicit dependencies.  
  	Xcode는 빌드 디렉토리의 파일을 검사하여 암묵적 종속성을 발견한다.  
  	For example, if one project included in a workspace builds a library that is linked against by another project in the same workspace,  
  	예를 들어, 한 프로젝트가 동일한 워크스페이스의 다른 프로젝트에 의해 연결된 라이브러리를 빌드하는 경우,  
  	Xcode automatically builds the library before building the other project, even if the build configuration does not make this dependency explicit.  
  	빌드 구성이 이 종속성을 명시하지 않더라도 Xcode는 다른 프로젝트를 구축하기 전에 라이브러리를 자동으로 구축한다.  
  	You can override such implicit dependencies with explicit build settings if necessary.  
  	필요한 경우 이러한 암묵적 의존성을 명시적 빌드 설정으로 재정의할 수 있다.  
  	For explicit dependencies, you must create project references.  
  	명시적 종속성을 위해 프로젝트 참조를 만들어야 한다.  
  
  	Each project in a workspace continues to have its own independent identity.  
  	워크스페이스의 각 프로젝트는 독립적인 정체성을 추구한다.  
  	To work on a project without affecting—or being affected by—the other projects in the workspace,  
  	워크스페이스의 다른 프로젝트에 영향을 주거나 영향을 받지 않고 프로젝트를 진행하려면,  
  	you can open the project without opening the workspace, or you can add the project to another workspace.  
  	그 워크스페이스를 열지 않고 프로젝트를 열거나 다른 워크스페이스에 프로젝트를 추가할 수 있다.  
  	Because a project can belong to more than one workspace,  
  	한 프로젝트는 둘 이상의 워크스페이스에 속할 수 있기 때문에  
  	you can work on your projects in any number of combinations without having to reconfigure any of the projects or workspaces.  
  	프로젝트나 워크스페이스를 재구성할 필요 없이 원하는 수의 조합으로 프로젝트를 수행할 수 있다.  
  
  	You can use the workspace’s default build directory or you can specify one.  
  	워크스페이스의 기본 빌드 디렉토리를 사용하거나 지정할 수 있다.  
  	Note that if a project specifies a build directory,  
  	프로젝트가 빌드 디렉토리를 지정하는 경우, 다음을 유의해라.  
  	that directory is overridden by the build directory of whatever workspace the project is in at the time you build the project.  
  	프로젝트를 빌드할 때 프로젝트가 있는 워크스페이스의 빌드 디렉토리에 의해 해당 디렉토리가 재정의될 수 있다.  
  
5. Scheme  
An Xcode scheme defines a collection of targets to build, a configuration to use when building, and a collection of tests to execute.  
Xcode scheme은 빌드할 타겟의 집합, 빌드할 때 사용할 구성 및 실행할 테스트 집합을 정의한다.  
  
You can have as many schemes as you want, but only one can be active at a time.  
scheme은 얼마든지 가질 수 있지만 한 번에 하나만 활성화할 수 있다.  
You can specify whether a scheme should be stored in a project—in  
scheme을 프로젝트에 저장할지 워크스페이스에 저장할지 지정할 수 있다.  
which case it’s available in every workspace that includes that project, or in the workspace—in which case it’s available only in that workspace.  
프로젝트에 저장하는 경우, 해당 프로젝트를 포함하는 모든 워크스페이스에서 사용할 수 있고, 워크스페이스에 저장할 경우, 워크스페이스에서만 사용할 수 있다.  
When you select an active scheme, you also select a run destination (that is, the architecture of the hardware for which the products are built).  
활성 scheme을 선택할 때는 실행 대상(프로덕트가 빌드될 하드웨어의 아키텍처)도 선택해야 한다.  