# 한국어 모딩 가이드
<ins>[[ < 이전 페이지 ]](./main.md)</ins> <ins>[[ 다음 페이지 > ]](./dev-2.md)</ins>

## 최소 개발 조건 (참고용)
* [.net framework 4.8](https://go.microsoft.com/fwlink/?linkid=2088517) - (무조건 4.8일 필요는 없으나 개인적으로 추천하는 버전입니다.)
* [UnityModManager](https://www.nexusmods.com/site/mods/21)
* Harmony - UnityModManager와 같이 설치됩니다.
* Unity - 기존 게임 코드에 있는 dll 파일을 Reference에 추가하면 됩니다.

## 개발 환경 만들기

여기서는 [Visual Studio 2019](https://visualstudio.microsoft.com/) IDE를 기준으로 설명합니다. 만약 다른 IDE를 사용중이시라면 추가 Pull Request를 올려주세요.

1. [빈 C# 프로젝트를 생성](https://docs.microsoft.com/en-us/visualstudio/get-started/tutorial-projects-solutions?view=vs-2019)합니다.
2. [필요한 Reference를 추가](https://docs.microsoft.com/en-us/visualstudio/ide/managing-references-in-a-project?view=vs-2019)합니다.
    * UnityModManager/0Harmony.dll
    * UnityModManager/UnityModManager.dll
    * A Dance of Fire and Ice_Data/Managed/Unity*.dll
    * A Dance of Fire and Ice_Data/Managed/Assembly-CSharp.dll
    * A Dance of Fire and Ice_Data/Managed/Assembly-CSharp-firstpass.dll

## 계속 진행하시려면 다음 페이지를 읽어주세요.