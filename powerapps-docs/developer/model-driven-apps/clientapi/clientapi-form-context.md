---
title: モデル駆動型アプリにおけるクライアント API フォーム コンテキスト | Microsoft Docs
ms.date: 04/10/2019
ms.service: powerapps
ms.topic: conceptual
applies_to:
  - Dynamics 365 (online)
ms.assetid: 0cf94e8d-801a-451f-98c3-130e912f963b
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="client-api-form-context"></a>クライアントAPIフォームコンテキスト



クライアント API フォーム コンテキスト (**formContext**) は、フォームまたは、現在のコードが実行される、簡易表示コントロールまたは編集可能グリッドの列などの、フォーム上のアイテムへの参照を提供します。

先に、 **Xrm.Page** のグローバル オブジェクトがフォームまたはフォームのアイテムを示すのに使用されます。 最新バージョンで、**Xrm.Page** オブジェクトが [廃止](/dynamics365/get-started/whats-new/customer-engagement/important-changes-coming#some-client-apis-are-deprecated) され、適切なフォームまたはフォームのアイテムに参照を返す実行コンテキスト オブジェクトに渡される [getFormContext](reference/executioncontext/getFormContext.md) メソッドを使用する必要があります。 

> [!IMPORTANT]
> *Deprecated* はモデル駆動型アプリの将来の主要なリリースからフィーチャまたは機能が削除されることを意味します。フィーチャまたは機能は正式に削除されるまでの間、引き続き機能して完全にサポートされます。 公表は、この文書、公式ブログ、および他の多くの場所で、削除の少なくとも 6 ヶ月前に行われます。<br/><br/>プライマリ フォームのコンテンツへの静的なアクセスとして **Xrm.Page** オブジェクトを使用することにより、既存のスクリプトとの下位互換性の維持は*依然として*サポートされ、他の一部のクライアント API メソッドが [クライアント API の非推奨](/dynamics365/get-started/whats-new/customer-engagement/important-changes-coming#some-client-apis-are-deprecated) セクションに一覧表示されても直ぐに削除されません。 マイクロソフトは、使用可能な限り対象になるバージョン 9.0 または以降で、コードでは**Xrm.Page**オブジェクトの代わりに新しい**formContext**オブジェクトの使用を強く推奨します。 さらに**formContext**オブジェクトを使用すると、コールされる場所に応じてフォーム上または編集可能グリッド上のいずれかで操作することができる、共通イベント ハンドラーの作成が可能になります。 詳細については、[getFormContext (クライアント API 参照)](reference/executioncontext/getFormContext.md)を参照してください。<br><br>リボン アクションでの JavaScript 関数用 **formContext** オブジェクトの取得は、フォーム スクリプト内での取得方法とは異なります。 詳細については、[リボン アクションのフォームとグリッドのコンテキスト](../pass-data-page-parameter-ribbon-actions.md#form-and-grid-context-in-ribbon-actions)を参照してください。

## <a name="using-the-formcontext-object-instead-of-the-xrmpage-object"></a>Xrm.Pageオブジェクトの代わりに、formContextオブジェクトを使用する 

**Xrm.Page** の既存のコードを容易に変換して、新しい **formContext** オブジェクトを使用することができます。 たとえば、 **Xrm.Page** オブジェクトを使用する次のスクリプトを考えてみてください:

```JavaScript
function displayName()
{
    var firstName = Xrm.Page.getAttribute("firstname").getValue();
    var lastName = Xrm.Page.getAttribute("lastname").getValue();
    console.log(firstName + " " + lastName);
}
```

静的な **Xrm.Page** オブジェクトを使用する代わりに、実行コンテキストに渡されるオブジェクトを使用して **formContext** オブジェクトを取得する、更新されたスクリプトがあります:

```JavaScript
function displayName(executionContext)
{
    var formContext = executionContext.getFormContext(); // get formContext

    // use formContext instead of Xrm.Page  
    var firstName = formContext.getAttribute("firstname").getValue(); 
    var lastName = formContext.getAttribute("lastname").getValue();
    console.log(firstName + " " + lastName);
}
```

>[!IMPORTANT]
>**formContext** オブジェクトを使用してイベント ハンドラーを定義するときは、**ハンドラーのプロパティ**ダイアログの**実行コンテキストを最初のパラメーターとして渡す**オプションを選択する必要があります。 詳細については、「[クライアント API 実行コンテキスト](clientapi-execution-context.md)」を参照してください。

## <a name="formcontext-object-model"></a>formContext オブジェクト モデル

モデル駆動型アプリのデータおよびユーザー インターフェイス要素をプログラムで処理するために、**formContext** オブジェクトの下で**データ**および **ui** オブジェクトを使用します。

![formContext オブジェクト モデル](../media/ClientAPI-formContextModel.png)

### <a name="data-object"></a>データ オブジェクト

業務プロセス フローのコントロールに加えて、エンティティのデータへのアクセスと、フォーム内のデータを管理するメソッドを提供します。 以下のオブジェクトを含みます:

| **オブジェクト**  | **説明**|
|-----------------|----------------|
|エンティティ|ページに表示されるレコードに固有の情報を取得するメソッド、save メソッド、およびフォーム上に含まれるすべての属性のコレクションを提供します。|
|プロセス|業務プロセス フローのプロパティを取得するメソッドを提供します。|

また、非エンティティのバインドされるコントロールにアクセスするための**属性**コレクションを提供します。 このトピックの後の方にある **formContextオブジェクト モデルのコレクション**セクションを参照してください。

詳細: [formContext.data](reference/formContext-data.md) 

### <a name="ui-object"></a>UI オブジェクト

ユーザー インターフェイスに関する情報を取得するメソッド、およびフォームまたはグリッドのいくつかのサブ コンポーネントのコレクションを提供します。 以下のオブジェクトを含みます:

| **オブジェクト**  | **説明**|
|-----------------|----------------|
|formSelector|現在のユーザーが利用できるフォームを問い合わせる機能を提供するアイテムコレクションを提供します。 現在のフォームを閉じ、別のフォームを開くには、操作メソッドを使用します。|
|ナビゲーション|メソッドを含みません。 アイテムのコレクションによってナビゲーション アイテムへのアクセスを提供します。 詳細については、コレクションの次のセクションを参照してください。|
|プロセス|フォームの業務プロセス フローのコントロールを操作するためのメソッドを提供します。|

詳細: [formContext.ui](reference/formContext-ui.md)

## <a name="collections-in-the-formcontext-object-model"></a>formContextオブジェクト モデルのコレクション

次の表に、 **Xrm** オブジェクト モデルのコレクションを示します。 一般にコレクションに使用できるメソッドの詳細については、「 [コレクション (クライアント API 参照)](reference/collections.md)」を参照してください。

| **集荷**  | **説明**|
|-----------------|----------------|
| [attributes](reference/attributes.md)  | 二つのオブジェクトには属性コレクションが含まれます:<br/><br/>- **formContext.data.attributes** コレクションは、非エンティティのバインドされる属性へのアクセスを提供します。<br/><br/>- **formContext.data.entity.attributes** コレクションは、フォームで利用できる各エンティティ属性へのアクセスを提供します。 フォームに追加されるフィールドに対応する属性のみを利用できます。| 
| [controls](reference/controls.md)  | 次の 3 つのオブジェクトに、controls コレクションが含まれます。<br/><br/> - **formContext.ui.controls**: フォームに存在する各コントロールへのアクセスを提供します。<br/><br/>- **formContext.data.entity.attribute.controls**: 属性がフォーム上のコントロールを複数持つ場合があるため、このコレクションは各コントロールへのアクセスを提供します。 属性のコントロールがフォームに複数追加されている場合を除き、このコレクションにはアイテムが 1 つしか含まれません。<br/><br/>- **formContext.ui.tabs.sections.controls**: このコレクションには、セクションで見つかるコントロールしか含まれません。|
|**formContext.data.process.**[ステージ](reference/formContext-data-process/process/getStages.md) および **formContext.data.process**.[ステップ](reference/formContext-data-process/stage/getSteps.md)| 業務プロセス フロー内のステージおよびステップコレクションへのアクセスを提供します。 また、これらにより、コレクションからアイテムの追加および削除ができます。|
|**formContext.ui.formSelector.**[アイテム](reference/formContext-ui-formselector.md)|複数のフォームが 1 つのエンティティに提供されている場合、各フォームをセキュリティ ロールに関連付けることができます。 ユーザーに関連付けられているセキュリティ ロールによって、ユーザーに複数のフォームを表示できる場合、 **formContext.ui.formSelector.items** コレクションはそのユーザーが利用できる各フォーム定義へのアクセスを提供します。|
|**formContext.ui.navigation.**[アイテム](reference/formContext-ui-navigation.md)|**formContext.ui.navigation.items** コレクションは、フォーム エディターのナビゲーション領域を使用して定義されているナビゲーション アイテムへのアクセスを提供します。 コマンド バーを使用して、これらに移動します。|
| **formContext.ui.**[quickForms](reference/formContext-ui-quickForms.md) | Customer Enagagement フォームのすべての簡易ビューコントロールおよびその構成コントロールにアクセスするためのメソッドを提供します。| **Xrm.Page.ui.tabs** コレクションは、これらの各タブへのアクセスを提供します。|
| **formcontext.ui.tabs**[タブ](reference/formContext-ui-tabs.md) | 1 つ以上のタブを使用して、各フォームを整理できます。 このコレクションは、これらの各タブへのアクセスを提供します。|
| **formcontext.ui.tabs**[セクション](reference/formContext-ui-sections.md) | 1 つ以上のセクションを使用して、各フォーム タブを整理できます。 タブ**セクション**コレクションは、これらの各セクションへのアクセスを提供します。|


  
### <a name="related-topics"></a>関連トピック

[getFormContext メソッド](reference/executioncontext/getFormContext.md)<br/>
[getGlobalContext メソッド](reference/xrm-utility/getGlobalContext.md)<br/>
[実行コンテキストのメソッド](reference/execution-context.md) 

 

