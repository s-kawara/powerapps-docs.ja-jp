---
title: 埋め込みキャンバス アプリの共有 | MicrosoftDocs
ms.custom: ''
ms.date: 01/07/2019
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
[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

このトピックでは、既に作成済みの埋め込みキャンバス アプリを共有する方法を説明します。

埋め込みキャンバス アプリを作成し、モデル駆動型フォームに追加した後、モデル駆動型フォームにアクセスするすべてのユーザーもキャンバス アプリおよび使用するデータに確実にアクセスできるようにする手順を実行する必要があります。 次のガイドラインを参照してください:
-   組織またはセキュリティ グループまたは特定のユーザーと埋め込みキャンバス アプリを共有します。 詳細: [アプリの共有](../canvas-apps/share-app.md#share-an-app)
-   ユーザーが埋め込みキャンバス アプリを使用しているすべての Common Data Service エンティティに適切なアクセス許可があることを確認します。 詳細: [エンティティのアクセス許可の管理](../canvas-apps/share-app.md#manage-entity-permissions)
-   SharePoint や OneDrive など、ユーザーが埋め込みキャンバス アプリを使用しているすべてのクラウド サービスのデータに適切なアクセス許可があることを確認します。 共有する手順は、各クラウド サービス固有で、PowerApps の範囲を超えています。

> [!NOTE]
> 現在、セキュリティ ロール内の**キャンバス アプリ**特権を使用して、埋め込みキャンバス アプリまたはスタンドアロン キャンバス アプリのいずれかに対するアクセス権をアプリ ユーザーに付与することはできません。

埋め込みキャンバス アプリもソリューションに対応していません。 既定では、埋め込みキャンバス アプリはホストのモデル駆動型フォームと同じソリューションで作成されます。 1 つの環境から別の環境に埋め込みキャンバス アプリを移動するには、他のコンポーネントと同じようにソリューションの一部として埋め込みキャンバス アプリをエクスポートおよびインポートします。

## <a name="see-also"></a>関連項目
[モデル駆動型フォームないにキャンバス アプリを埋め込む](embed-canvas-app-in-form.md) <br />
[埋め込みキャンバス アプリに現在のレコードをデータ コンテキストとして渡す](pass-current-embedded-canvas-app.md) <br />
[関連付けられたレコードのリストをデータ コンテキストとして埋め込みキャンバス アプリに渡す](pass-related-embedded-canvas-app.md) <br />
[組み込みキャンバス アプリ内からホスト フォームで事前定義済みの操作を実行する](embedded-canvas-app-actions.md) <br />
[埋め込みキャンバス アプリの作業のガイドライン](embedded-canvas-app-guidelines.md)
