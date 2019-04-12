---
title: PowerAppsを使用したシステム エンティティ メッセージの編集| MicrosoftDocs
description: システム エンティティ メッセージの編集方法を説明する
ms.custom: ''
ms.date: 05/15/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: 3ccbd8de-8d6f-4058-87f7-15463667cfc6
caps.latest.revision: 41
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="edit-system-entity-messages"></a>システム エンティティ メッセージの編集

一部のシステム エンティティの既定の表示名は、Common Data Service のユーザー インターフェイスのテキストおよびエラー メッセージで使用されます。 表示名を変更した場合は、既定の表示名を使用するメッセージも更新する必要があります。 たとえば、表示名を *取引先企業* から *会社* に変更した場合は、古い名前を使用するエラー メッセージがまだ表示されます。  

PowerApps ポータルを使用してシステム メッセージを編集することはできません。ソリューション エクスプローラーを使用する必要があります。

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

ソリューション エクスプローラーでは、エンティティの下に**メッセージ**ノードが表示される場合、元のエンティティ表示名への参照を含む特定のテキストを編集できます。 

![エンティティ メッセージ](../model-driven-apps/media/entity-messages.png)

このテキストの編集は簡単です。 メッセージをダブルクリックすると、次の 3 つのフィールドのあるフォームが表示されます。  
  
|フィールド|説明|  
|-----------|-----------------|  
|**既定の表示文字列**|元のテキストを表示します。|  
|**カスタム表示文字列**|表示文字列を変更するには、このテキストを編集します。|  
|**コメント**|任意。 変更内容とその理由に関するコメントが含まれます。|  
  
メッセージ テキストの一部にはプレースホルダーを持ったものがあります。 これらのプレースホルダーは、かっこ付きの数値です。 例: `{0}`。 これらのプレースホルダーにより、テキストをメッセージに挿入できます。 メッセージを編集する場合は、これらのプレースホルダーを保持していることを確認します。 

![保存](media/save-entity-icon-solution-explorer.png)を選択して変更を保存します。 保存するときに、**保存して閉じる**を選択してフォームを閉じます。

> [!NOTE]
> システム エンティティ メッセージを編集するために表示される UI には、エンティティ名への多くの参照が含まれていますが、すべてが含まれているわけではありません。 総合的な方法の詳細は、「[基本言語のローカライズ可能なテキストの更新](../model-driven-apps/translate-localizable-text.md#updating-localizable-text-in-the-base-language)」を参照してください。

## <a name="programmatically-update-entity-display-strings"></a>エンティティ表示文字列のプログラムによる更新

コードでこれらを使用する方法を探している開発者は、表示文字列が [DisplayString](../../developer/common-data-service/reference/entities/displaystring.md) エンティティに格納されます。 

`DisplayString` エンティティには、既定の表示文字列は含まれません。 テキストを含むこのエンティティの 2 つの属性は、[CustomDisplayString](../../developer/common-data-service/reference/entities/displaystring.md#BKMK_CustomDisplayString) および [PublishedDisplayString](../../developer/common-data-service/reference/entities/displaystring.md#BKMK_PublishedDisplayString) です。 既定では、表示文字列がカスタマイズおよび公開されていない限り、これらの属性値は null です。 `PublishedDisplayString` 値は読み取り専用であり、現在公開済みの `CustomDisplayString` を表します。
 
## <a name="see-also"></a>関連項目
[エンティティの編集](edit-entities.md)<br />
[モデル駆動型アプリのローカライズ可能なテキストの変換](../model-driven-apps/translate-localizable-text.md)
