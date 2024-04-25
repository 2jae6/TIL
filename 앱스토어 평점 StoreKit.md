### 앱스토어 평점 유도하는 기능 StoreKit

### 배경
우리 앱은 평점이 2.6으로 매우 낮다. 
앱의 특성상 평점을 잘받기 어렵기도 하지만 그래도 좋은 유저 저니를 경험한 분들에게 별점을 받아보고자한다.

HIG Best Practice 조건
https://developer.apple.com/design/human-interface-guidelines/ratings-and-reviews

1. 충분한 경험을 통해 앱을 사용해본 유저에게 리뷰 받기. 첫 화면 X 
2. 사람들을 괴롭히는 것을 피해라. 반복되는 요청은 짜증나게 할 수 있고, 요청 사이의 간격은 1~2주를 권장  
유저가 게임 중, 혹은 앱의 일 중간에 묻지마라.
3. 시스템에서 제공하는 팝업을 써라. 365일 내 3번 제한이 있음
4.재설정은 자제해라.

https://developer.apple.com/documentation/storekit

StoreKit 
iOS 14 이상
    if let scene = UIApplication.shared.connectedScenes
      .first(where: { $0.activationState == .foregroundActive }) as? UIWindowScene {
      SKStoreReviewController.requestReview(in: scene)
    }
    
이하
SKStoreReviewController.requestReview()




레퍼런스
