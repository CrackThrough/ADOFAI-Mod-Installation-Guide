# 한국어 모딩 가이드 <!-- omit in toc -->

[[ < 이전 페이지 ]](./dev-1.md) [[ 다음 페이지 > ]](./dev-3.md)

- [이용자 배려](#이용자-배려)
  - [독해, 가독성 문제 최소화](#독해-가독성-문제-최소화)
  - [접근성](#접근성)
- [모드의 기본적인 틀 구축](#모드의-기본적인-틀-구축)
  - [UnityModManager.ModEntry 세부 사항](#unitymodmanagermodentry-세부-사항)
- [빌드와 모드 적용 및 실행](#빌드와-모드-적용-및-실행)

<details>
<summary>이 페이지는 아직 완성되지 않았습니다. 펼쳐서 현재 문서에서 다룰 내용과 링크를 확인할 수 있습니다.</summary>

<ul>
    <li>유니티 모드 만들기 튜토리얼: <a href="https://wiki.nexusmods.com/index.php/How_to_create_mod_for_unity_game">
    https://wiki.nexusmods.com/index.php/How_to_create_mod_for_unity_game</a>
    <ul>
        <li>모드를 만들 때 클래스들의 형태 및 필수 조건 등을 설명하면서 Reflection을 이용해 더 깔끔하게 정리하면 특정 기능을 중점으로 한 프로그래밍이 가능함을 설명.</li>
        <li>Reflection 및 Attribute에 대한 소개 또한 포함.</li>
        <li>+) 독자의 Unity 엔진 자체에 대한 이해도가 중요함. Unity 엔진이 작동하는 방식, 게임의 파일 구조등을 모르면 모딩이 쉽지 않을 가능성이 상당히 높음.</li>
    </ul>
    </li>
    <li>커스텀 Asset 추가: <a href="https://docs.unity3d.com/ru/2021.1/Manual/AssetBundlesIntro.html">https://docs.unity3d.com/ru/2021.1/Manual/AssetBundlesIntro.html</a>
    <ul>
        <li>만약 게임 내에 없는 특정 텍스처를 모드가 필요로 할 일이 생겼을 때 위 문서를 참조해 에셋을 모드 단위로 추가할 수 있는 방법 소개.</li>
    </ul>
    </li>
    <li>커스텀 GUI: <a href="https://docs.unity3d.com/Manual/GUIScriptingGuide.html">https://docs.unity3d.com/Manual/GUIScriptingGuide.html</a>
    <ul>
        <li>유니티 내에서 GUI를 쉽게 만드는 방법을 소개하고 간단한 모드 설정 GUI를 만드는 방법 소개.</li>
    </ul>
    </li>
    <li>Harmony 패치: <a href="https://harmony.pardeike.net/articles/intro.html">https://harmony.pardeike.net/articles/intro.html</a>
        <ul>
        <li>Harmony를 이용해 게임 내에 있는 어셈블리의 메서드를 패치하는 방법 소개.</li>
        <li>패치의 원리에 대한 설명 또한 포함.</li>
        </ul>
    </li>
    <li>C# Reflection: <a href="https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/reflection">
    https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/reflection</a></li>
    <li>dnSpy: <a href="https://github.com/dnSpy/dnSpy">https://github.com/dnSpy/dnSpy</a>
        <ul>
        <li>프로그램을 이용해 게임의 코드를 읽는 방법 소개.</li>
        </ul>
    </li>
    <li>UnityAssetBundleExtractor (UABE): <a href="https://github.com/DerPopo/UABE">https://github.com/DerPopo/UABE</a>
        <ul>
        <li>필요한 경우 유니티의 Asset을 뜯고 특정 리소스를 사용하는 방법 소개.</li>
        </ul>
    </li>
    <li>GitHub 등으로 출시된 오픈 소스 (모드)를 참고할 때 오픈 소스의 라이선스를 준수하도록 설명.</li>
</ul>

</details>

---

## 이용자 배려

모드를 이용하는 사람들을 배려하며 모드를 설계하는 것은 바람직한 일입니다. 모드를 제작하기 전에, 이용자를 배려할 수 있는 방법을 알아 봅시다.

**(참고) 아래 내용을 전부 준수해야 모드를 출시할 수 있는 것은 아닙니다.**

### 독해, 가독성 문제 최소화

- 생소한 단어 사용을 최소화하고, 사용한다면 설명을 덧붙이세요.
  - 개발 용어는 지양하고, 사람들이 알기 쉬운 용어를 사용하세요. (ex. 스프라이트 → 사진, 콘텐츠)
- 되도록 공식 용어를 사용하세요.

### 접근성

- 광과민성 발작을 일으킬 수 있는 콘텐츠는 표시 이전에 경고하거나, 표시 버튼 등의 상호 작용을 통해서만 표시될 수 있도록 하세요.

## 모드의 기본적인 틀 구축

프로젝트를 생성할 때 같이 생긴 `Class1.cs`에 코드를 작성하겠습니다. 원한다면 알아보기 쉽게 이름을 바꿀 수도 있습니다.

```cs
using System.Reflection;
using UnityModManagerNet;
using HarmonyLib;

namespace ExampleMod
{
    static class Main
    {
        public static UnityModManager.ModEntry.ModLogger Logger;
        public static Harmony harmony;
        public static bool IsEnabled;

        static bool Load(UnityModManager.ModEntry modEntry)
        {
            // 이 메서드는 게임 실행 시 UnityModManager가 호출할 함수입니다.
            // Info.json의 EntryMethod 값을 바꾸어 다른 메서드가 호출되게 설정할 수 있습니다.

            Logger = modEntry.Logger;
            modEntry.OnToggle = OnToggle;

            harmony = new Harmony(modEntry.Info.Id);

            return true;
            // 반환된 값이 false라면 UnityModManager가 사용자에게 모드가 정상적으로 로드되지 않았다고 표시합니다.
            // 굳이 필요없다고 느껴지면 삭제하고 반환 값을 void로 바꾸어도 됩니다.
        }

        // 이 메서드는 모드를 켜거나 끌 때 호출됩니다. 이 메서드가 없으면 모드를 켜거나 끌 때 마다 게임을 재시작해야 합니다.
        // value 파라미터에는 모드가 켜졌는지(true) 꺼졌는지(false)가 인자로 들어갑니다.
        static bool OnToggle(UnityModManager.ModEntry modEntry, bool value)
        {
            IsEnabled = value;

            if (value)
            {
                // 모드가 켜질 때 아래 코드를 실행합니다.
                harmony.PatchAll(Assembly.GetExecutingAssembly());
            }
            else
            {
                // 모드가 꺼질 때 아래 코드를 실행합니다.
                harmony.UnpatchAll(modEntry.Info.Id);
            }
            
            return true;
            // 반환된 값이 true라면, 모드 상태를 전환합니다. false라면 전환하지 않습니다.
        }
    }
}
```

위 코드에서 modEntry 파라미터에는 [모드에 대한 데이터](#unitymodmanagermodentry-세부-사항)가 인자로 들어갑니다.

harmony에 대한 내용은 추후 다루겠습니다.

### UnityModManager.ModEntry 세부 사항

| Name            	| Description                                                                                                                  	|
|---------------	|-------------------------------------------------------------------------------------------------------------------------------	|
| Info          	| Info.json의 내용입니다.                                                                                                       	|
| Path          	| 모드가 있는 경로입니다. 예를 들어, "Steam\steamapps\common\A Dance of Fire and Ice\Mods\ExampleMod\"같은 형식으로 나옵니다.     	|
| Active        	| 모드가 활성화 됐는지 여부입니다.                                                                                              	|
| Logger        	| Log.txt 파일에 로그를 쓰는 함수입니다.                                                                                         	|
| OnToggle      	| 모드가 켜지거나 꺼질 때 호출됩니다.                                                                                            	|
| OnGUI         	| 게임 내의 모드 매니저 설정에서, 이 모드의 설정이 열려있을 때 **매 프레임마다** 호출됩니다.                                        	|
| OnSaveGUI     	| 게임 내의 모드 매니저 설정에서 Save 버튼을 누를 때 호출됩니다.                                                                    	|
| OnUpdate      	| MonoBehaviour.Update에 의해 호출됩니다. MonoBehaviour.Update는 MonoBehaviour가 켜져 있다면 **매 프레임마다** 호출됩니다.          	|
| OnLateUpdate  	| MonoBehaviour.LateUpdate에 의해 호출됩니다. MonoBehaviour.LateUpdate는 MonoBehaviour.Update 이후에 호출됩니다.                   	|
| OnFixedUpdate 	| MonoBehaviour.FixedUpdate에 의해 호출됩니다.                                                                                     	|
| OnShowGUI     	| 게임 내의 모드 매니저 설정에서, 이 모드의 설정이 열릴 때 호출됩니다.                                                                	|
| OnHideGUI     	| 게임 내의 모드 매니저 설정에서, 이 모드의 설정이 닫힐 때 호출됩니다.                                                              	|

## 빌드와 모드 적용 및 실행

1. 프로젝트를 빌드합니다.
2. A Dance of Fire and Ice 게임 폴더를 엽니다.
3. Mods 폴더를 엽니다.
4. 모드 이름으로 된 폴더를 생성합니다.
5. 그 폴더 안에 Info.json 파일과 빌드된 dll 파일을 넣습니다.
6. 게임을 실행합니다.

가이드를 정상적으로 따라오면 문제 없이 실행될 것입니다.

---

위 내용 중 일부는 다음 문서를 번역한 내용을 담고 있습니다.

* NexusMods 위키의 [How to create mod for unity game 문서](https://wiki.nexusmods.com/index.php/How_to_create_mod_for_unity_game)

위 내용 중 일부는 원저작자의 허락을 맡고 수정 및 가공한 내용을 담고 있습니다.

* GitHub 리포지토리 [NoBrain0917](https://github.com/NoBrain0917)/[ADOFAI-Mod-Development-Guide](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md)

---

## [이곳을 클릭하면 다음 페이지로 넘어갑니다.](./dev-3.md) <!-- omit in toc -->