### ResultBuilder

- Swift 5.4 도입
- 여러 표현식을 단일 값으로 결합하여 결과를 빌드
- ex) return 생략, 콤마 생략 등


결합하여 결과를 빌드와 return 생략 예시
  
```swift
@TestBuilder
func testFunction() -> [Test] {
  Test()
  Test()
  Test()
}
```


@resultBuilder 를 사용함녀 statkc func buildBlock 을 강제로 재정의 해야함
```swift
@resultBuilder
struct TestBuilder {
  static func buildBlock(_ components: Test...) -> [Test] {
    components.map { Test() }
  }
}​

```

이를 사용하면 return 키워드를 사용하지 않아도 리턴임을 암시 할 수 있음


