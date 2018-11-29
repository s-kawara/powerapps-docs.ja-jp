---
title: リボンの使用による URL へのパラメーターの受け渡し (モデル駆動型アプリ) | Microsoft Docs
description: リボンの使用による URL へのパラメーターの受け渡しについて説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="pass-parameters-to-a-url-by-using-the-ribbon"></a>リボンの使用による URL へのパラメーターの受け渡し

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/pass-parameters-url-by-using-ribbon -->

リボン アクションは、`<CommandDefinition>` 要素の `<Actions>` 要素に定義されます。 リボンを使用してモデル駆動型アプリのコンテキスト情報をクエリ文字列パラメーターとして URL に渡す方法はいくつかあります。  
  
-   `<Url>` 要素を使用します。 `Url` 要素内で、**PassParams** 属性を使用します。  
  
-   `<Url>` 要素と `<CrmParameter>` 要素を一緒に使用します。 `Url` 要素から使用する場合は、名前属性の値を設定する必要があります。  
  
-   `<JavaScriptFunction>` 要素と `<CrmParameter>` 要素を一緒に使用します。  
  
## <a name="use-the-passparams-attribute-to-set-dynamic-values"></a>PassParams 属性を使用して動的な値を設定する  
 ターゲットのアプリケーションは、**PassParams** 属性を使用してターゲット URL に渡されたパラメーターから、レコードまたはユーザーのコンテキストについての情報を受け取ります。 **PassParams** 属性を使用してリボン コントロールを構成している場合、すべてのパラメーターが渡されます。 渡されるパラメーターを次の表に示します。  
  
|パラメーター|名前|説明|  
|---------------|----------|-----------------|  
|`typename`|エンティティ名|エンティティの名前です。 ユーザー定義エンティティの場合、名前にはカスタマイズの接頭辞 (new_entityname など) が含まれます。|  
|`type`|エンティティの種類コード|現在の組織内のエンティティを一意に識別する整数です。 **注:** `Entity Type Code` 値は、組織でエンティティが作成された順序によって決まります。 ユーザー定義エンティティの `Entity Type Codes`は、通常、組織が違うと異なります。|  
|`id`|オブジェクトの GUID|レコードを表すグローバル一意識別子 (GUID) です。|  
|`orgname`|組織名|組織の一意の名前です。|  
|`userlcid`|ユーザー言語コード|現在のユーザーが使用する言語コードの識別子です。|  
|`orglcid`|組織言語コード|組織の基本言語を表す言語コードの識別子です。|  
  
[!INCLUDE[languagecode](../../includes/languagecode.md)]
  
> [!NOTE]
>  エンティティの種類コードではなく、エンティティ名を使用することをお勧めします。エンティティの種類コードは MDA のインストール環境間で異なることがあります。  
  
### <a name="example"></a>例  
 次のサンプルは、パラメーターのない URL の表示方法を示しています。  
  
```  
http://myserver/mypage.aspx  
```  
  
 次のサンプルは、ユーザーの言語および組織の基本言語が英語で、取引先企業レコードの GUID が DBD5DBFB-0666-DC11-A5D9-0003FF9CE217 であるときに、"AdventureWorksCycle" という組織の、取引先企業エンティティに対するリボン コントロールを表示する場合に含めるパラメーターを示しています。  
  
```  
http://myserver/mypage.aspx?orgname=AdventureWorksCycle&userlcid=1033&orglcid=1033&type=1&typename=account&id=%7BDBD5DBFB-0666-DC11-A5D9-0003FF9CE217%7D  
```  
  
## <a name="use-a-querystring-parameter-in-the-url"></a>URL での Querystring パラメーターの使用  
 URL 属性には `querystring` パラメーターを含めることができます。 これは、「[URL を使用してフォーム、ビュー、ダイアログ、およびレポートを開く](open-forms-views-dialogs-reports-url.md)」の説明に従って特定のレコードやビューを開く場合に非常に役立ちます。  
  
> [!NOTE]
>  URL で複数の `querystring` パラメーターの区切り文字としてアンパサンド文字 (&) が使用されている場合は、リボンをインポートできません。 この文字を使用すると、XML が無効になります。 "&amp;" を含む URL 属性の値では、アンパサンド文字をエスケープする必要があります。  
  
## <a name="reading-passed-parameters"></a>渡されたパラメーターの読み取り  
 渡されたパラメーターは、通常、`HttpRequest.QueryString` プロパティを使用して、ターゲットの .aspx ページに読み込まれます。 詳細: [HttpRequest.QueryString プロパティ](https://msdn.microsoft.com/library/system.web.httprequest.querystring.aspx)  
  
> [!NOTE]
>  URL のターゲットが Web リソースの場合は、トピック「[HTMLWeb リソースへのパラメーターの引き渡し](webpage-html-web-resources.md#BKMK_PassingParametersToWebResources)」に指定されているパラメーターのみを使用できます。 ユーザー定義値を渡す方法は、`data` パラメーターにその値を含める方法のみです。 1 つのパラメーターに複数の値を含めるには、特殊な処理が必要です。 詳細: [Sample: サンプル: データ パラメーターを使用した Web ページの Web リソースへの複数の値の引き渡し](sample-pass-multiple-values-web-resource-through-data-parameter.md)  
  
### <a name="see-also"></a>関連項目

 [コマンド、およびリボンをカスタマイズする](customize-commands-ribbon.md)   
 [URL を使用してフォームおよびビューを開く](open-forms-views-dialogs-reports-url.md)    
 [リボン タブ表示ルールを定義する](define-ribbon-tab-display-rules.md)   
 [サンプル: リボン定義をエクスポートする](sample-export-ribbon-definitions.md)


