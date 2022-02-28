# 한국어 모딩 가이드 <!-- omit in toc -->

[[ < 이전 페이지 ]](./main.md) [[ 다음 페이지 > ]](./dev-2.md)

- [모드 구상](#모드-구상)
- [모드 개발을 위해 필요한 것들 (참고용)](#모드-개발을-위해-필요한-것들-참고용)
  - [선택 사항](#선택-사항)
- [개발 환경 구축](#개발-환경-구축)
  - [Visual Studio 2019을 사용해 개발 환경 구축](#visual-studio-2019을-사용해-개발-환경-구축)
  - [Info.json](#infojson)
    - [템플릿](#템플릿)

---

## 모드 구상

어느 모드를 만들지 이미 생각하고 있어도, 이 문단을 읽어주시길 바랍니다. 만약 만들고자 하는 모드가 아래 항목에 하나라도 부합한다면, 그 모드는 제작하지 않는 것이 좋을 것입니다.

 - 치트 등 불공정한 이득을 취할 수 있는 모드. 특히 다음같은 모드가 해당됩니다
   - 점수를 위조하는 모드
   - 일시 정지 후 계속했을 때 카운트다운이 나타나는 모드
   - 카운트다운 속도나 횟수에 관여하는 모드
 - 이미 제작된, 제작 중인 모드
   - 이 경우, 모드가 오픈 소스로 출시됐다면, 기여하는 방법을 택할 수 있습니다.

## 모드 개발을 위해 필요한 것들 (참고용)

* 사전 지식 - C#를 사용하는 법을 알고 있는 게 좋습니다.
* [.NET Framework 4.8](https://go.microsoft.com/fwlink/?linkid=2088517) - (4.8 버전이 권장됩니다.)
* [UnityModManager](https://www.nexusmods.com/site/mods/21)
* Harmony - UnityModManager와 같이 설치됩니다.
* Unity - 기존 게임 코드에 있는 dll 파일을 Reference에 추가하면 됩니다.

### 선택 사항

* 앞으로 [ADOFAI.gg 커뮤니티](https://discord.gg/TKdpbUUfUa)에 대해 언급하는 내용이 있으니, 미리 가입해 두는 것을 권장 드립니다.

## 개발 환경 구축

### Visual Studio 2019을 사용해 개발 환경 구축

Visual Studio 2019는 [이곳을 눌러](https://visualstudio.microsoft.com/) 설치할 수 있습니다.

1. [클래스 라이브러리 C# 프로젝트를 생성](https://docs.microsoft.com/en-us/dotnet/core/tutorials/library-with-visual-studio)합니다.
2. [필요한 Reference를 추가](https://docs.microsoft.com/en-us/visualstudio/ide/managing-references-in-a-project?view=vs-2019)합니다.
    * `UnityModManager/0Harmony.dll`
    * `UnityModManager/UnityModManager.dll`
    * `A Dance of Fire and Ice_Data/Managed/Unity*.dll` (모드가 필요로 하는 유니티 모듈들을 추가하세요.)
    * `A Dance of Fire and Ice_Data/Managed/Assembly-CSharp.dll`
    * `A Dance of Fire and Ice_Data/Managed/Assembly-CSharp-firstpass.dll`
3. [Info.json 파일](#infojson)을 생성하고 모드의 정보를 채워 넣습니다.

### Info.json
Info.json 안에는 아래의 내용이 들어갑니다.
 
|       키       	| 설명                                                          	|    값 타입   	| 비고                                            	|
|:--------------:	|---------------------------------------------------------------	|:------------:	|-------------------------------------------------	|
| **Id**             	| 모드의 아이디입니다.                                          	| String       	| **필수**. 폴더 이름과 같게 하는 게 좋습니다.        	|
| DisplayName    	| 표시될 모드의 이름입니다.                                     	| String       	| 선택.                                           	|
| Author         	| 모드 제작자의 이름입니다.                                     	| String       	| 선택.                                           	|
| **Version**        	| 이 모드의 버전입니다.                                         	| String       	| **필수**. 형식은 x.x.x                            	|
| **ManagerVersion** 	| 이 모드가 요구하는 UnityModManager의 최소 버전입니다.         	| String       	| **권장**. 형식은 x.x.x                            	|
| GameVersion    	| 이 모드가 요구하는 A Dance of Fire and Ice의 최소 버전입니다. 	| String       	| 선택. 형식은 x.x.x                            	|
| Requirements   	| 이 모드가 요구하는 다른 모드의 목록입니다.                    	| List[String] 	| 선택.                                           	|
| LoadAfter      	| 이 모드보다 먼저 로드될 모드의 목록입니다.                    	| List[String] 	| 선택.                                           	|
| AssemblyName   	| 만들고 있는 모드의 파일(dll) 이름입니다.                      	| String       	| 선택.                                           	|
| **EntryMethod**    	| 게임 실행 시 UnityModManager가 호출할 메소드입니다.             	| String       	| **필수**. 형식은 `폴더명.파일명.메서드명`입니다. 예시: "ExampleMod.Main.Load".             	|
| HomePage       	| 모드의 홈 페이지(Github 등) 링크입니다.                       	| String       	| 선택.                                           	|
| Repository     	| 이 링크로 업데이트를 확인합니다. 추후 설명하니 비워두어도 됩니다.   | String       	| 선택. json이 Raw로 드러나 있는 링크여야 합니다. 	|

* 위 정보는 [이 사이트](https://wiki.nexusmods.com/index.php/How_to_create_mod_for_unity_game)의 내용을 번역해 수정한 것입니다.

#### 템플릿
```json
{
 "Id": "ExampleMod",
 "DisplayName": "Example Mod",
 "Author": "Your Name",
 "Version": "1.0.0",
 "EntryMethod": "ExampleMod.Main.Load"
}
```

---

## [이곳을 클릭하면 다음 페이지로 넘어갑니다.](./dev-2.md) <!-- omit in toc -->