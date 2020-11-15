## Caching  
  
  
### How HTTP caching headers work  
Cache-control은 HTTP 헤더로 클라이언트 요청과 서버 응답 양쪽 모두에 브라우저의 캐싱 정책을 지정하는데 사용한다.  
캐싱 정책은 리소스가 캐싱되는 방법, 캐싱되는 위치, 캐싱 데이터가 파기되기까지 최대 기간 등을 포함한다.  
이 중 캐싱 데이터 최대 유지 기간은 대부분의 API들이 응답 헤더에 지정한다. 이 기간은 초단위 시간으로 수신자는 이 시간 내의 정보는 유효하다고 간주한다.  
이 기간이 지나면 응답은 오래된 것으로 간주되며, 새 데이터를 불러와야 한다.  
  
URLSession과 URLRequest는 기본적으로 useProtocolCachePolicy라는 캐시 정책을 가지고 있다.  
즉, URLSession과 URLRequest로 요청할 때, HTTP 캐싱 헤더를 완성한다는 것이다.  
위와 같은 경우에 헤더에 지정된 시간만큼 요청에 대한 응답을 캐싱할 것이다. 다른 옵션들을 사용하고자 한다면, 이를 override 할 수도 있다.  
  
### Caching in URLSession  
  
```swift
let url = URL(string: "https://postman-echo.com/response-headers?Content-Type=text/html&Cache-Control=max-age=30")!
let request = URLRequest(url: url)

let task = URLSession.shared.dataTask(with: url) { (data, response, error) in
	if let httpResponse = response as? HTTPURLResponse,
		let date = httpResponse.value(forHTTPHeaderField: "Date"),
		let cacheControl = httpResponse.value(forHTTPHeaderField: "Cache-Control") {
			print("Request1 date: \(date)")
			print("Request1 Cache Header: \(cacheControl)")
		}
}  
task.resume()

sleep(5)

let task2 = URLSession.shared.dataTask(with: url) { (data, response, error) in
	if let httpResponse = response as? HTTPURLResponse,
		let date = httpResponse.value(forHTTPHeaderField: "Date"),
		let cacheControl = httpResponse.value(forHTTPHeaderField: "Cache-Control") {
			print("Request2 date: \(date)")
			print("Request2 Cache Header: \(cacheControl)")
		}
}  
task2.resume()
```  
  
task1과 task2의 수행 결과는 다음과 같다.  

```git
Request1 date: Tue, 23 Jun 2020 09:21:36 GMT
Request1 Cache Header: max-age=30
Request2 date: Tue, 23 Jun 2020 09:21:36 GMT
Request2 Cache Header: max-age=30
```  
  
캐싱 유지 시간 내에 재요청했으므로 동일한 응답값을 받음을 확인할 수 있다.  
만약 Cache-Control=max-age=3으로 바꾸어 요청할 경우, 결과는 다음과 같을 것이다.  
  
```git
Request1 date: Tue, 23 Jun 2020 11:34:58 GMT
Request1 Cache Header: max-age=3
Request2 date: Tue, 23 Jun 2020 11:35:03 GMT
Request2 Cache Header: max-age=3
```  
  
캐싱 유지 시간을 지나 재요청을 하기 때문에 새로운 응답값을 받음을 확인할 수 있다.  

  
  
참조: https://medium.com/dev-genius/simple-offline-caching-in-swift-and-combine-e940427ad6e4  