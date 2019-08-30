---
title: Teams に PowerApps アプリを埋め込む |Microsoft Docs
description: PowerApps で作成したアプリを Microsoft Teams に埋め込み、共有することができます。
author: jimholtz
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 05/29/2019
ms.author: jimholtz
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: ca3430d6b639b7a4c3980f5bbb0ba202220f6d9e
ms.sourcegitcommit: 935470edc7441b76533cc937e6f32229bfd6f11f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70117807"
---
# <a name="embed-a-powerapps-app-in-teams"></a>チームへの PowerApps アプリの埋め込み 

Microsoft Teams に直接埋め込むことで作成した PowerApps を共有することができます。 完了したら、ユーザーは **+** を選択し、所属するチーム内のチャネルまたは会話のいずれかにアプリを追加できます。 アプリは、**チーム タブ** の下にタイルとして表示されます。 

管理者がアプリをアップロードし、テナント内の**すべて**のチームの**すべてのタブ セクション** に表示するようにできます。 [Microsoft Teams にアプリを共有](https://docs.microsoft.com/en-us/power-platform/admin/embed-app-teams) を参照してください。

> [!NOTE]
> カスタム アプリのアップロードを許可するようにチームのカスタム アプリのポリシーを設定する必要があります。 アプリをチームに埋め込めない場合は、管理者に連絡し、[カスタム アプリの設定](https://docs.microsoft.com/MicrosoftTeams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)が設定されているか確認してください。 

## <a name="prerequisites"></a>前提条件

- [PowerApps ライセンスを持っている](https://docs.microsoft.com/power-platform/admin/pricing-billing-skus)
- キャンバスアプリを作成しました

## <a name="locate-your-powerapps-guid"></a>PowerApp の GUID を見つける

後の手順で使用する PowerApp の GUID を見つけてメモします。

1. [ https://web.powerapps.com ](https://web.powerapps.com)にサインインし、メニューから**アプリ**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![アプリの一覧を表示する](./media/embed-teams-app/file-apps2.png "アプリの一覧を表示する")

2. Teams で共有するアプリの**その他コマンドより(...)** を選択し、**詳細**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![アプリの詳細](./media/embed-teams-app/app-details.png "アプリの詳細")


3. 後で使用する為に**アプリ ID**を記録します。

   > [!div class="mx-imgBorder"] 
   > ![アプリの詳細](./media/embed-teams-app/app-details2.png "アプリの詳細")

## <a name="install-app-studio"></a>App Studio のインストール

App Studio が既にインストールされている場合は、これらの手順を省略できます。 

1. Teamsでは、チームメニューの左下の**アプリ**(![アプリ アイコン](./media/embed-teams-app/apps-icon.png "アプリ アイコン"))を選択します。

2. 検索ボックスで"App Studio"を検索し、それを選択します。

   > [!div class="mx-imgBorder"] 
   > ![App Studio](./media/embed-teams-app/store-app-studio.png "App Studio")

3. **インストール**を選択します。 

   > [!div class="mx-imgBorder"] 
   > ![App Studio のインストール](./media/embed-teams-app/install-app-studio.png "App Studio のインストール")

4. アプリ機能として**オープン**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![App Studio を開く](./media/embed-teams-app/open-app-studio.png "App Studio を開く")

## <a name="create-a-teams-app-for-your-powerapp"></a>PowerApp 用の Teams アプリを作成する

1. Teams で、App Studio を開きます。

   > [!div class="mx-imgBorder"] 
   > ![App Studio を開く](./media/embed-teams-app/open-app-studio2.png "App Studio を開く")

2. **マニフェスト エディター** タブを選択し、ようこそ下の**新しいアプリを作成**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![新しいアプリの作成](./media/embed-teams-app/create-new-app.png "新しいアプリの作成")

3. **アプリの詳細**ページにアプリに関する情報を入力します。  アプリ ID の GUID には、上記で記録した PowerApp のアプリ ID の GUID を使用してください。  これにより、特定の PowerApp に対する Teams アプリの重複が回避されます。
 
   > [!div class="mx-imgBorder"] 
   > ![情報の入力](./media/embed-teams-app/fill-in-info-about-app.png "情報の入力")

   |フィールド  |説明  |
   |---------|---------|
   |**アプリ名** |    |
   |短い名前     | 必須。 アプリの短い表示名。 30文字の制限。        |
   |長い名前     | アプリの完全名。完全なアプリ名が30文字を超える場合に使用されます。       | 
   |**番号**     |         |
   |アプリ ID     | 必須。 Microsoft が生成したこのアプリの一意の識別子。        |
   |パッケージ名     | 必須。 このアプリの一意の識別子。 逆引きドメイン表記を使用することをお勧めします。たとえば、「.com」のようにします<AppName>。       |
   |Version     | 必須。 特定のアプリのバージョン。 マニフェストの内容を更新する場合は、バージョンもインクリメントする必要があります。     |
   |**摘要**    |     |
   | 簡単な説明    | 必須。 領域が制限されている場合に使用される、アプリのエクスペリエンスに関する簡単な説明。 80文字の制限。   |
   | 長い説明    | 必須。 アプリの完全な説明。     |
   | **開発者向け情報**    |     |
   | 名前    | 必須。 会社または開発者の表示名。     |
   | 用    | 必須。 Powerapps.com を使用したアプリの web サイトへの https://URL。 だれかがアプリをインストールすると、"アプリについて" というページが表示されます。 Powerapps.com 上のアプリの web バージョンにリンクする必要があります。   |
   | **アプリの Url**    | これらのリンクは、web サイトの URL と共に **[バージョン情報]** ページに表示されます。     |
   | プライバシーに関する声明    | 必須。 開発者のプライバシーポリシーへの https://URL。 [例](https://go.microsoft.com/fwlink/p/?LinkID=698505)。   |
   | 利用規約    | 必須。 開発者の使用条件への https://URL。  [例](https://go.microsoft.com/fwlink/p/?LinkID=698507)。  |
   | **戦略**    |     |
   | 全色    | Full color 192x192 PNG アイコンへの相対ファイルパス。    |
   | 透明なアウトライン    |透過的な32x32 の PNG アウトラインアイコンへの相対ファイルパス。     |
   | アクセントカラー    | アウトラインアイコンの背景としておよびと組み合わせて使用する色。     |

詳細については、「[マニフェストエディター](https://docs.microsoft.com/microsoftteams/platform/get-started/get-started-app-studio#manifest-editor)と[マニフェストスキーマ](https://docs.microsoft.com/microsoftteams/platform/resources/schema/manifest-schema)」を参照してください。

4. [ブランド] セクションまで下にスクロールし、アプリに必要なロゴとアクセントカラーを追加します。  これらは、チームでアプリに対して表示されるロゴです。 

   > [!div class="mx-imgBorder"] 
   > ![ブランド化とタブ](./media/embed-teams-app/branding-tabs.png "ブランド化とタブ")

5. **機能**で**タブ**を選択します。

6. **チーム タブ**で**追加**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![チームタブの追加](./media/embed-teams-app/team-tab-add.png "チームタブの追加")

7. 次の形式を使用して、"Configuration URL" 入力フィールドにアプリの構成 URL を追加します。`https://web.powerapps.com/webplayer/teamsapptabsettings?appid=<PowerApp ID>`

   `<PowerApp ID>`を上記で記録したアプリ ID GUID に置き換えます。

   アプリを表示する[スコープ](https://docs.microsoft.com/microsoftteams/platform/concepts/tabs/tabs-overview#tab-scope)を選択します。 **構成を更新できる**がオンになっていることを確認し、**保存**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![構成 URL](./media/embed-teams-app/configuration-url.png "構成 URL")

8. **完了**で**有効なドメイン**を選択します。 Teams アプリケーションの有効なドメインとして**apps.powerapps.com**と**apps.preview.powerapps.com**を追加します。

   > [!div class="mx-imgBorder"] 
   > ![有効なドメインの追加](./media/embed-teams-app/add-valid-domains.png "有効なドメインの追加")

9. **完了**で**テストと配布**を選択します。 **インストール**で**インストール**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![インストールの選択](./media/embed-teams-app/test-distribute-app.png "インストールの選択")

10. アプリをインストールするチームを選択し、**インストール**を選択します。

    > [!div class="mx-imgBorder"] 
    > ![チームインストールに追加](./media/embed-teams-app/new-app-add-to-team.png "チームインストールに追加")
11. そのアプリのインスタンスをすぐにチャネルに追加する場合は、アプリを使用するチャネルを選択し**セットアップ**を選択します。

    > [!div class="mx-imgBorder"] 
    > ![セットアップの選択](./media/embed-teams-app/app-now-available.png "セットアップの選択")

12. **[保存]** を選択します。

## <a name="add-the-app-as-a-tab"></a>アプリをタブとして追加する

アプリをタブとしてチャネルまたは会話に追加するには、 **+** を選択し、**チーム タブ**下でアプリを選択します。 

> [!div class="mx-imgBorder"] 
> ![[アプリをタブとして追加]](./media/embed-teams-app/add-app-as-tab.png "[アプリをタブとして追加]")

これで、アプリがタブとして表示されるようになります。

> [!div class="mx-imgBorder"] 
> ![[アプリとしてのアプリ]](./media/embed-teams-app/app-as-tab.png "[アプリとしてのアプリ]")

### <a name="see-also"></a>関連項目
[Microsoft Teams へようこそ](https://docs.microsoft.com/MicrosoftTeams/teams-overview)<br />
[管理者の場合:Microsoft Teams へのアプリの埋め込み](https://docs.microsoft.com/power-platform/admin/share-app-teams)
