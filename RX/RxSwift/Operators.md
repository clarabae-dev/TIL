> RxSwift github의 해당 내용을 번역 및 추가한 내용입니다.
  
## Filtering  
  
  
### Debounce  
  
![Alt text](https://miro.medium.com/max/1400/1*qAVY1KT8EOQ5mOtzOy610w.png)  
  
origin stream이 계속 이벤트를 발생시키더라도 방출하지 않다가 지정한 시간이 흐른 후 가장 최근 발생한 이벤트만 방출한다.  
이벤트가 방출될 때마다 시간은 초기화되어 다시 시작한다.  
> debounce: 퇴짜 놓다  

UISearchBar.rx.text는 검색창에 포커스할 때, 자음/모음 입력마다 text를 배출한다. 배출될 때마다 실시간으로 api를 호출할 경우 부담이 된다.  
이 경우, debounce를 활용해 텍스트 입력 후, 일정 시간 동안 동작이 없으면 text를 배출하도록 조절할 수 있다.  
  
```swift
searchBar.rx.text.orEmpty
            .skip(1)
            .distinctUntilChanged()
            .debounce(.milliseconds(300), scheduler: MainScheduler.instance)
            .subscribe(onNext: { [weak self] searchText in
                self?.viewModel.searchText = searchText
                self?.viewModel.fetchRooms()
            }).disposed(by: disposeBag)
```  
  
  
### Throttle  
origin stream이 이벤트를 처음 방출한 후, 지정한 시간 동안 어떤 이벤트도 방출하지 않는다.  
이벤트가 방출될 때마다 시간이 초기화되지 않는다. 시간이 종료되었을 때는 latest 인자에 따라 결과가 달라진다.  
  
#### latest = true  
  
![Alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcfinEo%2FbtqAHoT41VX%2FeNKYDkk0PkpNk0lf6wBxKK%2Fimg.png)  
  
지정한 시간이 종료되면, 종료되었을 때 가장 최근에 발생한 이벤트를 방출하고 다시 시간이 초기화되어 시작된다.  
지정한 시간동안 아무 이벤트가 발생하지 않았다면, 시간 종료 후에도 이벤트를 방출하지 않고, 다음 이벤트가 발생하였을 때 해당 이벤트를 내보내고 시간이 초기화되어 시작된다.  
  
#### latest = false  
  
![Alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFHhJI%2FbtqAIEoqwph%2FLDzpkMXrsLILezDIJH1KY0%2Fimg.png)  
  
지정한 시간이 종료되어도 아무 이벤트도 방출되지 않는다. 새로운 이벤트가 발생하면 해당 이벤트를 방출하고 시간이 초기화되어 시작된다.  
사용자가 버튼을 눌러 새로고침할 경우, throttle latest = true를 활용해 여러 번 버튼을 눌러도 새로고침은 딱 한번만 발생할 수 있도록 할 수 있다.  
  
### skip  
skip(count: n)을 활용하여 첫 n번째 이벤트를 방출에서 제외할 수 있다.  
  
  
  
## Error Handling  
  
  
### Retry  
  
![Alt text](http://reactivex.io/documentation/operators/images/retry.C.png)  
  
Observable 소스가 오류를 방출했을 때, resubscribe한다. retry는 Observable 소스의 onError에 응답한다.  
다만 observer에 호출을 전달하지 않고, Observable 소스를 resubscribe하여 오류없이 완료될 수 있도록 기회를 준다.  
retry는 오류로 끝나는 시퀀스에서도 항상 observer에게 onNext를 전달하므로 중복된 방출이 발생할 수 있다.  
  
#### retry  
오류가 발생하였을 때 성공할 때까지 Observable을 resubscribe한다.  

#### retry(maxAttemptCount: Int)  
subscribe할 최대 횟수를 지정할 수 있다. retry(2)라면 첫시도, 재시도까지 총 두번의 시도가 발생한다. 지정한 횟수를 초과하면 error를 전달한다.  
  
#### retryWhen  
retry 시점을 지정할 수 있고, 한번만 수행된다. retry와 달리 마지막 error를 전달하지 않는다.  
  
  
  
참조:  
http://reactivex.io/documentation/operators.html  
https://jcsoohwancho.github.io/2019-09-05-Rxswift%EC%97%B0%EC%82%B0%EC%9E%90-throttle/  
https://damor.tistory.com/6  
https://medium.com/@ggaa96/rxswift-5-error-handling-example-9f15176d11fc  