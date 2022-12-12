# XcodeGen 에서 Tuist 전환 프로젝트

전환해야겠다고 생각한 이유
1. yml 이 아니라 swift 라서 프로젝트 제너레이트 할 때 오류를 더 잘 잡는 것 같습니다.
2. XcodeGen 도 멀티프로젝트 멀티타겟이 가능하지만 트위스트는 좀 더 쉽게 지원합니다.
3. 클래스 다이어그램을 지원함 (물론 Tuist 안써도 가능함  [swiftAutoDiagram](https://github.com/yoshimkd/swift-auto-diagram) 혹은 [SwiftPlantUML](https://github.com/MarcoEidinger/SwiftPlantUML-Xcode-Extension) )  
4. SPM 을 100% 쓰고 있었는데 동적 라이브러리 링킹 문제가 있어서 모듈별 의존성이 분리가 제대로 이루어지지 않았습니다. Mach-O-Type issues
5. xcodegen generate 할 때마다 spm 캐싱이 되지않아서 방법을 찾아봤는데 못찾겠습니다. 생산성이 너무 떨어지더라구요..


이유는 이정도인 것도 있고 사실 지원하는 기능도 많고 좀 더 잘되어있는 것 같아서 옮기려고 마음을 먹고 있습니다.
걱정되는건 서비스 중인 앱에 적용하는 것이라 되던게 안되는 문제는 없도록 꼼꼼하게 잘 확인하고 고쳐야할 것 같습니다.


겪었던 문제
1. Firebase 라이브러리 의존성 추가 시 다음과 같은 에러
![스크린샷 2022-12-12 오전 9 57 41](https://user-images.githubusercontent.com/47078140/206940174-dec6b3f2-e9fc-4a6d-baa1-f94ecad086bc.png)

해결방안
- 터미널에 `tuist version` 입력
- 터미널에 `tuist update` 입력하여 최신버전으로 업데이트
- 터미널에 `tuist clean`
- 터미널에 `tuist fetch`



레퍼런스

https://docs.tuist.io/guides/adopting-tuist

https://baechukim.tistory.com/98

https://silver-g-0114.tistory.com/150

https://nsios.tistory.com/183

https://okanghoon.medium.com/tuist-%EB%A1%9C-%EC%99%B8%EB%B6%80-%EC%9D%98%EC%A1%B4%EC%84%B1-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0-85609e70133c

https://github.com/choidam/tuist_sample
