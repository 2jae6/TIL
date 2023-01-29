
# Combine

Publisher 가 시간의 흐름에따라 비동기 이벤트를 나타내고 Subscriber 들이 값을 받도록합니다. (대부분 프로토콜로 이루어져있음)
(TL; DR RxSwift Apple Version)


### Publisher (구냥 옵저버블)
-> 값을 시간에 따라 전송할 수 있습니다. (Subscriber 에게 Element 를 전송한다는거죠) Output, Failure 타입이 제네릭으로 구현되어있으며 `Future`, `Just`, `Deferred`, `Empty`, `Fail`, `Record` 
등을 통해 구현할 수 있습니다.

```swift
let publisher = Just("Wookoo") // Just 는 Rx 의 Just 처럼 하나의 요소를 방출하는 옵저버블(여기선 퍼블리셔) 를 만드는 타입인가봄.
```

### Subscriber (구냥 구독자)
->  Publisher 로부터 input 을 받는 프로토콜로 Input, Failure 가 제네릭으로 구현되어있음. (Rx 와 동일한 기능)


```swift
let subscriber = publisher.sink(receiveCompletion: { result in
     switch result {
         case .finished:
              print("finished")
         case .failure(let error):
              print("error")
      }
}, receiveValue: { value in
      print(value)
})

Just("Wook").sink { value in
  print(value)
}
```


레퍼런스
https://zeddios.tistory.com/925

https://icksw.tistory.com/271
