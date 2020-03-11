#### 점선 그리기  
1. xml  
- shape 그리기  
<shape xmlns:android="http://schemas.android.com/apk/res/android"  
    android:shape="line">  
    <stroke  
        android:color="#ffff00" // 점선 색  
        android:width="1dp" // 점자 두께  
        android:dashWidth="10dp" // 점자 길이  
        android:dashGap="10dp"/> // 점자 간격  
</shape>  
- 뷰에 적용하기  
android:layerType="software" // 이렇게 설정해야 점선이 보임.  
android:layout_height 값은 점선의 width보다 큰 값이어야 한다. wrap_content도 안됨.  
