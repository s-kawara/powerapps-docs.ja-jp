---
title: モデル駆動型アプリの getNavigationBehavior (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 649fe7b0-016d-409f-ba3c-b14e0f1953e0
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getnavigationbehavior-client-api-reference"></a>getNavigationBehavior (クライアント API 参照)



[!INCLUDE[./includes/getNavigationBehavior-description.md](./includes/getNavigationBehavior-description.md)]

> [!NOTE]
> このメソッドは、[統一インターフェイス](/dynamics365/get-started/whats-new/customer-engagement/new-in-version-9#unified-interface-framework-for-new-apps) でのみ利用可能です。 

## <a name="syntax"></a>構文

```
stageObj.getNavigationBehavior().allowCreateNew = function () {
    return true|false;
}
```

## <a name="returns"></a>戻り値

**種類**: オブジェクト 

**説明**: クロス エンティティ 業務ビジネス フローのナビゲーション シナリオ内の entityA フォームから entityB のインスタンスを作成することができるように、ステージ内で **Create** ボタンが使用可能かどうか定義することができる `allowCreateNew` プロパティを持つオブジェクト。 

たとえば、これは取引先企業フォームから取引先担当者レコードを作成することができる、**AccountToContactProcess** サンプル業務プロセス フローの**提案作成**ステージにある**作成**ボタンです。

![](../../../../media/clientapi_getNavigationBehavior.png)

`allowCreateNew` プロパティは、クロス エンティティ ナビゲーションを実行しない業務プロセス フロー レコードに対して**未定義**を戻します。

## <a name="example"></a>例

次のサンプル コードは、名前に応じて業務ビジネス フローのアクティブなステージに対して、**作成**ボタンを非表示または表示する方法を示します。

```JavaScript
function sampleFunction(executionContext) {
    var formContext = executionContext.getFormContext();
    formContext.data.process.getActiveStage.getNavigationBehavior().allowCreateNew = function () {
        if (formContext.data.process.getName() === 'Test Process') {
            return false; // Create button is not available
        }
        else {
            return true; // Create button is available
        }
    }
}
```

### <a name="related-topics"></a>関連トピック
 
[formContext.data.process](../../formContext-data-process.md)

