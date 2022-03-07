# 한국어 모딩 가이드
<ins>[[ < 이전 페이지 ]](../README.md)</ins>

## 모드 사용 및 설치 설명
1. [UnityModManager 설치 방법](./use-1.md)
2. [모드 적용 및 사용 방법](./use-2.md)

## 모드 개발 설명
1. [개발 환경 구축](./dev-1.md)
2. [기본적인 틀 만들기](./dev-2.md)
3. [설정 UI 만들기](./dev-3.md)
4. [모드 업로드하기](./dev-99.md)


<details>
<summary>모드 개발 페이지는 아직 완성되지 않았습니다. 펼쳐서 개발 문서에서 다룰 내용과 링크를 확인할 수 있습니다.</summary>

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