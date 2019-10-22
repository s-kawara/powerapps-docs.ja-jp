---
title: 埋め込みキャンバス アプリの共有 | MicrosoftDocs
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

# <a name="share-an-embedded-canvas-app"></a>埋め込みキャンバス アプリの共有
このトピックでは、既に作成済みの埋め込みキャンバス アプリを共有する方法を説明します。

埋め込みキャンバス アプリを作成し、モデル駆動型フォームに追加した後、モデル駆動型フォームにアクセスするすべてのユーザーもキャンバス アプリおよび使用するデータに確実にアクセスできるようにする手順を実行する必要があります。 次のガイドラインを参照してください:
-   組織またはセキュリティ グループまたは特定のユーザーと埋め込みキャンバス アプリを共有します。 詳細: [アプリの共有](../canvas-apps/share-app.md#share-an-app)
-   ユーザーが埋め込みキャンバス アプリを使用しているすべての Common Data Service エンティティに適切なアクセス許可があることを確認します。 詳細: [エンティティのアクセス許可の管理](../canvas-apps/share-app.md#manage-entity-permissions)
-   SharePoint や OneDrive など、ユーザーが埋め込みキャンバス アプリを使用しているすべてのクラウド サービスのデータに適切なアクセス許可があることを確認します。 共有する手順は、各クラウド サービス固有で、PowerApps の範囲を超えています。

> [!NOTE]
> 現在、セキュリティ ロール内の**キャンバス アプリ**特権を使用して、埋め込みキャンバス アプリまたはスタンドアロン キャンバス アプリのいずれかに対するアクセス権をアプリ ユーザーに付与することはできません。

埋め込みキャンバス アプリもソリューションに対応していません。 既定では、埋め込みキャンバス アプリはホストのモデル駆動型フォームと同じソリューションで作成されます。 1 つの環境から別の環境に埋め込みキャンバス アプリを移動するには、他のコンポーネントと同じようにソリューションの一部として埋め込みキャンバス アプリをエクスポートおよびインポートします。

## <a name="see-also"></a>関連項目
[モデル駆動型フォーム上にキャンバス アプリを埋め込む](embed-canvas-app-in-form.md) <br />
[埋め込み型キャンバス アプリケーションをモデル駆動フォームに追加する](embedded-canvas-app-add-classic-designer.md) <br />
[モデル駆動型フォームの埋め込み型キャンバス アプリケーションを編集する](embedded-canvas-app-edit-classic-designer.md) <br />
[モデル駆動フォームに埋め込まれたキャンバス アプリケーションの画面サイズと表示方向をカスタマイズする](embedded-canvas-app-customize-screen.md) <br />
[組み込みキャンバス アプリ内からホスト フォームで事前定義済みの操作を実行する](embedded-canvas-app-actions.md) <br />
[ModelDrivenFormIntegrationコントロールのプロパティとアクション](embedded-canvas-app-properties-actions.md) <br />
[埋め込みキャンバス アプリの作業のガイドライン](embedded-canvas-app-guidelines.md) <br />
[パブリック プレビュー リリースを使用して作成された、モデル駆動型フォームの埋込み型キャンバスアプリケーションを最新版へと移行する](embedded-canvas-app-migrate-from-preview.md) <br />
