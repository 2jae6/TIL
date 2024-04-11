#Hitch

프레임이 스크린에 늦게 나타나는 시간
-> 다음 프레임의 생성이 늦어져 애니메이션이 끊기는 시간

원인은 Render Loop 제 시간에 완성시키지 못함


# Render Loop
렌더 루프란 앱의 생명 주기 중 사용자가 이벤트를 발생시키고 그에 따른 처리와 뷰의 변화가 운영체제로 전달되어 화면에 비추는 과정을 말합니다.

렌더 루프는 기기의 refresh rate 시점마다 실행이 됩니다.

## 렌더루프 3가지
### APP
이벤트 처리 후 UI에 생기는 변화 (VSync 전까지 완료되어야함) 

### RenderServer
실제로 UI 가 렌더되는 단계 (VSync 전까지 완료되어야함)

### On the display
완성된 새로운 프레임이 화면에 표시 

5가지는
1. Event (App) : 앱이 터치 이벤트를 처리하고 뷰를 변화 시킬지 결정 단계
2. Commit (App) : 앱이 뷰를 업데이트하고 업데이트 한 뷰를 렌더링해달라고 렌더 서버에게 제출
3. Render prepare (Render Prepare) : 렌더 서버는 뷰싱크에 제출본을 받아 새로운 뷰를 지피유에서 그릴 준비함
4. Render execute (Render Server) : 지피유는 뷰를 그림
5. Display (Display) : 뷰싱크 사용자에게 최종 프레임이 보여짐


# refresh rate 

refresh rate 가 60Hz 라면 1초에 60장의 프레임이 표시
1초 / 60 = 16.67ms 마다 프레임이 교체됩니다.

VSYNC 라는 이벤트를 프레임이 교체될 때 하드웨어가 방출하게 되는데
이 마감기한까지 맞추지 못하면 hitch가 발생합니다.
(버벅임, 렉)


-> Refresh rate 에 맞춰 frame 이 교체되고 그 시점을 VSync(뷰싱크) 라는 이벤트를 내보내고 이 기한보다 늦으면 hitch가 발생합니다.
파이프 라인은 모두 병렬적으로 실행됩니다.



힛치는 두가지 타입이 있습니다.
1. Commit hitch : 앱 프로세스에서 commit 시점에 오래걸려서 발생
2. Render hitch : 렌더 서버에서 제 시간 내 렌더링 오래 걸려서 발생



레퍼런스
https://velog.io/@yeahg_dev/UIAnimation-Hitch와-Render-Loop에-대해-알아보자


