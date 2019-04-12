---
title: PowerApps のモデル駆動型アプリのメイン フォーム用 Web リソースのプロパティ | MicrosoftDocs
description: メイン フォームの Web リソースのプロパティについて
Keywords: メイン フォーム; Web リソースのプロパティ; Dynamics 365
author: Mattp123
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
ms.author: matp
manager: kvivek
ms.date: 06/27/2018
ms.service: powerapps
ms.topic: article
ms.assetid: 82cd41ea-95b0-4606-9e7d-43eb5ce9ecd6
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-resource-properties-for-model-driven-app-forms"></a>モデル駆動型アプリ フォームの Web リソースのプロパティ

アプリ ユーザーにとってさらに魅力的で便利になるように、フォーム上の Web リソースを追加または編集することができます。 Web リソースが可能なフォームは、イメージまたは HTML ファイル コントロールです。

> [!NOTE]
> Silverlight Web リソースは、廃止されたため、統一インターフェイス クライアントで機能しなくなります。

## <a name="access-web-resource-properties"></a>Web リソースのプロパティへのアクセス

フォームを表示している間:
- **Web リソースを追加するとき**: 挿入する場所のタブ (たとえば、**全般** または **メモ**) を選択し、**挿入** タブ上で **Web リソース** を選択します。<br />![Web リソースの挿入](media/insert-web-resource.png)
- **Web リソースを編集するとき**: フォーム タブと編集する Web リソースを選択し、**ホーム** タブで **プロパティの変更** を選択します。 <br />![Web リソース プロパティの変更](media/web-resource-change-properties.png)

これにより、**Web リソースの追加** または **Web リソースのプロパティ** ダイアログ ボックスが開きます。

![Web リソースを追加する](media/add-web-resource-dialog.png)


## <a name="web-resource-properties"></a>Web リソースのプロパティ

 **Web リソースの追加** ダイアログ ボックスまたは **Web リソースのプロパティ** ダイアログ ボックスには、Web リソースの種類に応じて、2 つまたは場合によっては 3 つのタブがあります。

### <a name="general-tab"></a>全般タブ

これらのプロパティは、使用する Web リソースとその動作を定義します。

|フィールド|説明|
|--|--|
|**Web リソース**|*必須。* 既存の Web リソースを検索するか、新しい Web リソースを作成します。 フォームのビジュアル要素として追加できる HTML およびイメージ Web リソースのみを含めるには、**フォームに対応した Web リソース** ビューを使用します。|
|**名前**|*必須。* フォームに追加される Web リソース コントロールの名前を指定します。 この値は、フォーム上のコントロールを一意に識別します。|
|**ラベル**|*必須。* **名前** フィールドの値に基づいて自動的に生成されます。 フォームに追加される Web リソース コントロールのローカライズ可能なテキストを指定します。 これが表示されるようにする場合は、**フォームでラベルを表示する** を選択します。|
|**既定で表示する**|これが有効になっているとき、フォームが読み込まれるとき Web リソースが表示されます。 必要に応じて Web リソースを表示する業務ルールまたはフォーム スクリプトがある場合、このフィールドのチェックを外します。 詳細情報: [フォーム要素を表示または非表示にする](visibility-options-legacy.md)|
|**モバイルの有効化**|この Web リソースがモバイル アプリに表示されるようにするには、このオプションを選択します。|

選択した Web リソースの種類に応じて、追加のプロパティを設定します。

HTML Web リソースの場合、以下を参照してください。

![HTML Web リソースのプロパティ](media/web-resource-general-html-properties.png)

|フィールド|説明|
|--|--|
|**カスタム パラメーター (データ)**|通常、`data` クエリ文字列パラメーターとして HTML Web リソースに渡される構成データです。 HTML ページに関連付けられたスクリプトは、このデータにアクセスし、ページの動作を変更するために使用することができます。|
|**サポートされている場合はクロスフレーム スクリプトを制限します**|HTML Web リソースのコンテンツを完全には信頼しない場合は、このオプションを使用します。 詳細情報: [開発者ドキュメント: クロスフレーム スクリプトを制限するかどうかを選択する](/dynamics365/customer-engagement/developer/use-iframe-and-web-resource-controls-on-a-form#select-whether-to-restrict-cross-frame-scripting)|
|**パラメータとして、レコードのオブジェクトの種類コードおよび一意の識別子を渡します。**|フォームに表示される現在のレコードに関するデータは、ページで実行されるスクリプトがレコードに関するデータにアクセスできるように、HTML Web リソース ページに渡すことができます。 詳細: <br />[Web リソースへのパラメーターの引き渡し](#pass-parameters-to-web-resources)<br />[開発者ドキュメント: レコードに関するコンテキスト情報を渡す](/dynamics365/customer-engagement/developer/use-iframe-and-web-resource-controls-on-a-form#pass-contextual-information-about-the-record)|

イメージ Web リソースの場合、すべてのユーザーがページにアクセスできるようにする支援技術にとって重要な **代替テキスト** を指定するオプションがあります。

<!-- TODO: Why are Custom Parameters available to pass to image web resources? -->

### <a name="formatting-tab"></a>[形式] タブ

**形式** タブでは、表示されるオプションは挿入された Web リソースの種類とそれが挿入されるコンテキストにより異なります。 これらのオプションには、表示列および行の数の指定、境界を表示するかどうかの指定、およびスクロール動作の指定が含まれます。

![Web リソースの形式のプロパティ](media/web-resource-formatting-properties.png)

|プロパティ|説明|  
|--------------|-----------------|
|**コントロールが使用する列数を指定してください**|Web リソースを含むセクションに複数の列があるとき、フィールドがセクションにある列の数まで占めるように設定できます。|  
|**コントロールが使用する行数を指定してください**|行の数を指定することで Web リソースの高さを制御したり、**自動拡張して、使用可能なスペースを広げます** を選択して Web リソースの高さを使用可能なスペースに拡張したりすることができます。|  
|**IFRAME のスクロールの種類を選択してください**|HTML Web リソースは、IFRAME を使用してフォームに追加されます。<br /><br /> - **必要に応じて**: Web リソースのサイズが使用できるサイズより大きい場合、スクロールバーが表示されます。<br />- **常に**: スクロールバーを常に表示します。<br />- **しない**: スクロールバーは表示されません。|  
|**境界の表示**|Web リソースの周りに境界を表示します。|  


### <a name="dependencies-tab"></a>[依存関係] タブ

Web リソースがスクリプトを使用してフォームのフィールドと対話することがあります。 フィールドがフォームから削除されると、Web リソースのスクリプトが破損することがあります。 Web リソースのスクリプトで参照されるフィールドはすべて**依存フィールド**に追加して、誤って削除されないようにします。

![Web リソースの依存関係のプロパティ](media/web-resource-dependency-properties.png)
  
<a name="BKMK_PassingParametersToWebResource"></a> 
 
## <a name="pass-parameters-to-web-resources"></a>Web リソースへのパラメーターの引き渡し 

HTML Web リソースは、クエリ文字列パラメーターとして渡されるパラメーターを受け入れることができます。  
  
レコードについての情報は、**パラメーターとして、レコードのオブジェクトの種類コードおよび一意の識別子を渡します**オプションを有効にすることで、渡すことができます。 情報が**カスタム パラメーター (データ)** フィールドに入力される場合、データ パラメーターを使用して渡されます。 渡される値は次のとおりです。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`data`|このパラメーターは、テキストが**カスタム パラメーター (データ)** に提供されている場合のみ渡されます。|  
|`orglcid`|組織の既定の言語の LCID。|  
|`orgname`|組織の名前。|  
|`userlcid`|ユーザーが指定した言語の LCID|  
|`type`|**これは使用しません。** エンティティの種類コード。 この数値は、異なる組織のユーザー定義エンティティでは異なります。 代わりにエンティティの種類名を使用します。|  
|`typename`|エンティティの種類名。|  
|`id`|レコードの ID 値。 エンティティ レコードを保存するまで、このパラメーターには値がありません。|  
  
そのほかのどのパラメーターも許可されないので、その他のパラメーターを使用しても Web リソースは開きません。 複数の値を渡す必要がある場合、データ パラメーターはさらにパラメーターを含めるとオーバーロードする可能性があります。

詳細情報: [開発者ドキュメント: レコードに関するコンテキスト情報を渡す](/dynamics365/customer-engagement/developer/use-iframe-and-web-resource-controls-on-a-form#pass-contextual-information-about-the-record)

### <a name="see-also"></a>関連項目

[Web リソースを作成または編集してアプリを拡張](create-edit-web-resources.md)<br />
[メイン フォームとそのコンポーネントの使用](use-main-form-and-components.md)
