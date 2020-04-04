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

#### ConstraintLayout  
1. layout_constraintEnd_toStartOf 를 활용해 뷰의 너비를 제한하고 싶을 때,  
[ A ] [   B   ] [ C ]  
즉, B 뷰가 C 뷰를 침법하지 못하도록 막고 싶을 때, B 뷰의 width를 0dp로 설정한다.  
layout_width = "0dp"  
layout_constraintStart_toEndOf = "@+id/A"  
layout_constraintEnd_toStartOf = "@+id/C"  
layout_constraintHorizontal_bias="0"  

2. 특정 뷰와 너비를 동일하게 하고 싶을 때,  
[ A ]  
[ B ]  
layout_width = "0dp"  
layout_constraintStart_toStartOf = "@+id/A"  
layout_constraintEnd_toEndOf = "@+id/A"  
