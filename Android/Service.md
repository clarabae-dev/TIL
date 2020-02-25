0. Error  
* 내용: android.util.AndroidRuntimeException:  
Calling startActivity() from outside of an Activity context requires  
the FLAG_ACTIVITY_NEW_TASK flag. Is this really what you want?  
- 해결: 서비스는 테스크가 없기 때문에 액티비티를 시작하려면 new task 플래그를 지정해야 한다.  
* 내용: 안드로이드 Q(10) 이상부터 잠금화면 이슈  
- 해결: 설정 -> 어플리케이션 -> bigwalk -> 고급 -> 다른 앱 위에 표시 허가  
