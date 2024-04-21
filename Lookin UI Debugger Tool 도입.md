## Lookin

### 도입 배경
UI Debugger 로 쓸 수 있는 도구가 필요했었습니다.
디자인 QA 시 Xcode 에서 제공하는 View Debugger 는 현재 화면을 캡처한 상태로 시뮬레이션이 멈추기도하고 느렸습니다. 원래는 flex 와 같이 실제 디바이스에서 디버깅 가능한 도구를 원했으나 활성화된 sdk 들이 많이 없었습니다. 그 중 Lookin 이라는 중국 sdk 를 써보자합니다.


### 설치
https://lookin.work

### SPM 
https://github.com/hughkli/Lookin/
develop branch


### tuist 설정
static framework 로 추가해줘야합니다.
dynamic 설정 시 컴파일 오류가 나는데 추측하기로는 빌드되는 시점에 링킹되어야 캡쳐가 되나봅니다. (원인은 잘모르겠음.)
또한 프레임워크에 존재하는 SHOULD_COMPILE_LOOKIN_SERVER 전처리문이 동작하기 위해서는 아래와 같이
tuist 에서 PackageSettings 설정을 해줘야합니다.

```swift
  targetSettings: [
    "LookinServer" : ["GCC_PREPROCESSOR_DEFINITIONS": "$(inherited) SHOULD_COMPILE_LOOKIN_SERVER=1"],
    "LookinServerSwift" : ["GCC_PREPROCESSOR_DEFINITIONS": "$(inherited) SHOULD_COMPILE_LOOKIN_SERVER=1"],
    "LookinServerBase" : ["GCC_PREPROCESSOR_DEFINITIONS": "$(inherited) SHOULD_COMPILE_LOOKIN_SERVER=1"]
  ]

```



레퍼런스
https://lookin.work
https://github.com/tuist/tuist/issues/6157
