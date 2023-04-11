### @available (*, unavailable)

@available	은 특정 플랫폼, Swift Version, OS vesion 등의 조건을 활용할 때 사용한다. 

@available 은 컴파일 타임에 동작한다.

@available (*, unavailable) 를 사용하는 이유는 코드로 UI 를 작성하는 경우 xib를 사용하지않습니다.

코드로 UI 작성 후 해당 init 을 사용하면 runtime Error 가 발생하는데 @available (*, unavailable) 를 사용하게되면
컴파일타임에 에러가 나기때문에 미리 안전한 코드를 작성할 수 있습니다.

 