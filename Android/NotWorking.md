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
