# XcodeGen 에서 Tuist 전환 프로젝트

전환해야겠다고 생각한 이유

1. yml 이 아니라 swift 라서 문법적인 오류도 잘 잡아내고 프로젝트 제너레이트 할 때 오류를 훨씬 더 잘 잡는 것 같습니다. 또한 Swift 로 되어있어 iOS 개발자들에게 친숙하구요.  yml보단 훨씬 편하네요.
2. XcodeGen 도 멀티프로젝트 멀티타겟이 가능하지만 트위스트는 좀 더 쉽게 지원합니다.
3. 클래스 다이어그램을 지원함 (물론 Tuist 안써도 가능함  [swiftAutoDiagram](https://github.com/yoshimkd/swift-auto-diagram) 혹은 [SwiftPlantUML](https://github.com/MarcoEidinger/SwiftPlantUML-Xcode-Extension) )  
4. SPM 을 100% 쓰고 있었는데 동적 라이브러리 링킹 문제가 있어서 모듈별 의존성이 분리가 제대로 이루어지지 않았습니다. Mach-O-Type issues
5. xcodegen generate 할 때마다 spm 캐싱이 되지않아서 방법을 찾아봤는데 못찾겠습니다. 생산성이 너무 떨어지더라구요..


이유는 이정도인 것도 있고 사실 지원하는 기능도 많고 좀 더 잘되어있는 것 같아서 옮기려고 마음을 먹고 있습니다.
걱정되는건 서비스 중인 앱에 적용하는 것이라 되던게 안되는 문제는 없도록 꼼꼼하게 잘 확인하고 고쳐야할 것 같습니다.

썼던 명령어

```shell
tuist edit # 트위스트 프로젝트 코드 짤 때 실행
tuist clean # 간혹 에러발생하거나 할 때 써쭤야합니다. keyNotFound 같은.
tuist fetch # Dependency 관련된 수정 사항은 fetch 를 꼭 해줘야합니다.
tuist generate # workSpace 나 project 만드는 명령어입니다.
tuist generate --project-only # 프로젝트만 재생성하는 명령어입니다.
```

전환 이유 4번은 Tuist 기능 중 productType 으로 해결하였습니다.

### Tuist 전환 후 느낀점이나 후기

전환하고서 좋았던점은 일단 엑코젠은 원프로젝트 멀티 타겟으로 했었는데 (리액티브빼고)
멀티프로젝트로 모듈들이 바뀌면서 좀 더 관리하기가 쉬워졌다고 느껴졌어요. 원하는 것들끼리 데모앱도 만들 수 있고 의존성 그래프도 볼 수 있으니까요. 

그리고 generate 시 Dependency 들이 캐싱되어있는게 너어어어어무 만족스러워요.

만약 본인 팀이 spm을 쓰는데 XcodeGen을 쓰려고한다?... 저는 말리고싶다는 의견입니다.

음 또 좋은점은 저희 프로젝트는 뭐가 문제였는지 모르겠지만 새로운 파일이 추가되면 의존성 트리가 뭉게지면서 다른 타겟 header을 찾을 수 없다나 뭐라나 .. 

그래서 추가하고 다시 generate 하는 그런 문제들이 있었는데 말끔히 살아져서 너무 좋고요...

트위스트나 엑코젠이나 기능들이 드라마틱하게 다르지는 않아서 체감하기가 어렵긴 하지만 확실히 관리하기도 편하고 구조도 더 깔끔하다고 생각이 들었습니다.

무엇보다 배포하고나서 계획했던 

https://lazyowl.tistory.com/entry/%ED%9A%8C%EA%B3%A0-%EB%A6%AC%EB%93%9C%EC%9D%98-%EC%B2%AB%EC%8B%9C%EC%9E%91%EB%B6%80%ED%84%B0-%EC%B2%AB-%EB%B0%B0%ED%8F%AC%EA%B9%8C%EC%A7%80%EC%9D%98-%EC%97%AC%EC%A0%95

마일스톤들을 많이 지킨 것 같아서 뿌듯하구요.



### 겪었던 문제

### Firebase 라이브러리 의존성 추가 시 다음과 같은 에러

![스크린샷 2022-12-12 오전 9 57 41](https://user-images.githubusercontent.com/47078140/206940174-dec6b3f2-e9fc-4a6d-baa1-f94ecad086bc.png)

해결방안

- 터미널에 `tuist version` 입력

- 터미널에 `tuist update` 입력하여 최신버전으로 업데이트

- 터미널에 `tuist clean`

- 터미널에 `tuist fetch`

  

### Crashlytics Dsym upload 설정

앱을 실행하면 크래시틱스를 실행하려고 Build Phase 에 Script 를 넣어주는 부분이 있는데 기존 SPM 은 Build_DIR (DerivendData 있는 곳)에 넣어두는데 트위스트는 별도로 트위스트 디렉터리에 외부라이브러리를 캐싱해둔다. 

그래서 `"${BUILD_DIR%Build/*}SourcePackages/checkouts/firebase-ios-sdk/Crashlytics/run"` 를
`../../Tuist/Dependencies/SwiftPackageManager/.build/checkouts/firebase-ios-sdk/Crashlytics/run`
로 변경해주면된다. (../은 pwd 찍어서 잘해주시면 됩니다.)

### Xcode Cloud Clone Post Script 설정

Tuist 를 XcodeCloud 에서 돌리려면 ci_script 가 필요하다.

안타깝게도 XcodeCloud 는 Tuist 설치를 지원하지 않아서 로컬에서 직접 올려줘야한다.
https://wojciechkulik.pl/xcode/xcode-cloud-overview-and-setup
사이트에 조금 내려보면 Tuist 와 관련된 내용이 있다.
tuist bundle 명령어를 입력하고 추가된 .tuist-bin 파일들을 모두 리모트에 업로드해주면 됩니다.
그러고 XcodeCloud ci_post_clone.sh 파일에

```swift
cd ..
.tuist-bin/tuist fetch
.tuist-bin/tuist generate
```

추가해주면 됩니다.

아그리고 tuist bundle 입력 시  

`error io.tuist.support : [TuistSupport] Couldn't find a .tuist-version file in the directory`
뜨신다면 `tuist local` 입력 후 나타나는 버전을
`tuist local 3.14.0`
`tuist bundle` 입력해주시면됩니다.
( https://docs.tuist.io/guides/version-management/#bundle 공식문서 첨부할게요 )



레퍼런스

https://docs.tuist.io/guides/adopting-tuist

https://baechukim.tistory.com/98

https://silver-g-0114.tistory.com/150

https://nsios.tistory.com/183

https://okanghoon.medium.com/tuist-%EB%A1%9C-%EC%99%B8%EB%B6%80-%EC%9D%98%EC%A1%B4%EC%84%B1-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0-85609e70133c

https://github.com/choidam/tuist_sample
