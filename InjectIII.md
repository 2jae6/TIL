### 인젝트 당신은 누구인가?

인젝트는 Hot Reloading 이란 것을 지원하여 다시 컴파일되는 것이 아닌 실행 중 앱에 수정을 반영하는 것입니다. SwiftUI 의 Canvas 에 나타나는 Preview 같은 것입니다. UIKit을 사용하여 앱을 개발하는 개발자들에게 유용할 것 같아서 많은 개발자들이 이용하는 것 같습니다. 저는 몰라서 한번 알아보려구요.

### 준비사항
- 앱스토어에서 InjectionIII 다운로드 
<img width="250" alt="Screenshot 2023-01-07 at 11 11 03 PM" src="https://user-images.githubusercontent.com/47078140/211154963-0a9b3c02-b031-464e-a386-c60cd9e74391.png">
- 라이브러리 https://github.com/krzysztofzablocki/Inject 를 프로젝트에 추가
- Build Settings 에 Other Linker Flags 설정에 "-Xlinker -interposable" 추가

셋팅은 끝났고

이제 Inject.ViewControllerHost 를 이용해서 ViewController 를 띄우면 됩니다.

```swift
let viewController = Inject.ViewControllerHost(ViewController())
rootViewController.pushViewController(viewController, animated: true)
```

스유에서도 가능한데..  왜.. 쓰는지는 모르겠다..



### 겪었던 문제
💉 💉 ⚠️ Your project file seems to be in the Desktop or Documents folder and may prevent InjectionIII working as it has special permissions.
라는 메세지가 떴습니다. 프로젝트가 데스크탑 폴더에 있었거든요

해결방안
https://github.com/johnno1962/InjectionIII/issues/309
그냥 폴더를 다른 곳으로 옮기라는군요...
