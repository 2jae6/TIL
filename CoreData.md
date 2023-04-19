### CoreData

코어데이터는 Database 가 아닌 데이터 저장에 관한 프레임워크입니다. 디바이스에 영구적인 데이터를 저장 할 수 있고 UserDefault 가 간단한 정보를 저장한다면 CoreData 는 좀 더 복잡한 데이터를 저장하기에 적합합니다.
결론적으로 CoreData 는 앱의 모델 계층이며 객체 그래프를 관리하는 프레임워크입니다.
DB 같은 기능은 Core Data 의 Persistence 이니까 DB는 아니고 좀 더 넓은 의미라고 생각해야합니다.


1. Class Definition 
Core Data 가 알아서 managed object subclass 를 알아서 만들어서 프로퍼티 또는 기능을 편집할 필요가 없음

2. Manual/None
메소드, 비즈니스 로직을 추가하기위한 용도



코어데이터를 사용할 순서
1. 인스턴스 생성
2. 저장
2-1. NSManagedObjectContext를 가져오기 
2-2. Entity를 가져오기
2-3. NSManagedObject를 만든다.
2-4. NSManagedObject에 값을 세팅
2-5. NSManagedObjectContext를 저장

3. Core 저장한 내용 불러오기


/var/folders/hh/3gxtgs052_vg64l129212gsw0000gn/T/TemporaryItems/NSIRD_screencaptureui_iqekKK/스크린샷 2023-04-12 오전 10.13.42.png