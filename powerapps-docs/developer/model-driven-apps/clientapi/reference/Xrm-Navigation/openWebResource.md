---
title: モデル駆動型アプリにおける openWebResource (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 798dc921-1e80-42bc-b8ca-2056728bcba4
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="openwebresource-client-api-reference"></a>openWebResource (クライアント API 参照)



[!INCLUDE[./includes/openWebResource-description.md](./includes/openWebResource-description.md)]

## <a name="syntax"></a>構文

`Xrm.Navigation.openWebResource(webResourceName,windowOptions,data)`

## <a name="parameters"></a>パラメーター

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|webResourceName|String|あり|開く HTML Web リソースの名前。|
|windowOptions|オブジェクト|No|Web リソースを開くためのウィンドウ オプション。 オブジェクトには、次の属性が含まれています。<br/>- **height**: (任意) 数値。 開くウィンドウの高さ (単位はピクセル)。<br/>- **openInNewWindow**: ブール。 新しいウィンドウで Web リソースを開くかどうかを示します。<br/>- **width**: (任意) 数値。 開くウィンドウの幅 (単位はピクセル)。|
|data|String|No|データ パラメーターに渡されるデータ。|

## <a name="remarks"></a>備考

廃止された [Xrm.Utility.openWebResource](https://msdn.microsoft.com/library/jj602956.aspx#BKMK_OpenWebResource) 方式の代わりに、この方式を使用して Web リソースを表示する必要があります。

HTML Web リソースは、「[HTML Web リソースへのパラメーターの引き渡し](../../../webpage-html-web-resources.md#BKMK_PassingParametersToWebResources)」で説明されているパラメーター値を引き受けることができます。 この関数は、任意のデータ パラメーターの受け渡しのみを提供します。 その他の有効なパラメーターの値を渡すには、それらの値を `webResourceName` パラメーターに追加する必要があります。

> [!NOTE]
> **Xrm** オブジェクトは HTML Web リソースでは利用することができません。 したがって、`Xrm.*` メソッドを含むスクリプトは HTML Web リソースではサポートされません。 `parent.Xrm.*` は、HTML Web リソースがフォーム コンテナーに読み込まれた場合に機能します。 ただし、それ以外の場所では (たとえば、HTML Web リソースを SiteMap の一部として読み込んだ場合など)、`parent.Xrm.*` も機能しません。 詳細情報: [GetGlobalContext 関数および ClientGlobalContext.js.aspx](../GetGlobalContext-ClientGlobalContext.js.aspx.md)



## <a name="examples"></a>例

- “new_webResource.htm” という名前の HTML Web リソースを開きます。
   
   `Xrm.Navigation.openWebResource("new_webResource.htm");`

- HTML Web リソースを開き、windowOptions を設定します。

  ```
  var windowOptions = { openInNewWindow: true, height: 400, width: 400 }
  Xrm.Navigation.openWebResource("new_webResource.htm",windowOptions);
  ```

- `data` パラメーターのデータの単一アイテムを含む HTML Web リソースを開きます。

  `Xrm.Navigation.openWebResource("new_webResource.htm",null,"dataItemValue");`

 ### <a name="related-topics"></a>関連トピック

[Xrm.Navigation](../xrm-navigation.md)

