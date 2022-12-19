### Property Wrapper

Swift 5.1 에서 추가된 기능입니다.

프로퍼티에서의 중복을 줄여 재사용성을 높이는 용도로 사용합니다.

@가 붙은 어떤 속성을 보신적 적이 있으시겠죠?



`get/set ` 이용 시에 중복되는 것들을 활용 할 수 있게 도와주는 친구입니다.



```swift
@propertyWrapper
struct PlusThree {
  private var value = 0

  var wrappedValue: Int {
    get { value }
    set { value = newValue + 3 }
  }
}

struct TestStruct {
  @PlusThree var number: Int
}

var test = TestStruct()
test.number = 3
print(test.number)
```



특정 숫자에 값을 부여하게 되면 3을 반환하는 예시를 만들어보았습니다.



PlusThreee 구조체를 보시면 wrappedValue 가 있는데 여기 get set 에 구현해주시면 되고 프로퍼티래퍼의 핵심적인 역할의 변수입니다.



### 초기화시 값이 필요하다면?

```swift
@propertyWrapper
struct PlusThree {
  private var value = 0

  var wrappedValue: Int {
    get { value }
    set { value = newValue + 3 }
  }

  init(wrappedValue initialValue: Int) {
      self.wrappedValue = initialValue
  }
}

struct TestStruct {
  @PlusThree var number: Int
}

var test = TestStruct(number: 4)
print(test.number)
```



init 을 추가해주면됩니다.

주의 할 점은 wrappedValue 가 지금은 하나지만 여러개일 때도 맨 앞에 와야한다는점입니다.



### `_`Syntax 

변수 앞에 `_` 언더바를 붙임으로써 wrapper type에 접근할 수 있습니다.



```swift
@propertyWrapper
struct PlusThree {
  var value = 0

  var wrappedValue: Int {
    get { value }
    set { value = newValue + 3 }
  }

  init(wrappedValue initialValue: Int) {
      self.wrappedValue = initialValue
  }

  func talk() {
    print("말하기")
  }
}

struct TestStruct {
  @PlusThree var number: Int

  func testFunction() {
    _number.talk()
  }
}
```





### '$' Syntax

```swift
@propertyWrapper
struct PlusThree {
  var value = 0

  var wrappedValue: Int {
    get { value }
    set { value = newValue + 3 }
  }

  init(wrappedValue initialValue: Int) {
      self.wrappedValue = initialValue
  }

  func talk() {
    print("말하기")
  }
}

struct TestStruct {
  @PlusThree var number: Int
}

var test = TestStruct(number: 4)
print(test._number.talk())
```

이 코드를 돌려보면 '_number' is inaccessible due to 'private' protection level 라는 에러가 뜬다.

바깥에서 랩퍼를 부르면 private acceess level 이기 때문이다.



이를 해결하는 방법이 projection '$' 를 이용한 방법이다.

```swift
@propertyWrapper
struct PlusThree {
  var value = 0

  var wrappedValue: Int {
    get { value }
    set { value = newValue + 3 }
  }

  var projectedValue: PlusThree { return self }

  init(wrappedValue initialValue: Int) {
      self.wrappedValue = initialValue
  }

  func talk() {
    print("말하기")
  }
}

struct TestStruct {
  @PlusThree var number: Int
}

var test = TestStruct(number: 4)
test.$number.talk()
```







### 레퍼런스

https://value-of-life.tistory.com/157

https://zeddios.tistory.com/1221

https://wlaxhrl.tistory.com/90

https://minsone.github.io/programming/fixed-not-exist-key-of-response-using-propertywrapper

