1. 파이어베이스 모듈화 

배경
프로젝트에 Firebase SDK를 Tuist 의 SPM 을 이용하여 의존성을 추가하였습니다.
모듈화를 진행하여 ThirdPatyFirebase 라는 모듈을 만들었고 firebase SDK 를 추가하였습니다.
다이나믹 링크로 설정되어있어 다른 모듈을 통해 import 했으나 앱이 실제 동작할 때 crash 가 발생하여서 방법을 찾아보았는나 해결하지 못하여 직접 ThirdPartyModule 의존성을 추가해 해결이 되었습니다.
(요약: 파베 모듈은 다른 모듈 통해서 접근하면 동작이 안됐음..)

해결 방법
firebase 의 xcframework 자체를 프로젝트 내부에 넣고 tuist 에서는 추가한 xcframework 의 경로만 설정해주어 모듈화를 이루어낸다.
앱 내에서 우리가 필요로하는 firebase 내부 모듈은 총 5가지 (FirebaseAnalytics, FirebaseCrashlytics, FirebaseAuth, FirebaseDynamicLinks, FirebaseMessaging) 이며
이 모듈들이 포함하는 xcframework 들을 tuist dependencies 내에 추가해준다.

"""swift
      dependencies: [
        // FirebaseAnalytics
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAnalytics/FBLPromises.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAnalytics/FirebaseAnalytics.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAnalytics/FirebaseAnalyticsSwift.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAnalytics/FirebaseCore.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAnalytics/FirebaseInstallations.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAnalytics/FirebaseCoreInternal.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAnalytics/GoogleAppMeasurement.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAnalytics/GoogleAppMeasurementIdentitySupport.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAnalytics/GoogleUtilities.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAnalytics/nanopb.xcframework")),
        // FirebaseCrashlytics
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseCrashlytics/FirebaseCoreExtension.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseCrashlytics/FirebaseCrashlytics.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseCrashlytics/FirebaseSessions.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseCrashlytics/GoogleDataTransport.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseCrashlytics/PromisesSwift.xcframework")),
        // FirebaseAuth
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAuth/FirebaseAppCheckInterop.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAuth/FirebaseAuth.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAuth/GTMSessionFetcher.xcframework")),
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseAuth/RecaptchaInterop.xcframework")),
        // FirebaseDynamicLinks
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseDynamicLinks/FirebaseDynamicLinks.xcframework")),
        // FirebaseMessaging
        .xcframework(path: .relativeToRoot("Frameworks/Firebase/FirebaseMessaging/FirebaseMessaging.xcframework"))
      ]
"""

