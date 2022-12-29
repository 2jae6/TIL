배경
데이터를 소유한 VC 혹은 VM이 비대해질 수 있다. 또한 이들이 많아지고 DTO(모델)이 변경되었을 경우 연결되어있는 곳에 모두 수정을 해주어야한다.

Domain object 와 Repository 를 분리해야한다.

```swift
protocol Repository {
    associatedtype T
    
    func get(id: Int, completionHandler: (T?, Error?) -> Void)
    func list(completionHandler: ([T]?, Error?) -> Void)
    func add(_ item: T, completionHandler: (Error?) -> Void)
    func delete(_ item: T, completionHandler: (Error?) -> Void)
    func edit(_ item: T, completionHandler: (Error?) -> Void)
}

protocol CombineRepository {
    associatedtype T
    
    func get(id: Int) -> AnyPublisher<T, Error>
    func list() -> AnyPublisher<[T], Error>
    func add(_ item: T) -> AnyPublisher<Void, Error>
    func delete(_ item: T) -> AnyPublisher<Void, Error>
    func edit(_ item: T) -> AnyPublisher<Void, Error>
}
```
레퍼런스
https://devming.medium.com/repository-pattern%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-255731577927
https://blog.devgenius.io/repository-pattern-in-swift-a8eda25b515d
