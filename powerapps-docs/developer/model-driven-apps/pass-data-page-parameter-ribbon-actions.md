---
title: データをページからパラメーターとしてリボン操作に渡す (モデル駆動型アプリ) | Microsoft Docs
description: 'トピックでは、<CrmParameter> 要素を使用してこれらの値を取得するためのオプションについて説明します。 '
ms.custom: ''
ms.date: 02/15/2019
ms.reviewer: kvivek
ms.service: powerapps
ms.topic: article
author: hazhouMSFT
ms.author: hazhou
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="pass-data-from-a-page-as-a-parameter-to-ribbon-actions"></a>データをページからパラメーターとしてリボン操作に渡す

操作をリボン上に定義する場合、ページからデータを JavaScript 関数または URL に渡す処理が頻繁に必要とされます。 ここでは、[\<CrmParameter\>](https://msdn.microsoft.com/library/gg309332.aspx) 要素を使用してこれらの値を取得するためのオプションについて説明します。

## <a name="form-and-grid-context-in-ribbon-actions"></a>リボン アクションのフォームとグリッドのコンテキスト

実行コンテキスト (*フォーム コンテキスト*または*グリッドコンテキスト*) 情報をリボン操作の Javascript 関数に渡すには、リボン定義で `<CrmParameter>` 値として、フォーム コンテキストには **PrimaryControl**、グリッド コンテキストには **SelectedControl** を指定します。 **SelectedControl** は、サブグリッドおよびホームページ グリッドの両方に、グリッド コンテキストを渡します。 渡された **PrimaryControl** または**SelectedControl** の値は、それぞれ*フォーム コンテキスト*または*グリッド コンテキスト*の JavaScript 関数で引数として使用されます。 

たとえば、ここに **PrimaryControl** パラメーターを JavaScript 関数に渡す場所であるサンプル リボン定義があります:

```xml
<CommandDefinition Id="SampleCommand">
  <EnableRules/>
  <DisplayRules/>
  <Actions>
    <JavaScriptFunction Library="$webresource:new_mySampleScript.js" FunctionName="mySampleFunction">
      <CrmParameter Value="PrimaryControl" />
    </JavaScriptFunction>
  </Actions>
</CommandDefinition>
```

次に、上記のサンプルで参照される **new_mySampleScript.js** Web リソース ファイルで、**primaryControl** 変数を引数として指定して Javascript 関数を定義します。 この引数は、リボン コマンドが実行される場合は*フォーム* コンテキストを提供します。

```JavaScript
function mySampleFunction(primaryControl) {
    var formContext = primaryControl;
    // Perform operations using the formContext object
}
```

また、リボン定義で `<CrmParameter>` 値として **CommandProperties** を指定すると、リボン コントロールからイベントの詳細を渡すこともできます。 この機能を使用するとコンテキスト情報を中央機能に送信できるので、JavaScript 関数はイベントのコンテキストに基づいて、実行する操作を決めることができます。

> [!NOTE]
> リボン アクションでの JavaScript 関数用*フォーム コンテキスト*および*グリッド コンテキスト*の取得は、フォーム スクリプト内での取得方法とは異なります。 フォーム スクリプトおよび、これらのコンテキストを取得する方法については、「[クライアント API フォーム コンテキスト](clientapi/clientapi-form-context.md)」および「[クライアント API グリッド コンテキスト](clientapi/clientapi-grid-context.md)」を参照してください。

## <a name="form-values"></a>フォーム値

フォーム リボンに対しては、`data.entity`.[attributes](clientapi/reference/attributes.md) コレクションと `ui`.[controls](clientapi/reference/controls.md) コレクションを使用して、既知のフィールドから値を取得して設定できます。 

たとえば、次のサンプル コードは、取引先企業フォーム上の取引先企業名フィールドを取得し、取引先企業名の値に基づいて websiteurl フィールドに値を設定する方法を示しています。

```JavaScript
function mySampleFunction(primaryControl) {
    var formContext = primaryControl;    
    var accountName = formContext.getControl("name").getAttribute().getValue();    

    // Set the WebSiteURL field if account name contains "Contoso"
    if (accountName.toLowerCase().search("contoso") != -1) {
        formContext.getAttribute("websiteurl").setValue("http://www.contoso.com");
    }
    else {
        Xrm.Navigation.openAlertDialog({ text: "Account name does not contain 'Contoso'." });
    }
}
```

  
## <a name="grid-values"></a>グリッド値  
 `<CrmParameter>` 要素で使用可能な値の大半は、グリッドまたは階層グラフで表示されるデータを操作するためのものです。 `Value` 属性列挙オプションを使用すると、次のアイテムからアイテムを簡単に切り分けることができます。  
  
- **選択されているアイテム**  
  
    -   SelectedControlSelectedItemCount  
  
    -   SelectedControlSelectedItemIds  
  
    -   SelectedControlSelectedItemReferences  
  
- **すべての項目**  
  
    -   SelectedControlAllItemCount  
  
    -   SelectedControlAllItemIds  
  
    -   SelectedControlAllItemReferences  
  
- **選択されていないアイテム**  
  
    -   SelectedControlUnselectedItemCount  
  
    -   SelectedControlUnselectedItemIds  
  
    -   SelectedControlUnselectedItemReferences  
  
  これらのグループ分けごとに、アイテムの数や GUID 識別子を収集できます。 値を URL に渡している場合は、グリッド内のオブジェクトを一意に識別するために必要なすべての情報を格納した `EntityReference` オブジェクトも取得できます。 これらのパラメーターは、表示中のページがメイン グリッド (`HomepageGrid`) である場合とフォーム内のサブグリッドである場合のどちらにも適用されます。 `SelectedEntityTypeName` パラメーターと組み合わせて使用すると、別のアプリケーションに渡す必要がある情報がすべて入手できます。  
  
 
  
## <a name="other-context-information"></a>その他のコンテキスト情報  
 データ値のほかに、 [\<CrmParameter\>](https://msdn.microsoft.com/library/gg309332.aspx) を使用してクライアント コンテキスト情報を取得できます。  `CrmParameter` 要素の値として次のオプションを使用できます。`OrgName`、`OrgLcid`、および `UserLcid`。
 
 `<Url>` 操作を行う場合は、`PassParams` 属性を使用してコンテキスト情報を含めることもできます。  
  
 `Value` オプションの `PrimaryEntityTypeName` と `FirstPrimaryItemId` は、エンティティ レコードの情報を提供します。 `PrimaryItemIds` リボンの `HomepageGrid` を使用して、すべての表示中アイテムのリストを取得できます。
  
### <a name="see-also"></a>関連項目  
 [リボンのカスタマイズ](customize-commands-ribbon.md)   
 [リボンの使用による URL へのパラメーターの受け渡し](pass-parameters-url-by-using-ribbon.md)    
 [リボン アクションの定義](define-ribbon-actions.md)   
 [ユーザー定義のアクションによるリボンの変更](define-custom-actions-modify-ribbon.md)<br>
 [クライアントAPIフォームコンテキスト](clientapi/clientapi-form-context.md)<br>
 [クライアントAPIグリッドコンテキスト](clientapi/clientapi-grid-context.md)<br>
 
