---
title: モデル駆動型アプリの openForm (Client API reference) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 0206c43b-b1fc-490d-a867-1d75331885a8
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="openform-client-api-reference"></a>openForm (クライアント API 参照)



[!INCLUDE[./includes/openForm-description.md](./includes/openForm-description.md)]

## <a name="syntax"></a>構文

`Xrm.Navigation.openForm(entityFormOptions,formParameters).then(successCallback,errorCallback);`

## <a name="parameters"></a>パラメーター


<table style="width:100%">
  <tr>
    <th>Name</th>
    <th>種類​​</th> 
    <th>必須出席者</th>
    <th>内容</th>
  </tr>
  <tr>
    <td>entityFormOptions</td>
    <td>オブジェクト</td> 
    <td>あり</td>
    <td>フォームを開くためのエンティティ フォーム オプション。 オブジェクトには、次の属性が含まれています。<ul>
<li><b>cmdbar</b>: (任意) ブール値。 コマンド バーを表示するかどうかを指定します。 このパラメーターの値を指定しない場合、既定でコマンド バーが表示されます。</li>
<li><b>createFromEntity</b>: (任意) 検索。 マップした属性値に基づいて既定値を提供するレコードを指定します。 検索オブジェクトには、以下の文字列プロパティが含まれます。<code>entityType</code>、<code>id</code>、および<code>name</code> (任意)。</li>
<li><b>entityId</b>: (任意) 文字列。 フォームを表示するエンティティ レコードの ID。</li>
<li><b>entityName</b>: (任意) 文字列。 フォームを表示するエンティティの論理名。</li>
<li><b>formId</b>: (任意) 文字列。 表示するフォーム インスタンスの ID。</li>
<li><b>height</b>: (任意) 数値。 表示するフォーム ウィンドウの高さ (ピクセル単位)。</li>
<li><b>navBar</b>: (任意) 文字列。 サイト マップで定義されているエリアとサブエリアを使用して、ナビゲーション バーを表示するかどうか、およびアプリケーションのナビゲーションを使用可能にするかどうかを制御します。 有効な値は次のとおりです。"オン"、"オフ"、または "エンティティ"。<ul><li><code>on</code>: ナビゲーション バーが表示されます。 <b>navBar</b> パラメーターが使用されていない場合の既定の動作です。</li>
<li><code>off</code>: ナビゲーション バーは表示されません。 他のユーザー インターフェイス要素、または戻るボタンと進むボタンを使用して移動できます。</li><li><code>entity</code>: エンティティ フォームでは、関連するエンティティのナビゲーション オプションのみが利用可能です。 関連エンティティへの移動の後は、ナビゲーション バーに [戻る] ボタンが表示され、元のレコードに戻ることができます。</li></ul></li>
<li><b>openInNewwindow</b>: (任意) ブール値。 新しいウィンドウでフォームを表示するかどうかを示します。</li>
<li><b>windowPosition</b>: (任意) 数値。 画面でのフォームのウィンドウ位置に対して次のいずれかの値を指定します。<ul><li><code>1:center</code></li><li><code>2:side</code></li></ul>
<li><b>processId</b>: (任意) 文字列。 フォームに表示するビジネス プロセスの ID。</li>
<li><b>processInstanceId</b>: (任意) 文字列。 フォームに表示するビジネス プロセス インスタンスの ID。</li>
<li><b>relationship</b>: (任意) オブジェクト。 フォームに関連レコードを表示する関係オブジェクトを定義します。 オブジェクトには、次の属性があります。
<table style="width:100%">
  <tr>
    <th>Name</th>
    <th>種類​​</th> 
    <th>内容</th>
<tr>
<td>attributeName</td>
<td>String</td>
<td>関係で使用される属性の名前です。</td>
</tr>
<tr>
<td>名前</td>
<td>String</td>
<td>関係の名前。</td>
</tr>
<tr>
<td>navigationPropertyName</td>
<td>String</td>
<td>この関係のナビゲーション プロパティの名前。</td>
</tr>
<tr>
<td>relationshipType</td>
<td>数値</td>
<td>関係の種類。 次のいずれかの値を指定します。
<ul><li><code>0:OneToMany</code></li><li><code>1:ManyToMany</code></li></ul></td>
</tr>
<tr>
<td>roleType</td>
<td>数値</td>
<td>関係におけるロールの種類。 次のいずれかの値を指定します。
<ul><li><code>1:Referencing</code></li><li><code>2:AssociationEntity</code></li></ul></td>
</tr>
</table>
</li>
<li><b>selectedStageId</b>: (任意) 文字列。 ビジネス プロセス インスタンスで選択したステージの ID。</li>
<li><b>useQuickCreateForm</b>: (任意) ブール値。 簡易作成フォームを開くかどうかを示します。 これを指定しない場合、既定で <b>false</b> が渡されます。</li>
<li><b>width</b>: (任意) 数値。 表示するフォーム ウィンドウの幅 (ピクセル単位)。</li>
</ul>
</tr>
<tr>
<td>formParameters</td>
<td>オブジェクト</td>
<td>No</td>
<td>追加のパラメーターをフォームに渡すディクショナリ オブジェクト。 パラメーターが無効の場合、エラーが発生します。<br/><br/>フォームにパラメータを渡す方法の詳細については、「[フォームに渡すパラメーターを使用してフィールド値を設定する](../../../set-field-values-using-parameters-passed-form.md)」および「[カスタム クエリストリング パラメーターが許可されるフォームの構成](../../../configure-form-accept-custom-querystring-parameters.md) 」を参照してください。 </td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>いいえ</td>
<td>以下の場合に実行する関数:
<ul>
<li>既存のレコードのエンティティ フォームが表示される。</li>
<li>新しいレコードのために表示されるエンティティ フォームにレコードが保存される。</li>
<li>レコードが簡易作成フォームに保存される。</li>
</ul>
<b>メモ</b>: [統一インターフェイス](/dynamics365/get-started/whats-new/customer-engagement/new-in-july-2017-update#unified-interface-framework-for-new-apps)では、<b>successCallback</b> 関数は **openForm** メソッドを使用して開いた簡易作成フォームにレコードを保存するときにのみ実行されます。

この関数は、オブジェクトにパラメーターとして渡されます。 オブジェクトには、表示または作成されるレコード (複数) を識別するための以下のプロパティと共に <b>savedEntityReference</b> 配列があります。
<ul>
<li><b>entityType</b>: エンティティの論理名。</li>
<li><b>id</b>: レコードの GUID 値を表す文字列。</li>
<li><b>名前</b>: 表示または作成されるレコードの主属性値。</li></ul>

<b>メモ</b>: 既存のレコードのためまたはレコードを作成するためにフォームを開くとき、<b>savedEntityReferenceを</b> には一つのアイテムが含まれます。 簡易作成フォームを[統一インターフェイス](/dynamics365/get-started/whats-new/customer-engagement/new-in-july-2017-update#unified-interface-framework-for-new-apps)で開き、<b>保存して​​新規作成</b>をクリックして複数のレコードを作成するとき、<b>savedEntityReference</b> には複数のアイテムが含まれます。各アイテムは簡易作成フォームを使用して作成されたレコードを表します。
</td>
</tr>
<tr>
<td>errorCallback</td>
<td>関数</td>
<td>いいえ</td>
<td>処理が失敗したときに実行する関数。<br>

<b>メモ</b>: [統一インターフェイス](/dynamics365/get-started/whats-new/customer-engagement/new-in-july-2017-update#unified-interface-framework-for-new-apps)では、<b>errorCallback</b> 関数は簡易作成フォームを開いている場合にのみ実行されます。</td>
</tr>
</table>

## <a name="remarks"></a>備考

エンティティまたは簡易作成フォームを開くには、廃止された [Xrm.Utility.openEntityForm](https://msdn.microsoft.com/library/jj602956.aspx#openEntityForm) メソッドおよび [Xrm.Utility.openQuickCreate](https://msdn.microsoft.com/library/jj602956.aspx#openQuickCreate) メソッドの代わりに、このメソッドを使用する必要があります。
 

## <a name="examples"></a>例

### <a name="example-1-open-an-entity-form-for-existing-record"></a>例 1: 既存のレコードのエンティティ フォームを開く

次のサンプル コードは、既存の取引先担当者レコードを表示する取引先担当者フォームを開きます。

```JavaScript
var entityFormOptions = {};
entityFormOptions["entityName"] = "contact";
entityFormOptions["entityId"] = "8DA6E5B9-88DF-E311-B8E5-6C3BE5A8B200"

// Open the form.
Xrm.Navigation.openForm(entityFormOptions).then(
    function (success) {
        console.log(success);
    },
    function (error) {
        console.log(error);
    });
```

### <a name="example-2-open-an-entity-form-for-new-record"></a>例 2: 新しいレコードのエンティティ フォームを開く

次のサンプル コードは、新しいレコードを作成する、一部の値が事前に入力された取引先担当者フォームを開きます。

```JavaScript
var entityFormOptions = {};
entityFormOptions["entityName"] = "contact";

// Set default values for the Contact form
var formParameters = {};
formParameters["firstname"] = "Sample";
formParameters["lastname"] = "Contact";
formParameters["fullname"] = "Sample Contact";
formParameters["emailaddress1"] = "contact@adventure-works.com";
formParameters["jobtitle"] = "Sr. Marketing Manager";
formParameters["donotemail"] = "1";
formParameters["description"] = "Default values for this record were set programmatically.";

// Open the form.
Xrm.Navigation.openForm(entityFormOptions, formParameters).then(
    function (success) {
        console.log(success);
    },
    function (error) {
        console.log(error);
    });
```

### <a name="example-3-open-a-quick-create-form"></a>例 3: 簡易作成フォームを開く

次のサンプル コードは、一部の値が事前に入力された簡易作成の取引先担当者フォームを開きます。

```JavaScript
var entityFormOptions = {};
entityFormOptions["entityName"] = "contact";
entityFormOptions["useQuickCreateForm"] = true;

// Set default values for the Contact form
var formParameters = {};
formParameters["firstname"] = "Sample";
formParameters["lastname"] = "Contact";
formParameters["fullname"] = "Sample Contact";
formParameters["emailaddress1"] = "contact@adventure-works.com";
formParameters["jobtitle"] = "Sr. Marketing Manager";
formParameters["donotemail"] = "1";
formParameters["description"] = "Default values for this record were set programmatically.";

// Open the form.
Xrm.Navigation.openForm(entityFormOptions, formParameters).then(
    function (success) {
        console.log(success);
    },
    function (error) {
        console.log(error);
    });
```

### <a name="related-topics"></a>関連トピック

[Xrm.Navigation](../xrm-navigation.md)




