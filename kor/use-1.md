# 한국어 모딩 가이드
<ins>[[ < 이전 페이지 ]](./main.md)</ins> <ins>[[ 다음 페이지 > ]](./2.md)</ins>

## UnityModManager 설치 방법

### UnityModManager 다운로드하기

1. `UnityModManager` 설치 링크: https://www.nexusmods.com/site/mods/21
    * 링크를 타고 들어간 후 맨 오른쪽 위 버튼에서 계정을 생성한 후 로그인 하세요.
    * 로그인 후 `Download:` 텍스트 옆 `Manual` 버튼을 클릭하세요.
    * `Slow Download` 버튼을 클릭하세요.
2. 다운받은 `UnityModManager.zip` 파일을 압축 해제하세요.
3. 필요한 경우 자신의 게임 버전에 맞게 `UnityModManagerConfig.xml` 파일을 수정하시고, `UnityModManager.exe` 파일을 실행하세요.
    * 지금 만약 당신이 정식 버전을 사용하신다면 무조건 수정하셔야 합니다. [혹은 이미 여기서 수정된 파일을 다운로드할 수 있습니다.](https://drive.google.com/file/d/1BZ6XJwMnb9KsKtLcuQ5JctRs81nw_60V/view?usp=sharing)
    * 만약 직접 수정하고 싶으시다면 밑의 추가 정보 - 파일 수정 항목을 참조하시길 바랍니다.
4. `UnityModManager`를 설정해 주세요.
    * `Install` 탭을 클릭하세요.
    * `Game` 텍스트 옆에 있는 드롭다운을 클릭하시고 `A Dance of Fire and Ice`를 선택하세요. (다른 게임일 경우 다른 게임의 이름을 선택하시면 됩니다.)
    * `Folder` 텍스트 옆에 있는 버튼을 클릭하시고 얼불춤 exe 파일이 있는 폴더(되도록이면 스팀 폴더)를 선택해 주세요. 폴더를 선택하고 OK를 누르시면 됩니다.
    * `Installation Method` 그룹 이내에서 `Assembly`를 선택해주세요.
    * `Install` 버튼을 누르신 후 얼불춤을 실행하시고 메모장에 오류가 뜨는지 확인해보세요. 오류가 뜬다면 뭔가 잘못 설정한게 있는지 확인해주세요. 만약 관련해 도움이 필요하다면 언제든지 [모딩 커뮤니티 디스코드](https://discord.gg/AGFXhCfyE5)를 참여해 도움을 받을 수 있습니다.
    * 글로 이해가 어려우시다면 아래 사진을 참고해보세요. <color style="color: #f00">빨강</color> → <color style="color: #00f">파랑</color> → <color style="color: #090">초록</color> 순입니다.
    ![](../resources/use-1/image1.png)

<!-- Additonal Info -->
### 추가 정보
#### 파일 수정

**사례 1:**
2021년 2월 25일 기준 베타 버전(`1.11.3 r70`) 과 정식 버전(`1.11.1 r68`)의 게임 코드가 달라서 파일을 수정해야 하는 경우가 있습니다.

우선 수정해야 할 대상은 `UnityModManagerConfig.xml` 파일입니다.
```xml
<GameInfo Name="A Dance of Fire and Ice">

...

</GameInfo>
```

이 내용이 있는 라인을 찾고 안에 있는 `StartingPoint`, `UIStartingPoint`를 다음과 같이 수정해야 합니다.

게임 버전 `r68`까지는 설정을 다음과 같이 적용해야 합니다.

```xml
<StartingPoint>[Assembly-CSharp.dll]ADOBase.SetupLevelEventsInfo:Before</StartingPoint>
<UIStartingPoint>[Assembly-CSharp.dll]ADOBase.SetupLevelEventsInfo:After</UIStartingPoint>
```

버전 `r70`부터는 설정을 다음과 같이 적용해야 합니다. (이게 기본값이므로 `r70` 및 그 이후 버전을 사용하시는 분들은 설정을 바꾸지 않아도 될겁니다.)

```xml
<StartingPoint>[Assembly-CSharp.dll]ADOStartup.Startup:Before</StartingPoint>
<UIStartingPoint>[Assembly-CSharp.dll]ADOStartup.Startup:After</UIStartingPoint>
```

만약 설정이 끝났다면 이렇게 보일 것입니다. 밑의 `여러분이 설정한 내용..` 은 실질적으로 들어가는 값이 아니라 위에 보여준 두개의 설정 중 하나입니다.
```xml
<GameInfo Name="A Dance of Fire and Ice">
    <Folder>ADOFAI</Folder>
    <ModsDirectory>Mods</ModsDirectory>
    <ModInfo>Info.json</ModInfo>
    <GameExe>A Dance of Fire and Ice.exe</GameExe>
    <EntryPoint>[UnityEngine.UIModule.dll]UnityEngine.Canvas.cctor:Before</EntryPoint>
    <StartingPoint> 여러분이 설정한 내용.. </StartingPoint>
    <UIStartingPoint> 여러분이 설정한 내용.. </UIStartingPoint>
    <MinimalManagerVersion>0.22.14</MinimalManagerVersion>
    <Comment>Required minimum game version 1.11.3</Comment>
</GameInfo> 
```

만약 이 프로그램이 어떻게 작동하는지 정확히 알지 못하신다면, **절대 주석 안에 설정을 쓰지 않도록 주의하십시오.**

**사례 2:**
UnityModManager에 등록된 게임이 아니라서 본인이 직접 게임을 등록해야 하는 경우가 있습니다.

이런 경우엔 다른 게임의 등록된 데이터를 복제하고 게임에 맞춰서 값을 다르게 하면 됩니다.

## 계속 진행하시려면 다음 페이지를 읽어주세요.