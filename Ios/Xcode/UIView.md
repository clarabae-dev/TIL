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
  
  
  
참조: https://namu.wiki/w/%EC%83%89%20%EC%98%81%EC%97%AD  