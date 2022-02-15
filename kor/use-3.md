# 한국어 모딩 가이드
[[ < 이전 페이지 ]](./use-2.md)
     
## 개요
  
   이 페이지는 모드를 적용하고 사용하는 데 종종 발생하는 문제들과 해결법을 설명합니다.
  
   ### 목차
   
   1. [UnityModManager에 모드를 설치해도 Status에 OK가 뜨지 않습니다](#UnityModManager에-모드를-설치해도-Status에-OK가-뜨지-않습니다)
   1. [모드를 설치하고 게임을 실행하니 모드 적용이 안 되며 메모장이 실행됩니다](#모드를-설치하고-게임을-실행하니-모드-적용이-안-되며-메모장이-실행됩니다)
   1. [이 페이지에 나와 있지 않은 오류](#이-페이지에-나와-있지-않은-오류)
  
-----

## UnityModManager에 모드를 설치해도 Status에 OK가 뜨지 않습니다
  
   대개 UnityModManager가 최신 버전이 아닐 경우 나타나는 문제입니다.

   UnityModManager의 Install 탭에 들어가 `Download X.XX.X`이라 쓰인 초록색 버튼을 눌러 업데이트해 해결할 수 있습니다.

   그리고 Mods 탭에 들어가 모드를 우클릭하고, Install을 눌러 주세요.
   
-----
  
## 모드를 설치하고 게임을 실행하니 모드 적용이 안 되며 메모장이 실행됩니다
  
   얼불춤과 UnityModManager가 서로 충돌할 경우, 모드 적용이 되지 않으며 메모장이 실행됩니다.
  
   ### 메모장 내용 중 `'SetupLevelEventsInfo' not found.`가 포함돼 있다면 
     
   UnityModManager 폴더에 있는 UnityModManagerConfig.xml 파일에 문제가 있는 경우입니다.
     
   * UnityModManagerConfig.xml를 열고, `<GameInfo Name="A Dance of Fire and Ice">` 부분을 찾아 주세요.
   * `<GameInfo Name="A Dance of Fire and Ice">` 안에 있는 `<StartingPoint>`으로 시작하는 줄과 `<UIStartingPoint>`로 시작하는 줄을 지워 주세요.
   * 다음 내용을 복사해서 지운 부분에 붙여 넣어 주세요. 
     ```xml
     <StartingPoint>[Assembly-CSharp.dll]ADOStartup.Startup:Before</StartingPoint>
     <UIStartingPoint>[Assembly-CSharp.dll]ADOStartup.Startup:After</UIStartingPoint>
     ```
   * 그리고 UnityModManager를 껐다 키고, Install 탭에서 Uninstall 버튼을 누르고 연달아 Install 버튼을 눌러 주세요.
   * 이제 얼불춤을 실행하고 오류가 발생하는지 확인해 주세요.
  
   ### 메모장 내용 중 `'ADOStartup' not found.`가 포함돼 있다면
  
   혹시 오랫동안 얼불춤을 업데이트하지 않으셨나요? 얼불춤이 최신 버전이라면 이 오류는 나올 수 없습니다. 얼불춤을 업데이트해 주세요.
   
   ### 이외의 경우
  
   ['이 페이지에 나와 있지 않은 오류' 문단을 참고해서](#이-페이지에-나와-있지-않은-오류) 다른 사람들에게 도움을 요청할 수 있습니다.
  
-----
  
## 이 페이지에 나와 있지 않은 오류
  
  디스코드 서버인 ADOFAI.gg 커뮤니티 서버에서 도움을 요청할 수 있습니다.
  
  * 디스코드 서버인 [ADOFAI.gg 커뮤니티 서버](https://discord.gg/TKdpbUUfUa)에 접속하고(디스코드 계정이 필요합니다), `#규칙` 채널을 정독해서 인증 역할을 얻으세요.
  * `#모드-도움` 채널에서 자신이 처한 상황을 **직설적으로, 할 수 있는 한 최대한 자세히** 말하세요.
    * 문제 원인을 찾기 위해서는 사실 꽤 많은 정보들이 필요합니다. 어떤 과정에서 문제가 생겼는지, 적용된 모드들은 무엇무엇이 있는지 등등을 자세히 말해 주세요.
    * 세상에 모드가 한두 개 있는 게 아닙니다. 모드의 기능이 아니라 모드 이름을 제대로 말해 주세요.
      * ❌ 정확도 띄워 주는 모드
      * ⭕ ProgressDisplayer
