---
title: JavaScript を使用するモデル駆動型アプリでクライアント スクリプトを使用してビジネス ロジックを適用 | Microsoft Docs
description: 開発者がクライアント側スクリプトおよびモデル駆動型アプリ内で JavaScript を使用する方法について説明します。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: kvivek
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/31/2018
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="apply-business-logic-using-client-scripting-in-model-driven-apps-using-javascript"></a>JavaScript を使用するモデル駆動型アプリでクライアント スクリプトを使用してビジネス ロジックを適用

JavaScript を使用したクライアント側スクリプトは、モデル駆動型アプリのフォームでデータを表示するためのカスタム ビジネス プロセスのロジックを適用する方法の一つですが、最初の選択にする必要はありません。 *業務ルール*は、JavaScript を知らない、開発者ではないユーザー向けにフォームでのビジネス プロセスのロジックを適用する手段を提供します。 詳細: [ロジックに適用するための業務ルールを作成する](/powerapps/maker/model-driven-apps/create-business-rules-recommendations-apply-logic-form)

> [!TIP]
> 業務ルール デザイナーは [powerapps.com](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) の **Common Data Service** 領域内にあります。 エンティティを表示するとき、**業務ルール**タブを検索します。

業務ルールを使用して業務要件を達成できない場合、クライアント API オブジェクト モデルを使用したクライアント スクリプトは、アプリケーションの動作を拡張し、クライアントの自動化を有効にする強力な方法を提供します。

## <a name="use-client-scripting-in-model-driven-apps"></a>モデル駆動型アプリでクライアント スクリプトを使用する

モデル駆動型アプリのフォームのヘルプにより、データをユーザーに表示します。 モデル駆動型アプリのフォームは、フィールド、簡易入力フォームまたはグリッドなどのアイテムを含むことができます。 [イベント](clientapi/events-forms-grids.md) は次の場合はいつでもモデル駆動型アプリ フォームで発生します:
- フォームロード
- データはフォーム内のフィールドまたはアイテムにおいて変更されます
- データはフォームに保存されます。

フォームにイベントが発生した場合にコードが実行されるように、これらのイベントに「応答」するためのJavaScriptコードを添付できます。 モデル駆動型アプリの [スクリプト Web リソース](script-jscript-web-resources.md) を使用して、これらのイベントに JavaScript コード (スクリプト) を添付します。 

モデル駆動型アプリは、何時および何をフォームに表示するかをコントロールするフォームオブジェクトおよびイベントと対話するための**クライアント API** の豊富なセットを提供します。

> [!NOTE]
> モデル駆動型アプリの現在のリリースで、一部のクライアント API が削除されます。 モデル駆動型アプリのクライアント側のコードを記述する際に、これらの API に注意しているか確認してください。 詳細: [使用が中止されたクライアントAPI](/dynamics365/get-started/whats-new/customer-engagement/important-changes-coming#some-client-apis-are-deprecated)

## <a name="get-started-here"></a>ここから始めましょう

[フォームおよびグリッドのイベント](clientapi/events-forms-grids.md)<br/>
[クライアント API オブジェクト モデルについて](clientapi/understand-clientapi-object-model.md)<br/>
[チュートリアル: 最初のクライアント スクリプトを記述する](clientapi/walkthrough-write-your-first-client-script.md)

## <a name="reference"></a>参照

[クライアント API リファレンス](clientapi/reference.md)


### <a name="related-topics"></a>関連トピック

[モデル駆動型アプリのための Web リソース](web-resources.md)<br/>
[コマンド、およびリボンをカスタマイズする](customize-commands-ribbon.md)

