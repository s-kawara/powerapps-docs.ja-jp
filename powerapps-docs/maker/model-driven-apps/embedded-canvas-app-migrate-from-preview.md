---
title: 共有プレビュー リリースを使用して作成されたモデル駆動型フォーム上の埋め込みキャンバス アプリへの移行 | MicrosoftDocs
ms.custom: ''
ms.date: 06/25/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - PowerApps
author: Aneesmsft
ms.author: matp
manager: kvivek
tags:
  - PowerApps maker portal impact
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="migrate-embedded-canvas-apps-on-model-driven-forms-created-using-the-public-preview-release"></a>共有プレビュー リリースを使用して作成されたモデル駆動型フォーム上の埋め込みキャンバス アプリに移行します。
> [!IMPORTANT]
> 最新のリリースでは、モデル駆動型フォーム上の埋め込みキャンバス アプリが利用可能になりました。 共有プレビュー リリースを使用して作成されたモデル駆動型フォーム上の埋め込みキャンバス アプリは、最新リリースを使用して作成された新しい埋め込みキャンバス アプリに移行する必要があります。
> 共有プレビュー リリースを使用して作成されたモデル駆動型フォーム上の埋め込みキャンバス アプリのサポートは、まもなく非推奨になります。 

共有プレビュー リリースを使用して作成されたモデル駆動型フォーム上の埋め込みキャンバス アプリを最新のものに移行するには、作成者はまず最新リリースを使用して新しい埋め込みキャンバス アプリを作成する必要があります。 作成者は既存のものから新しい埋め込みキャンバス アプリにコントロールをコピーして、必要なデータ ソースを追加して、破損した参照があれば更新します。 詳細な手順を以下に示します。

1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。
2. PowerApps Studioで編集するために共有プレビュー リリースを使用して作成した埋め込みキャンバス アプリを開きます 。 キャンバス アプリの編集手順については [キャンバス アプリの編集](../canvas-apps/edit-app.md) をご覧ください。
3. 新しいブラウザー タブで、手順に従って [新しい埋め込みキャンバス アプリをモデル駆動型フォームを追加 ](embedded-canvas-app-add-classic-designer.md) します。
4. 以下の手順に従って、共有プレビュー リリースを使用して作成された埋め込みキャンバス アプリから新しい埋め込みキャンバス アプリにコントロールを一度に一画面ずつコピーします。
    1. PowerApps Studio で、共有プレビュー プレビュー リリースを使用して、作成された埋め込みキャンバス アプリのある手順2のブラウザー タブを選択し、開きます。
    2. コントロールをコピーする画面を選択します。
    3. **Ctrl + A** を使用して、画面上のすべてのコントロールを選択します。
    4. **Ctrl + C** 使用して、選択したすべてのコントロールをコピーします。
    5. 最新のリリースを使用して作成された新しい埋め込みキャンバス アプリのある手順3のブラウザー タブを選択します。
    6. 画面を選択するか、新しい画面を追加してください。
    7. **Ctrl + V** 使用して、指定画面のコントロールを貼り付けます。
    8. 各画面をコピーする手順を繰り返します。
5. すべての画面のコピーが完了したら、手順3のブラウザー タブを選択します。最新のリリースを使用して作成された新しい埋め込みキャンバス アプリがあります。
6. ホスト モデル駆動型フォームのレコードにアクセスするすべての場所を更新します。 **最初に (ModelDrivenFormIntegration.Data)** を **ModelDrivenFormIntegration.Item** に置き換えます。
7. 新しい埋め込みキャンバス アプリに足りないデータ ソースを追加します。
8. 新しい埋め込みキャンバス アプリのすべてのリンク切れした参照を更新します。 
9. 変更が完了したら、 **ファイル** タブを選択し、 **保存**を選択します。
10. 変更した内容をエンドユーザーが利用できるようにするには、 **公開** を選択し、 **このバージョンを公開する**を選択します。

## <a name="migrating-embedded-canvas-apps-on-model-driven-forms-that-use-a-list-of-records-related-to-the-current-main-form-record"></a>現在の (メイン フォーム) レコードに関連するレコードの一覧を使用するモデル駆動型フォーム上の埋め込みキャンバス アプリへの移行。

プレビュー リリースでは、 キャンバス アプリをモデル駆動型フォームに埋め込むために、現在の (メイン フォーム) レコードをデータ コンテキストとして渡すのか、現在の (メイン フォーム) レコードに関連するレコードの一覧を渡すのか事前に決める必要がありました。 次に、フィールドやサブグリッド コントロールに、キャンバス アプリコント ロール を追加する必要がありました。

最新リリースでは、モデル駆動型フォームに埋め込みキャンバス アプリを追加すると、フィールドに対してのみ簡素化および合理化されます。 作業者は、 Common Data Service コネクタを使用して、簡単にキャンバス アプリ内で関連レコードの一覧に直接アクセス できます。 

現在の (メイン フォーム) レコードに関連するレコードの一覧を使用するモデル駆動型フォーム上の埋め込みキャンバス アプリへ移行するために、以下の手順に従ってください。

1. 上記セクションの手順にしたがって、共有プレビュー リリースを使用して、作成されたモデル駆動型フォーム上の埋め込みキャンバス アプリを最新のものに移行します。
2. Common Data Service コネクタを使用して、関連エンティティのデータ ソースをアプリに追加します。 キャンバス アプリにデータ ソースを追加する方法ついては、 [PowerAppsでキャンバス アプリにデータ接続を追加](../canvas-apps/add-data-connection.md) を参照してください。
3. [ギャラリー](../canvas-apps/controls/control-gallery.md) や [データ テーブル](../canvas-apps/controls/control-data-table.md) などのコントロールに関連エンティティのデータ ソースを使用する場合は、 **[フィルター](../canvas-apps/functions/function-filter-lookup.md)** 関数をを使用します。レコードを現在の (メイン フォーム) レコードに関連するレコードにフィルタ処理します。 現在の (メイン フォーム) レコードが、**ModelDrivenFormIntegration.Item**を介して利用できます。
    > [!NOTE]
    > 埋め込み型キャンバス アプリケーションは、ModelDrivenFormIntegration.Itemを経由してホストのモデル駆動フォームからのすべてのレコードにアクセスすることができます。 たとえば、**accountnumber** という名称と **アカウント番号** という表示名称を持つフィールドの値を取得するには、 **ModelDrivenFormIntegration.Item.accountnumber** または **ModelDrivenFormIntegration.Item.'Account Number'** を使用することができます。
4. 最新の更新では、 Common Data Service もフィルターとしてエンティティ ビューを使用するためのサポートを提供します。 詳細については、ブログ投稿[強化されたデータ ソースの選択と Common Data Service ビュー](https://powerapps.microsoft.com/blog/improved-data-source-selection-and-common-data-service-views/) を参照してください。 

## <a name="see-also"></a>関連項目
[モデル駆動型フォーム上にキャンバス アプリを埋め込む](embed-canvas-app-in-form.md) <br />
[埋め込み型キャンバス アプリケーションをモデル駆動フォームに追加する](embedded-canvas-app-add-classic-designer.md) <br />
[モデル駆動型フォームの埋め込み型キャンバス アプリケーションを編集する](embedded-canvas-app-edit-classic-designer.md) <br />
[モデル駆動フォームに埋め込まれたキャンバス アプリケーションの画面サイズと表示方向をカスタマイズする](embedded-canvas-app-customize-screen.md) <br />
[組み込みキャンバス アプリ内からホスト フォームで事前定義済みの操作を実行する](embedded-canvas-app-actions.md) <br />
[ModelDrivenFormIntegrationコントロールのプロパティとアクション](embedded-canvas-app-properties-actions.md) <br />
[埋め込みキャンバス アプリの共有](share-embedded-canvas-app.md)。 <br />
[埋め込みキャンバス アプリの作業のガイドライン](embedded-canvas-app-guidelines.md) <br />
