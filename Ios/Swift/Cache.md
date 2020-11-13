## Caching  
  
  
### How HTTP caching headers work  
Cache-control은 HTTP 헤더로 클라이언트 요청과 서버 응답 양쪽 모두에 브라우저의 캐싱 정책을 지정하는데 사용한다.  
캐싱 정책은 리소스가 캐싱되는 방법, 캐싱되는 위치, 캐싱 데이터가 파기되기까지 최대 기간 등을 포함한다.  
이 중 캐싱 데이터 최대 유지 기간은 대부분의 API들이 응답 헤더에 지정한다. 이 기간은 초단위 시간으로 수신자는 이 시간 내의 정보는 유효하다고 간주한다.  
이 기간이 지나면 응답은 오래된 것으로 간주되며, 새 데이터를 불러와야 한다.  
  
URLSession과 URLRequest는 기본적으로 useProtocolCachePolicy라는 캐시 정책을 가지고 있다.  
즉, URLSession과 URLRequest로 요청할 때, HTTP 캐싱 헤더를 완성한다는 것이다.  
위와 같은 경우에 헤더에 지정된 시간만큼 요청에 대한 응답을 캐싱할 것이다. 다른 옵션들을 사용하고자 한다면, 이를 override 할 수도 있다.  
  
.. 작성 중 
  
  
  
참조: https://medium.com/dev-genius/simple-offline-caching-in-swift-and-combine-e940427ad6e4  