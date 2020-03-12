1. Reboot Receiver  
- <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />  
- <action android:name="android.intent.action.BOOT_COMPLETED" /> 인텐트 필터만으로  
리부트 리시버가 동작하지 않을 수 있다. '다시 시작'을 하는 경우  
<action android:name="android.intent.action.QUICKBOOT_POWERON" /> 필터를 추가한다.  
단, BOOT_COMPLETED와 QUICKBOOT_POWERON 필터를 <intent-filter></intent-filter>로  
각각 분리해서 적어줘야 한다.  

2. 앱 업데이트 후에도 적용해야하는 서비스가 있는 경우  
- <action android:name="android.intent.action.MY_PACKAGE_REPLACED"/>  
위 action이 등록된 broadcastreceiver를 추가한다.  

3. Never Die Service  
절대 죽지 않는 서비스를 구현할 때와 같이, 서비스나 리시버를 별도의 프로세스에서 실행하려면  
App Manifest에 android:process 속성을 추가해야 한다.  
- android:process=":<프로레스명>"  

4. lateinit property has not been initialized  
* lateinit 조건  
- var(mutable)에서만 사용이 가능하다  
- var이기 때문에 언제든 초기화를 변경할 수 있다.  
- null로 초기화할 수 없다.  
- 초기화를 하기 전에는 변수에 접근할 수 없다.  
lateinit property subject has not been initialized 오류 발생  
- 변수에 대한 setter/getter properties 정의가 불가능하다.  
- lateinit은 모든 변수가 가능한 건 아니고, primitive type에서는 활용이 불가능하다(Int, Double 등)  
* 초기화 확인 방법  
.isInitialized (::을 통해서만 접근이 가능)  
예시: if (::sampleAdapter.isInitialized)  

5. NoSuchMethodException in Activity OnCreate  
activity는 savedInstanceState bundle에서 복구되는데, 복구 작업 중 fragment도 재생성한다.  
activity의 fragment가 파라미터가 있는 생성자를 갖고 있는 경우, 발생할 수 있는 오류.  
> stackoverflow  

* 적용한 방법  
Fragment.newInstance()  

6. KotlinNullPointerException  
!! 사용할 경우 발생  
* 적용한 방법  
!!의 사용을 지양하며, ?로 항상 체크해준다.  
