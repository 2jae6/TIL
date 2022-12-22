### 배경
Firebase 를 모듈로 분리하던 중 `Undefined Symbol` 에러를 만났다.
Carthage 로 Firebase 를 사용하는 방법에 보면 Other Link Flag 에 `$(OTHER_LDFLAGS) -ObjC` 를 추가하라는 내용이있다.

https://github.com/firebase/firebase-ios-sdk/blob/master/Carthage.md

추가해서 했는데 옵씨 라이브러리들에 링킹해줄 수 있게 도와주는 플래그다는건 알겠습니다. 저 속성이 Build Setting에서 어떤 역할을 하는지 잘 정리해주신 포스트가 있더라구요

저도 함께 알아보겠습니다.

### Other Link Flag 너 누구야???
Objective-C 언어로 개발된 framework 를 사용할 때 발생하는 문제를 해결하기위함이다.

Dynamic 한 프레임워크는 메서드가 호출되기전까지는 Symbol로만 표시해두고 Runtime 에 직접적으로 실행할 코드가 결정됩니다. 거기서 Objective-C는 클래스의 심볼은 있으나 메서드를 위한 심볼은 없다. 

ObjC라는 Linker Flag는 링커가 static library에 있는 모든 Objective-C로 작성된 class와 category를 load
할 수 있게 도와주는 것이다.
그래서 파이어베이스는 Static library 이기도하고 오브젝티브씨에 Static library 로 설정되어있다면 추가해주어어야한다.

 static library에서만 발생하는 문제인 만큼 Mach-O Type을 Dynamic Library로 변경하면 -ObjC Flag를 추가하지 않아도 문제가 해결된다. 





### 레퍼런스
https://syjdev.tistory.com/27
https://developer.apple.com/library/archive/qa/qa1490/_index.html

 

