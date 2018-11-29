---
title: モデル駆動型アプリの GetGlobalContext 関数および ClientGlobalContext.js.aspx| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: conceptual
applies_to:
  - Dynamics 365 (online)
ms.assetid: b58e6173-e3cd-4a3b-b39a-334c295503ec
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getglobalcontext-function-and-clientglobalcontextjsaspx-client-api-reference"></a>GetGlobalContext 関数および ClientGlobalContext.js.aspx (クライアント API 参照)



特定のクライアント、組織、または モデル駆動型アプリ インスタンスのユーザーなどへのグローバル コンテキスト情報に対するアクセス権を取得するために、[Web リソース](../../web-resources.md) でプログラミングをするときは、**GetGlobalContext** 関数を使用します。 

HTML Web リソース内の **GetGlobalContext** 関数に対するアクセス権を取得するには、**ClientGlobalContext.js.aspx** への参照を含めます。

> [!NOTE]
> **ClientGlobalContext.js.aspx** への参照を含めても **Xrm** オブジェクトは HTML Web リソースでは利用可能になりません。 したがって、`Xrm.*` メソッドを含むスクリプトは HTML Web リソースではサポートされません。 `parent.Xrm.*` は、HTML Web リソースがフォーム コンテナーに読み込まれた場合に機能します。 ただし、それ以外の場所では (たとえば、HTML Web リソースを SiteMap の一部として読み込んだ場合など)、`parent.Xrm.*` も機能しません。

## <a name="getglobalcontext-function"></a>GetGlobalContext 関数

**GetGlobalContext** 関数は **Xrm.Utility.getGlobalContext** メソッドが戻すのと同じコンテキスト オブジェクトを戻します。これは、そのコンテキスト オブジェクトに **Xrm.Utility.getGlobalContext** で利用可能なものと同じプロパティおよびメソッドがあることを意味します。 詳細: Xrm.Utility.[getGlobalContext](Xrm-Utility/getGlobalContext.md)

## <a name="clientglobalcontextjsaspx"></a>ClientGlobalContext.js.aspx

**GetGlobalContext** 関数を使用することができるようにするには、Web リソース ディレクトリのルートにある **ClientGlobalContext.js.aspx** ページへの参照を含める必要があります。

- フォルダー構造をシミュレートするために HTML Web リソース名にバックスラッシュ文字を使用していない場合、直接参照することによりこのスクリプトをページに含めることができます。 たとえば、次のようになります。

    ```HTML
    <head>
      <title>HTML Web Resource</title>
      <script src="ClientGlobalContext.js.aspx" type="text/javascript" ></script>
      
    </head>
    ```
- ディレクトリ構造をシミュレートするために HTML Web リソース名にバックスラッシュ文字を使用している場合、スクリプト要素にこれを反映する必要があります。 以下のものは、**sdk_/Styles/ContosoStyles.css** という名前の CSS Web リソースを使用する、**sdk_/Contoso.htm** という名前の HTML Web リソースおよび **sdk_/Scripts/ContosoScript.js** という名前の JavaScript Web リソースの例です。

    ```HTML
    <head>
      <title>HTML Web Resource</title>
      <script src="../ClientGlobalContext.js.aspx" type="text/javascript" ></script>

      <script src="Scripts/ContosoScript.js" type="text/javascript"></script>
      <link href="Styles/ContosoStyles.css" rel="stylesheet" type="text/css" />
    </head>

    ```

> [!NOTE]
> /WebResources/ClientGlobalContext.js.aspx などのルート WebResources フォルダーを含む相対パスを使用することは推奨されません。マルチ テナント環境ではページから組織コンテンツが失われる可能性があります。

**ClientGlobalContext.js.aspx** ページには一部のグローバル イベント ハンドラーが含まれます。 これらのイベント ハンドラーは、[onselectstart](https://developer.mozilla.org/en-US/docs/Web/Events/selectstart)、[contextmenu](https://developer.mozilla.org/en-US/docs/Web/Events/contextmenu)、および [ondragstart](https://developer.mozilla.org/en-US/docs/Web/Events/dragstart)イベントをキャンセルします。 

### <a name="related-topics"></a>関連トピック

[Xrm.Utility.getGlobalContext](Xrm-Utility/getGlobalContext.md)

[クライアント API オブジェクト モデルについて](../understand-clientapi-object-model.md) 

[モデル駆動型アプリのための Web リソース](../../web-resources.md)

