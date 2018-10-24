---
title: PowerApps におけるモデル駆動型アプリのメイン フォーム用の Web リソースのプロパティ | MicrosoftDocs
description: メイン フォーム用の Web リソースのプロパティについて
Keywords: Main form; Web resource properties; Dynamics 365
author: Mattp123
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
ms.author: matp
manager: kvivek
ms.date: 06/27/2018
ms.service: crm-online
ms.topic: article
ms.assetid: 82cd41ea-95b0-4606-9e7d-43eb5ce9ecd6
ms.openlocfilehash: a08ca32b1d300d4302064940e65fd1d067c3ade6
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39695574"
---
# <a name="web-resource-properties-for-model-driven-app-forms"></a>モデル駆動型アプリのフォーム用の Web リソースのプロパティ

アプリ ユーザーにとってさらに魅力的で便利になるように、フォーム上の Web リソースを追加または編集することができます。 フォームに対応した Web リソースは、イメージまたは HTML ファイルのコントロールです。

> [!NOTE]
> Silverlight の Web リソースは非推奨であり、統一インターフェイスのクライアントでは動作しません。

## <a name="access-web-resource-properties"></a>Web リソースのプロパティにアクセスする

フォームの表示中に次の操作を行います。
- **Web リソースを追加する場合**: その上に挿入するタブ (たとえば **[全般]** や **[メモ]**) を選択した後、**[挿入]** タブ上で **[Web リソース]** を選択します。<br />![Web リソースを挿入する](media/insert-web-resource.png)
- **Web リソースを編集する場合**: フォームのタブと編集する Web リソースを選択し、**[ホーム]** タブ上で **[プロパティの変更]** を選択します。 <br />![Web リソースのプロパティを変更する](media/web-resource-change-properties.png)

これにより **[Web リソースの追加]** または **[Web リソースのプロパティ]** ダイアログ ボックスが開きます。

![Web リソースの追加ダイアログ](media/add-web-resource-dialog.png)


## <a name="web-resource-properties"></a>Web リソースのプロパティ

 **[Web リソースの追加]** または **[Web リソースのプロパティ]** ダイアログ ボックスにはタブが 2 つ、場合によっては 3 つあります。これは Web リソースの種類によって異なります。

### <a name="general-tab"></a>[全般] タブ

これらのプロパティでは、使用する Web リソースとその動作方法を定義します。

|フィールド|説明|
|--|--|
|**Web リソース**|*必須。* 既存の Web リソースを検索するか、新規に作成します。 **[フォームに対応した Web リソース]** ビューを使用して、フォームに視覚要素として追加できる HTML およびイメージ Web リソースのみを含めます。|
|**Name**|*必須。* フォームに追加する Web リソース コントロールの名前を指定します。 この値によってフォーム内のコントロールが一意に識別されます。|
|**ラベル**|*必須。* **[名前]** フィールドの値に基づいて自動的に生成されます。 フォームに追加する Web リソース コントロールのローカライズ可能なテキストを指定します。 これを表示させる場合は **[フォームでラベルを表示する]** を選択します。|
|**既定で表示する**|これが有効なときは、フォームの読み込み時に Web リソースが表示されます。 必要に応じて Web リソースを表示するビジネス ルールやフォーム スクリプトがある場合は、このフィールドをオフにします。 詳細については、[フォーム要素の表示または非表示](visibility-options-legacy.md)に関する記事をご覧ください。|
|**モバイルの有効化**|この Web リソースがモバイル アプリで表示されるようにするには、このオプションを選択します。|

選択する Web リソースの種類に合わせて、その他のプロパティを設定します。

HTML Web リソースの場合は次が表示されます。

![HTML Web リソースのプロパティ](media/web-resource-general-html-properties.png)

|フィールド|説明|
|--|--|
|**カスタム パラメーター (データ)**|通常、構成データは、クエリ文字列パラメーター `data` として HTML Web リソースに渡されます。 HTML ページに関連付けられているスクリプトからこのデータにアクセスすることができます。これを利用してページの動作を変更します。|
|**Restrict cross-frame scripting where supported (サポートされている場合はクロスフレーム スクリプトを制限します)**|HTML Web リソースのコンテンツを完全に信頼していない場合は、このオプションを使用します。 詳細については、開発者向けドキュメント「[Select whether to restrict cross-frame scripting](/dynamics365/customer-engagement/developer/use-iframe-and-web-resource-controls-on-a-form#select-whether-to-restrict-cross-frame-scripting)」(クロスフレーム スクリプトを制限するかどうか選択する) をご覧ください。|
|**Pass record object-type code and unique identifier as parameters (パラメーターとして、レコードのオブジェクトの種類コードおよび一意の識別子を渡します)**|フォームに表示される現在のレコードに関するデータは、ページで実行中のスクリプトがそのデータにアクセスできるように HTML Web リソースに渡すことができます。 詳細情報: <br />[Web リソースにパラメーターを渡す](#pass-parameters-to-web-resources)<br />[開発者向けドキュメント: コンテキストに応じてレコードに関する情報を渡す](/dynamics365/customer-engagement/developer/use-iframe-and-web-resource-controls-on-a-form#pass-contextual-information-about-the-record)|

イメージ Web リソースの場合は**代替テキスト**を選択することができます。これは、ページをだれでもアクセスできるものにするための補助技術として重要です。

<!-- TODO: Why are Custom Parameters available to pass to image web resources? -->

### <a name="formatting-tab"></a>[書式設定] タブ

**[書式設定]** タブ上に表示されるオプションは、挿入する Web リソースの種類とそれを挿入したコンテキストによって変化します。 このオプションには、表示する列と行の数、境界を表示させるかどうか、スクロールの動作の指定などが含まれます。

![Web リソースの書式設定プロパティ](media/web-resource-formatting-properties.png)

|プロパティ|説明|  
|--------------|-----------------|
|**Select the number of columns the control occupies (コントロールが使用する列数を指定してください)**|Web リソースを含むセクションに複数の列がある場合は、最大でセクションの列数を占めるフィールドを設定できます。|  
|**Select the number of rows the control occupies (コントロールが使用する行数を指定してください)**|Web リソースの高さを制御するには、行数を指定するか、または **[Automatically expand to use available space]\(自動拡張し、空き領域を利用する\)** を選択して、使用可能な領域まで Web リソースの高さが拡張されるようにします。|  
|**IFRAME のスクロールの種類を選択する**|IFRAME を使用してフォームに HTML Web リソースが追加されます。<br /><br /> - **必要に応じて**: Web リソースが利用可能なサイズよりも大きい場合にスクロール バーを表示します。<br />- **常に**: 常にスクロール バーを表示します。<br />- **表示しない**: スクロール バーは表示されません。|  
|**境界の表示**|Web リソースの周りに境界を表示します。|  


### <a name="dependencies-tab"></a>[依存関係] タブ

Web リソースがスクリプトを使用してフォームのフィールドとやり取りしている場合があります。 フォームからフィールドが削除されると、Web リソース内のスクリプトが壊れる可能性があります。 Web リソースのスクリプトによって参照されているすべてのフィールドを**依存フィールド**に追加して、これらが誤って削除されないようにします。

![Web リソースの依存関係プロパティ](media/web-resource-dependency-properties.png)
  
<a name="BKMK_PassingParametersToWebResource"></a> 
 
## <a name="pass-parameters-to-web-resources"></a>Web リソースにパラメーターを渡す 

HTML Web リソースは、クエリ文字列パラメーターとして渡されるパラメーターを受け取ることができます。  
  
**[Pass record object-type code and unique identifiers as parameters]\(パラメーターとして、レコードのオブジェクトの種類コードおよび一意の識別子を渡します\)** オプションを有効にすることで、レコードに関する情報を渡すことができます。 情報が **[カスタム パラメーター (データ)]** フィールドに入力された場合は、データ パラメーターを使用して渡されます。 渡される値は次のとおりです。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`data`|このパラメーターが渡されるのは、**[カスタム パラメーター (データ)]** にテキストが指定された場合のみです。|  
|`orglcid`|組織の既定の言語の LCID です。|  
|`orgname`|組織の名前です。|  
|`userlcid`|ユーザーの優先する言語の LCID です。|  
|`type`|**これは使用しないでください。** エンティティ型のコードです。 この数値は、さまざまな組織のカスタム エンティティでは異なる場合があります。 代わりにエンティティ型の名前を使用します。|  
|`typename`|エンティティ型の名前です。|  
|`id`|レコードの ID 値です。 エンティティ レコードが保存されるまで、このパラメーターには値がありません。|  
  
その他のパラメーターは許可されていません。その他のパラメーターが使用されている場合、Web リソースは開きません。 複数の値を渡す必要がある場合は、データ パラメーターをオーバーロードしてその中により多くのパラメーターを含めることができます。

詳細については、開発者向けドキュメントの[コンテキストに応じてレコードに関する情報を渡す](/dynamics365/customer-engagement/developer/use-iframe-and-web-resource-controls-on-a-form#pass-contextual-information-about-the-record)に関する記事をご覧ください。

### <a name="see-also"></a>関連項目

[Web リソースを作成または編集してアプリを拡張する](create-edit-web-resources.md)<br />
[メイン フォームとそのコンポーネントを使用する](use-main-form-and-components.md)
