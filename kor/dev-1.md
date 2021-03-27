# 한국어 모딩 가이드
<ins>[[ < 이전 페이지 ]](./main.md)</ins> <ins>[[ 다음 페이지 > ]](./dev-2.md)</ins>

## 최소 개발 조건 (참고용)
* [.NET Framework 4.8](https://go.microsoft.com/fwlink/?linkid=2088517) - (무조건 4.8일 필요는 없으나 개인적으로 추천하는 버전입니다.)
* [UnityModManager](https://www.nexusmods.com/site/mods/21)
* Harmony - UnityModManager와 같이 설치됩니다.
* Unity - 기존 게임 코드에 있는 dll 파일을 Reference에 추가하면 됩니다.

## 개발 환경 만들기

여기서는 [Visual Studio 2019](https://visualstudio.microsoft.com/) IDE를 기준으로 설명합니다. 만약 다른 IDE를 사용중이고 내용을 추가해 주실 의향이 있으시면 Pull Request를 올려주시면 감사하겠습니다.

### Visual Studio 2019

1. [클래스 라이브러리 C# 프로젝트를 생성](https://docs.microsoft.com/en-us/dotnet/core/tutorials/library-with-visual-studio)합니다.
2. [필요한 Reference를 추가](https://docs.microsoft.com/en-us/visualstudio/ide/managing-references-in-a-project?view=vs-2019)합니다.
    * UnityModManager/0Harmony.dll
    * UnityModManager/UnityModManager.dll
    * A Dance of Fire and Ice_Data/Managed/Unity*.dll
    * A Dance of Fire and Ice_Data/Managed/Assembly-CSharp.dll
    * A Dance of Fire and Ice_Data/Managed/Assembly-CSharp-firstpass.dll
3. Info.json 파일을 생성하고 모드의 정보를 채워넣습니다.
    * 관련된 정보는 [이 사이트](https://wiki.nexusmods.com/index.php/How_to_create_mod_for_unity_game)에서 찾을 수 있습니다.

---

## [이 곳을 클릭하면 다음 페이지로 넘어갑니다.](./dev-2.md)