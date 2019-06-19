---
title: Teams で PowerApps アプリを埋め込む |Microsoft Docs
description: 共有する Microsoft Teams で PowerApps で作成されたアプリを埋め込むことができます。
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
ms.openlocfilehash: d17b02cc87bb219474aade955a2910f12fcf7f27
ms.sourcegitcommit: 2376c1f1f3431bca52a8deb9b966ce1fe9f88da0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2019
ms.locfileid: "66381388"
---
# <a name="embed-a-powerapps-app-in-teams"></a>Teams で PowerApps アプリを埋め込む 

Microsoft Teams に直接埋め込むことで作成した PowerApps を共有することができます。 完了したら、ユーザーが選択できる **+** のいずれかにアプリを追加する **、** team チャンネルまたはでは、チーム内のメッセージ交換します。 下のタイルとして、アプリが表示されます**チーム タブ**します。 

管理者がアプリをアップロードし、テナント内の**すべて**のチームの**すべてのタブ セクション** に表示するようにできます。 [Microsoft Teams にアプリを共有](https://review.docs.microsoft.com/en-us/power-platform/admin/embed-app-teams?branch=JimHoltzWorkBranch) を参照してください。

> [!NOTE]
> カスタム アプリのアップロードを許可するのには、チームのカスタム アプリのポリシーを設定する必要があります。 セットアップをしたかどうかを参照してください。 には、管理者に確認して場合、Teams にアプリを埋め込むにはできません[カスタム アプリの設定](https://docs.microsoft.com/MicrosoftTeams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)します。 

## <a name="prerequisites"></a>前提条件

- [PowerApps のライセンスがあります。](https://docs.microsoft.com/power-platform/admin/pricing-billing-skus)
- キャンバス アプリの作成

## <a name="locate-your-powerapps-guid"></a>検索の PowerApp の GUID

PowerApp のメモを見つけて、後の手順で使用する GUID。

1. [ https://web.powerapps.com ](https://web.powerapps.com)にサインインし、メニューから**アプリ**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![アプリの一覧を表示する](./media/embed-teams-app/file-apps2.png "アプリの一覧を表示します。")

2. Teams で共有するアプリの**その他コマンドより(...)** を選択し、**詳細**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![アプリの詳細](./media/embed-teams-app/app-details.png "アプリの詳細")

3. 後で使用する為に**アプリ ID**を記録します。

   > [!div class="mx-imgBorder"] 
   > ![アプリの詳細](./media/embed-teams-app/app-details2.png "アプリの詳細")

## <a name="install-app-studio"></a>App Studio をインストールします。

App Studio が既にインストールされている場合は、次の手順を省略できます。 

1. チームで選択**アプリ**チーム メニューの左下で (![アプリ アイコン](./media/embed-teams-app/apps-icon.png "アプリ アイコン"))。

2. 検索ボックスに"App Studio"を検索し、それを選択します。

   > [!div class="mx-imgBorder"] 
   > ![App Studio](./media/embed-teams-app/store-app-studio.png "App Studio")

3. **インストール**を選択します。 

   > [!div class="mx-imgBorder"] 
   > ![App Studio をインストール](./media/embed-teams-app/install-app-studio.png "App Studio のインストール")

4. アプリ機能として**オープン**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![App Studio を開いて](./media/embed-teams-app/open-app-studio.png "App Studio を開く")

## <a name="create-a-teams-app-for-your-powerapp"></a>チーム アプリ、PowerApp を作成します。

1. チームでは、App Studio を開きます。

   > [!div class="mx-imgBorder"] 
   > ![App Studio を開いて](./media/embed-teams-app/open-app-studio2.png "App Studio を開く")

2. **マニフェスト エディター** タブを選択し、ようこそ下の**新しいアプリを作成**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![新しいアプリの作成](./media/embed-teams-app/create-new-app.png "新しいアプリの作成")

3. **アプリの詳細**ページにアプリに関する情報を入力します。  アプリ ID の GUID には、上記で記録した PowerApp のアプリ ID の GUID を使用してください。  これにより、チームのアプリの特定の PowerApp の重複が回避されます。
 
   > [!div class="mx-imgBorder"] 
   > ![情報を入力](./media/embed-teams-app/fill-in-info-about-app.png "情報を入力")

   |フィールド  |説明  |
   |---------|---------|
   |**アプリ名** |    |
   |短い名前     | 必須。 アプリの短い表示名。 30 文字の制限。        |
   |長い名前     | アプリケーションの完全名が 30 文字を超える場合は、使用、アプリの完全名。       | 
   |**識別**     |         |
   |アプリ ID     | 必須。 Microsoft 生成の一意の識別子このアプリ。        |
   |パッケージ名     | 必須。 このアプリの一意の識別子。 逆引きドメイン表記を使用することをお勧めします。たとえば、com.example します.<AppName>。       |
   |バージョン     | 必須。 特定のアプリのバージョン。 マニフェストで何かを更新する場合のバージョンが増分される必要があります。     |
   |**説明**    |     |
   | 簡単な説明    | 必須。 空き領域が少ないときに使用、アプリのエクスペリエンスの短い説明。 80 文字の制限。   |
   | 長い説明    | 必須。 アプリの詳細について説明します。     |
   | **開発者向け情報**    |     |
   | 名前    | 必須。 会社または developer の表示名。     |
   | Web サイト    | 必須。 Powerapps.com 経由でアプリの web サイトに https:// URL です。 ユーザーが、アプリのインストール時に、"アプリ"に関するページが表示されます。 Powerapps.com でのアプリの web バージョンにリンクする必要があります。   |
   | **アプリの Url**    | これらのリンクが表示されます、**について**ページと web サイトの URL。     |
   | プライバシーに関する声明    | 必須。 開発者のプライバシー ポリシーを https:// URL です。 [例](https://go.microsoft.com/fwlink/p/?LinkID=698505)します。   |
   | 使用条件    | 必須。 開発者の使用条件に https:// URL です。  [例](https://go.microsoft.com/fwlink/p/?LinkID=698507)します。  |
   | **ブランド化**    |     |
   | 完全な色    | 192 x 192 の完全な色の PNG アイコンへの相対ファイル パス。    |
   | 透過的なアウトライン    |透過的な 32 x 32 PNG アウトライン アイコンへの相対ファイル パス。     |
   | アクセントの色    | アウトライン アイコンの背景としてと組み合わせて使用する色。     |

詳細については、次を参照してください。[マニフェスト エディター](https://docs.microsoft.com/microsoftteams/platform/get-started/get-started-app-studio#manifest-editor)と[マニフェスト スキーマ](https://docs.microsoft.com/microsoftteams/platform/resources/schema/manifest-schema)します。

4. ブランド化セクションまでスクロールし、ロゴおよびアプリの必要なアクセントの色を追加します。  これらは、Teams にアプリが表示されるロゴです。 

   > [!div class="mx-imgBorder"] 
   > ![ブランド化およびタブ](./media/embed-teams-app/branding-tabs.png "ブランドおよびタブ")

5. **機能**で**タブ**を選択します。

6. **チーム タブ**で**追加**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![[チーム] タブ追加](./media/embed-teams-app/team-tab-add.png "チーム タブの追加")

7. 次の形式を使用して、"構成 URL"の入力フィールドで、アプリの構成の URL を追加します。 `https://web.powerapps.com/webplayer/teamsapptabsettings?appid=<PowerApp ID>`

   `<PowerApp ID>`を上記で記録したアプリ ID GUID に置き換えます。

   アプリを表示する[スコープ](https://docs.microsoft.com/microsoftteams/platform/concepts/tabs/tabs-overview#tab-scope)を選択します。 **構成を更新できる**がオンになっていることを確認し、**保存**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![構成 URL](./media/embed-teams-app/configuration-url.png "構成 URL")

8. **完了**で**有効なドメイン**を選択します。 Teams アプリケーションの有効なドメインとして**apps.powerapps.com**と**apps.preview.powerapps.com**を追加します。

   > [!div class="mx-imgBorder"] 
   > ![有効なドメインを追加](./media/embed-teams-app/add-valid-domains.png "有効なドメインの追加")

9. **完了**で**テストと配布**を選択します。 **インストール**で**インストール**を選択します。

   > [!div class="mx-imgBorder"] 
   > ![インストールを選択](./media/embed-teams-app/test-distribute-app.png "インストールを選択します。")

10. アプリをインストールするチームを選択し、**インストール**します。

    > [!div class="mx-imgBorder"] 
    > ![インストールのチームに追加](./media/embed-teams-app/new-app-add-to-team.png "チームのインストールに追加")

11. チャンネルにすぐにそのアプリのインスタンスを追加する場合に選択し、アプリを使用するチャネルを選択します。**セットアップ**します。

    > [!div class="mx-imgBorder"] 
    > ![上のセットを選択](./media/embed-teams-app/app-now-available.png "選択を設定します。")

12. **[保存]** を選択します。

## <a name="add-the-app-as-a-tab"></a>タブとして、アプリを追加します。

任意のチャネルまたはメッセージ交換にタブとして、アプリを追加するには、選択 **+** 、下にある**チーム タブ**アプリを選択します。 

> [!div class="mx-imgBorder"] 
> ![アプリの追加のタブとして](./media/embed-teams-app/add-app-as-tab.png "タブとしてアプリの追加")

アプリは、タブとして表示されます。

> [!div class="mx-imgBorder"] 
> ![アプリのタブとして](./media/embed-teams-app/app-as-tab.png "アプリ タブ")

### <a name="see-also"></a>関連項目
[Microsoft Teams へようこそ](https://docs.microsoft.com/MicrosoftTeams/teams-overview)<br />
[管理者。Microsoft Teams にアプリを埋め込む](https://docs.microsoft.com/power-platform/admin/share-app-teams)