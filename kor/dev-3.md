# 한국어 모딩 가이드 <!-- omit in toc -->

[[ < 이전 페이지 ]](./dev-1.md) [[ 다음 페이지 > ]](./dev-3.md)

- [이용자 배려](#이용자-배려)
  - [독해, 가독성 문제 최소화](#독해-가독성-문제-최소화)
  - [접근성](#접근성)
- [모드의 기본적인 틀 구축](#모드의-기본적인-틀-구축)
  - [UnityModManager.ModEntry 세부 사항](#unitymodmanagermodentry-세부-사항)
- [모드 설정 UI 제작](#모드-설정-ui-제작)
  - [원리와 기본적인 UI 제작](#원리와-기본적인-ui-제작)

---

## 모드 설정 UI 제작

모드 설정 UI는 [IMGUI](https://docs.unity3d.com/Manual/GUIScriptingGuide.html)를 이용해 제작할 수 있습니다.

### 원리와 기본적인 UI 제작

IMGUI는 OnGUI()라는 특수 메서드를 사용합니다. `OnGUI` 메서드는 `OnUpdate` 메서드와 비슷하게, 모드 설정이 열려 있을 때 매 프레임마다 호출됩니다.

우선 Reference에 `UnityEngine.CoreModule`과 `UnityEngine.IMGUIModule`을 추가합니다.

```cs
using UnityEngine;

(생략)

    static bool Load(UnityModManager.ModEntry modEntry)
    {
        modEntry.OnToggle = OnToggle;
        modEntry.OnGUI = OnGUI;
        return true;
    }

    static void OnGUI(UnityModManager.ModEntry modEntry)
    {
        GUILayout.Label("테스트 라벨");
    }

(생략)
```

위 코드를 차례차례 살펴 보면,
* `OnGUI` 메서드를 `modEntry.OnGUI`에 대입합니다.
* `OnGUI` 메서드는 "테스트 라벨"이라는 텍스트가 쓰여진 라벨을 생성합니다.

---

위 내용 중 일부는 다음 문서를 번역한 내용을 담고 있습니다.

* NexusMods 위키의 [How to create mod for unity game 문서](https://wiki.nexusmods.com/index.php/How_to_create_mod_for_unity_game)
* 유니티 매뉴얼의 [Immediate Mode GUI (IMGUI)](https://docs.unity3d.com/Manual/gui-Basics.html)

---

## [이곳을 클릭하면 다음 페이지로 넘어갑니다.](./dev-4.md) <!-- omit in toc -->