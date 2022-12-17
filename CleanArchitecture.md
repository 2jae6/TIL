# Clean Architecture + MVVM 습득하기

![img](https://blog.kakaocdn.net/dn/bWMRAV/btqFKC0qasx/jjFOnehurZAaf2gtGJscr0/img.png)

바깥쪽은 저수준 안쪽으로 갈수록 고수준이며 안쪽 단방향으로만 의존성을 갖는다. (안은 밖을 모르도록)



- **Domain Layer** = Entities + Use Cases + Repositories Interfaces

- **Data Repositories Layer** = Repositories Implementations + API (Network) + Persistence DB

- **Presentation Layer (MVVM)** = ViewModels + Views

 
 

### 뷰모델과 유즈케이스의 역할
- 비즈니스로직은 유즈케이스에 넣어야함
- 클린 아키텍처의 뷰모델 역할은 UI 이벤트들이 발생하면 무엇을 해야하는지 알고있는 것입니다.

### 레퍼지토리 구성 방법
아키텍처에 정답이 없어서 다양한 구현 방법이 있지만 레퍼지토리의 프로토콜은 도메인 계층에 두고 구현부는 데이터 계층에서 구현하는 것을 많이 사용하는 것 같습니다.
레퍼지토리의 역할은 Service 를 실행 시켜 필요한 데이터를 만들어 유즈케이스에 반환 시킬 수 있도록 구현합니다.



레퍼런스

https://github.com/kudoleh/iOS-Clean-Architecture-MVVM

https://ios-development.tistory.com/555

https://jeonyeohun.tistory.com/305
