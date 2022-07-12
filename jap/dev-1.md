# 日本語MODガイド
<ins>[[ < 前へ ]](./main.md)</ins> <ins>[[ 次へ > ]](./dev-2.md)</ins>

## 最小開発条件 (参考用)
* [.NET Framework 4.8](https://go.microsoft.com/fwlink/?linkid=2088517) - （絶対4.8である必要はないですが、個人的に推薦するバージョンです。）
* [UnityModManager](https://github.com/newman55/unity-mod-manager)
* Harmony - `UnityModManager`と一緒にインストールされます。（ファイル名：`0Harmony.dll`）
* Unity - ゲームのフォルダ内のdllファイルを参照に追加すればOKです。

## 開発環境の整備

ここでは[Visual Studio 2019](https://visualstudio.microsoft.com/) IDEを基準に説明します。

1. [クラス ライブラリ C# プロジェクトを作成](https://docs.microsoft.com/ja-jp/dotnet/core/tutorials/library-with-visual-studio)します。
2. [必要な参照を追加](https://docs.microsoft.com/ja-jp/visualstudio/ide/managing-references-in-a-project?view=vs-2019)します。
    * `UnityModManager/0Harmony.dll`
    * `UnityModManager/UnityModManager.dll`
    * `A Dance of Fire and Ice_Data/Managed/Unity*.dll`（MODが必要とするUnityモジュールを追加してください。）
    * `A Dance of Fire and Ice_Data/Managed/Assembly-CSharp.dll`
    * `A Dance of Fire and Ice_Data/Managed/Assembly-CSharp-firstpass.dll`
3. Info.jsonファイルを作成し、MODの情報を記入します。
    * これに関しては[このサイト](https://wiki.nexusmods.com/index.php/How_to_create_mod_for_unity_game)で詳しく説明されています。

---

## [ここをクリックして次へ進む](./dev-2.md)