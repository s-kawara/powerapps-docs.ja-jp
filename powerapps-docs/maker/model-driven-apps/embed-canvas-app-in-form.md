---
title: モデル駆動型フォーム上にキャンバス アプリを埋め込む | MicrosoftDocs
ms.custom: ''
ms.date: 12/10/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - PowerApps
ms.assetid: 00e62904-2ce9-4730-a113-02b1fedbf22e
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

# <a name="embed-a-canvas-app-on-a-model-driven-form"></a>モデル駆動型フォーム上にキャンバス アプリを埋め込む

キャンバス アプリを使用すると、メーカーはわずかなコードを記述するだけで使用できる、WYSIWYG キャンバス アプリ デザイナーを使用して、カスタム レイアウトを容易に設計および作成することができます。 また、キャンバス アプリを使用すると、メーカーはそれらのフォーム上で 200 を超えるデータ ソースに接続してデータを表示することができます。

> [!NOTE]
> この機能は現在はプレビュー中です。 <br />
> [!INCLUDE [cc-preview-features-definition](../../includes/cc-preview-features-definition.md)]

組み込みキャンバス アプリにより、メーカーはキャンバス アプリの機能を自分のモデル駆動型フォームで使用することができます。 組み込みキャンバス アプリを使用すると、フォーム上にリッチなビジュアル領域を簡単に作成して、Common Data Service からのデータのすぐ隣に、様々なソースからのデータを表示することができます。

   > [!div class="mx-imgBorder"] 
   > ![](media/embed-canvas-app-in-form.png "モデル駆動型アプリ フォーム内の埋め込みキャンバス アプリ")

キャンバス アプリは、他のカスタムコントロールが追加されるのと同じ方法で、モデル駆動型フォームに埋め込まれます。 埋め込みキャンバス アプリには、ホストのモデル駆動型フォームからのコンテキスト データを埋め込みキャンバス アプリに移行する、豊富なデータ統合機能が含まれています。

キャンバス アプリをユーザーのモデル駆動型フォームに埋め込むステップは、ホストのモデル駆動型フォームが埋め込みキャンバス アプリに対して提供するデータ コンテキストにより異なります。
-   現在のレコードをデータ コンテキストとして渡します。 詳細: [埋め込みキャンバス アプリで現在のレコードをデータ コンテキストとして渡す](pass-current-embedded-canvas-app.md)
-   現在のレコードに関連付けられたレコードのリストをデータ コンテキストとして渡します。 詳細: [埋め込みキャンバス アプリで関連付けられたレコードのリストをデータ コンテキストとして渡す](pass-related-embedded-canvas-app.md) 

<!-- After you have added an embedded canvas app to your model-driven form, learn how to share your embedded canvas app with other users (LINK TO ARTICLE #4).  -->

<!-- For things to keep in mind when working with embedded canvas apps and to help troubleshoot any issues you might encounter, see (LINK TO ARTICLE #5). -->

## <a name="see-also"></a>関連項目
[PowerApps のキャンバス アプリとは](../canvas-apps/getting-started.md) <br />
[PowerApps のキャンバス アプリ コントロールの追加および構成](../canvas-apps/add-configure-controls.md) <br />
[PowerApps のキャンバス アプリ コネクタの概要](../canvas-apps/connections-list.md) 
