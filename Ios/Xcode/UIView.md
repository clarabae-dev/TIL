### Opaque  
뷰의 불투명 여부를 결정하는 boolean 값이다.  
1. Yes  
뷰가 완전히 불투명하게 그려진다.  
2. No  
뷰가 투명하게 그려질 수 있으며, alpha 값을 통해 투명도를 조절할 수 있다.  
  
### UIColor  
1. UIColor(displayP3Red:green:blue:alpha)  
DCI P3는 디지털 영사기의 색영역으로 사용하기 위해 Digital Cinema Initiatives에서 정의한 색영역이다.  
기존 sRGB보다. 25% 더 넓은 색영역을 표현할 수 있고 적색에 특히 더 넓은 커버리지를 갖추었다.  
Display P3는 애플이 DCI-P3를 디스플레이 환경에 맞춰 수정하여 개발한 규격이다.  
아이폰 7 이후로는 기본 사진앱으로 촬영한 모든 사진들은 P3 색영역을 기본으로 지정하고 있다.  
해당 메소드는 Display P3 color space에 해당하는 컬러 객체를 생성한다.  
  
> color space: 색 표시계를 3차원으로 표현한 공간 개념.  
  
2. 컬러 프로필에 따라 rgb값 변경하기.  
storyboard -> color custom -> 톱니바퀴 -> 컬러 프로필 선택  
sRGB와 displayP3 등 Generic RGB와는 다른 rgb 값이 나온다.  
  
3. 코드로 적용한 컬러가 다르게 나올 경우.  
2번의 방법대로 먼저 제플린 컬러를 Generic RGB 값으로 뽑는다.  
다시 설정에서 displayP3로 옵션을 변경하면, 옵션에 해당하는 컬러값이 새로 나온다. 이를 코드에 적용한다.  
  
### UIButton  
UIButton을 extension하여 backgroundColor를 변경하려고 시도하면 잘 동작하지 않는다.  
실제 UIButton 컴포넌트 문서를 보아도 backgroundColor에 대한 설명은 없다. 대신 backgroundImage를 설정하도록 한다.  
  
### UIImageView  
UIImageView에서 적용할 수 있는 사이즈와 비율 옵션은 다음과 같다.  
1. Scale To Fill  
이미지 원본의 비율을 무시하고 전체 이미지가 UIImageView에 들어가도록 한다. 전체 이미지가 보여지지만 비율 왜곡이 발생할 수 있다.  
2. Aspect Fit  
이미지 원본의 비율을 유지하면서 이미지를 모두 표시한다. 따라서 이미지가 매우 작게 나올 수도 있다.  
3. Aspect Fill  
이미지 원본의 비율을 유지하면서 UIImageView에 가득 차보이도록 한다. 비율이 유지되기 때문에 부분적으로 이미지가 짤릴 수 있다.  
이미지가 UIImageView 영역을 벗어날 수 있는데 UIImageView에 ClipToBounds 항목을 체크해주거나 다음의 코드를 작성한다.  
  
```swift
imageView.layer.masksToBounds = true
```  
  
  
  
  
참조: https://namu.wiki/w/%EC%83%89%20%EC%98%81%EC%97%AD  