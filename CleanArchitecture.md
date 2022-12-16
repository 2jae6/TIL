# Clean Architecture + MVVM 습득하기

![img](https://blog.kakaocdn.net/dn/bWMRAV/btqFKC0qasx/jjFOnehurZAaf2gtGJscr0/img.png)

바깥쪽은 저수준 안쪽으로 갈수록 고수준이며 안쪽 단방향으로만 의존성을 갖는다. (안은 밖을 모르도록)



- **Domain Layer** = Entities + Use Cases + Repositories Interfaces

- **Data Repositories Layer** = Repositories Implementations + API (Network) + Persistence DB

- **Presentation Layer (MVVM)** = ViewModels + Views

  



전체적인 MVVM 구조 플로우를 살펴보면



뷰 -> 뷰모델 -> 모델 -> 뷰모델 -> 뷰

순서로 가잖아요?

클린아키텍쳐도 비슷해요

뷰 -> 뷰모델 -> 유즈케이스 -> 모델 -> 유즈케이스 -> 뷰모델 -> 뷰

여기서 모델이 API, 혹은 Core Data 일수도 있으니 레퍼지토리 패턴을 사용해 추가한다면?

뷰 -> 뷰모델 -> 유즈케이스 -> 레퍼지토리 -> 모델 -> 레퍼지토리 -> 유즈케이스 -> 뷰모델 -> 뷰

하나의 액션 사이클이 이렇게 될 것 같습니다.









레퍼런스

https://github.com/kudoleh/iOS-Clean-Architecture-MVVM

https://ios-development.tistory.com/555

