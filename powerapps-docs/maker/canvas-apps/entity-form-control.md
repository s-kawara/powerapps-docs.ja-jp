---
title: エンティティ フォーム コントロールの使用 | Microsoft Docs
description: エンティティ フォーム コントロールを使用して、Common Data Service エンティティに豊富なフォームを追加し、アプリをさらに短い期間で作成できます。
author: aneesmsft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 03/11/2017
ms.author: aneesa
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: ee8573cb9ae4df5ac42deefad4ac67aede3a3502
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42836279"
---
# <a name="use-the-entity-form-control"></a>エンティティ フォーム コントロールの使用
**エンティティ フォーム** コントロールを使用して、Common Data Service エンティティに豊富なフォームを追加し、アプリをさらに短い期間で作成できます。

**エンティティ フォーム** コントロールの概要については、「[New Entity form control (experimental feature) for Common Data Service](https://powerapps.microsoft.com/blog/new-entity-form-control-experimental-feature-for-common-data-service/)」 (Common Data Service の新しいエンティティ フォーム コントロール (試験的機能)) のブログ投稿をご覧ください。

> [!IMPORTANT]
> このブログ投稿で記載されているとおり、**エンティティ フォーム** コントロールの試験的な性質に注意してください。また、少なくとも現時点では、**エンティティ フォーム** コントロールの実稼働アプリでの使用については慎重に検討してください。

## <a name="key-properties"></a>主要なプロパティ
**エンティティ フォーム** コントロールの主要なプロパティは次のとおりです。

**DataSource** – 表示するレコードを含むデータ ソースを指定します。   
> [!NOTE]
> 現在、Common Data Service 内のエンティティのみが**エンティティ フォーム** コントロールのデータ ソースとしてサポートされています。  

**Pattern** – **エンティティ フォーム** コントロールで表示するフォームのスタイルを指定します。 **FormPattern** 列挙型を使用して、このプロパティを設定します。

* **FormPattern.List** – レコードの表形式のリストを表示します。
* **FormPattern.CardList** – レコードのカード リストを表示します。
* **FormPattern.Details** – 単一レコードの詳細を表示または編集するためのフォームを表示します。
* **FormPattern.None** – スタイルが明示的に指定されていません。 既定値はタブレット アプリは **List**、携帯電話アプリは **CardList** です。

**Item** – **エンティティ フォーム** コントロールが表示する必要のあるデータ ソース内のレコードを指定します。 このプロパティは、**Pattern** が **FormPattern.Details** に設定されている場合にのみ使用されます。

**Selected**– 現在選択されているレコードを取得します。  
例: **エンティティ フォーム**コントロールが販売注文レコードの一覧を表示する場合、**Selected** プロパティは現在選択されているレコードを指定します。 レコード内のフィールドにアクセスすることもできます。 (たとえば、選択したレコードの **Account** フィールドを **Selected.Account** として指定します。)

**SelectableFields** – どのフィールドがリンクとして表示される必要があるかを指定します。 次の構文を使用して、このプロパティの値を設定します。  
**{Field1Name : true, Field2Name : true}**  
例: フォームで **SalesOrderId** および **Account** フィールドをリンクとして表示するには、そのフォームの **SelectableFields** プロパティを次の値に設定します。  
**{SalesOrderId : true, Account : true}**

**SelectedField** – どのフィールドがクリックまたはタップされたかを特定します。 これは、**SelectableFields** として指定されたフィールドにのみ適用されます。  
例: **SelectableFields** プロパティを **{SalesOrderId : true, Account : true}** に設定し、ユーザーが **Account** フィールドをクリックまたはタップすると、**SelectedField.Account** が true に設定されます。

**OnFieldSelect** – ユーザーがフィールドをクリックまたはタップしたときのアプリの応答方法。 これは、**SelectableFields** として指定されたフィールドにのみ適用されます。

**Mode** – フォームのモードを決定します。 モードを変更するには、**ViewForm**、**EditForm**、または **NewForm** 関数を使用します。 これらの関数は、**Pattern** プロパティが **FormPattern.Details** に設定されている場合にのみ機能します。 **Mode** プロパティの値を **FormMode** 列挙型の値に設定します。

* **FormMode.View** – レコードを表示できますが、編集や追加はできません。
* **FormMode.Edit** – レコードを編集できます。
* **FormMode.New** – レコードを追加できます。

**OnSuccess** – データ操作が成功したときのアプリの応答方法。

**OnFailure** – データ操作が失敗したときのアプリの応答方法。

**Unsaved** – ユーザーが編集中のレコードに未保存の変更があるかどうかを特定します。

## <a name="related-functions"></a>関連する関数
**エンティティ フォーム** コントロールまたは[編集フォーム コントロール](functions/function-form.md)のいずれかで、次の共有関数を使用できます。 これらの関数は、**Pattern** プロパティが **FormPattern.Details** に設定されている場合にのみ**編集フォーム** コントロールで機能します。

**ViewForm** – **エンティティ フォーム** コントロールの **Mode** プロパティを **FormMode.View** に設定します。

**EditForm** – **エンティティ フォーム** コントロールの **Mode** プロパティを **FormMode.Edit** に設定します。

**NewForm** - **エンティティ フォーム** コントロールの **Mode** プロパティを **FormMode.New** に設定します。

**SubmitForm** - ユーザーが**エンティティ フォーム** コントロールのレコードを編集するときに、変更を保存します。

**ResetForm** - ユーザーが**エンティティ フォーム** コントロールでレコードを編集するときに、未保存の変更を破棄します。

さまざまなプロパティや関数の概要を説明しました。これ以降では、これらの操作について説明します。

> [!NOTE]
> Common Data Service データベースへのアクセス権がない場合は、以下の手順を行う前にアクセス権を取得してください。

## <a name="display-a-list-of-records"></a>レコードの一覧を表示する
次の 5 つの手順では、単一の、エンド ツー エンドの**エンティティ フォーム** コントロール使用方法の例を提供します。 この手順では、販売注文の一覧を表示するフォームを追加します。  

1. 空白のタブレット アプリを作成します。
   
    ![](media/entity-form-control/entityform-tutorial-01-01.png)
2. 最初の画面 **SalesOrderListScreen** の名前を変更します。
   
    ![](media/entity-form-control/entityform-tutorial-01-02.png)
3. **[挿入]** タブの **[フォーム]** をクリックまたはタップし、**[エンティティ フォーム (試験段階)]** をクリックまたはタップします。  
   
    **エンティティ フォーム** コントロールが画面に追加されます。  
   
    ![](media/entity-form-control/entityform-tutorial-01-03.png)
4. **エンティティ フォーム** コントロール **SalesOrderListForm** の名前を変更し、画面全体をカバーするサイズに変更します。
5. 右側のウィンドウで、テキスト **[データ ソースが選択されていません ]** の横にあるデータベース アイコンをクリックまたはタップしてから、**[データ ソースの追加]** をクリックまたはタップします。  
   
    ![](media/entity-form-control/entityform-tutorial-01-04.png)
6. 接続の一覧で、データベースの接続をクリックまたはタップします。  
   
    ![](media/entity-form-control/entityform-tutorial-01-05.png)
7. エンティティの一覧で、**[販売注文]** をクリックまたはタップしてから、**[接続]** をクリックまたはタップします。  
   
    **販売注文**エンティティのデータ ソースが作成され、**SalesOrderListForm** の **DataSource** プロパティがそのデータ ソースに設定されます。
   
    ![](media/entity-form-control/entityform-tutorial-01-06.png)  
   
    **エンティティ フォーム**コントロールが販売注文の一覧を表示します。 **エンティティ フォーム**コントロールを使用して、手動で構築することなく、リスト フォームをすばやく表示しました。
   
    ![](media/entity-form-control/entityform-tutorial-01-07.png)  
   
    **エンティティ フォーム** コントロールの **Pattern** プロパティを設定していないため、既定で **List** パターンになります。 さらに、**販売注文**エンティティの **DefaultList** フィールド グループが、リスト フォームの表示に使用されます。 また、フォームは動的であり、フィールド グループでの変更を自動的に反映します。


## <a name="display-the-details-of-a-record"></a>レコードの詳細を表示する
別の**エンティティ フォーム** コントロールを追加して、前に作成した一覧で選択されている販売注文の詳細を表示しましょう。  

1. **SalesOrderListForm** のサイズを、画面の半分をカバーするように変更し、2 つ目の**エンティティ フォーム** コントロールを追加して、画面のもう半分をカバーするようにします。  
   <br>![](media/entity-form-control/entityform-tutorial-01-09.png)
2. 2 つ目の**エンティティ フォーム** コントロール **SalesOrderDetailsForm** の名前を変更し、前に作成した**販売注文**データ ソースに接続します。  
   <br>![](media/entity-form-control/entityform-tutorial-01-10.png)
3. **SalesOrderDetailsForm** の **Pattern** プロパティを **FormPattern.Details** に設定します。  
   
    **SalesOrderDetailsForm** は、**販売注文**エンティティの **DefaultDetails** フィールド グループを使用して、フォームを表示します。 **SalesOrderListForm** と同様、フォームを手動で作成することなく、すばやくレコードの詳細を表示することができます。  
   
    ![](media/entity-form-control/entityform-tutorial-01-11.png)
4. **SalesOrderDetailsForm** の **Item** プロパティを **SalesOrderListForm.Selected** に変更します。
   
    **SalesOrderDetailsForm** は、ユーザーが **SalesOrderListForm** でクリックまたはタップするレコードの詳細を表示します。
   
    ![](media/entity-form-control/entityform-tutorial-01-12.png)
5. F5 を押してアプリをプレビューしてから、左側の一覧にある販売注文をクリックまたはタップします。  
   
    選択した注文の詳細は、右側に表示されます。  
   
    ![](media/entity-form-control/entityform-tutorial-01-13.png)  

## <a name="configure-a-field-to-navigate-to-another-screen"></a>別の画面に移動するためのフィールドの構成
次は、アプリにさらに画面を追加してから、**エンティティ フォーム** コントロールのフィールドを構成して、アプリでフィールドをクリックまたはタップしたときに、別の画面に移動するようにしましょう。  

1. 2 つ目の画面をアプリに追加し、画面 **SalesOrderDetailsScreen** の名前を変更します。
2. **SalesOrderDetailsForm** を切り取って **SalesOrderDetailsScreen** に貼り付け、上部のにあるアイコンのスペースを確保した状態で、画面の大部分がカバーされるようにフォームのサイズを変更します。
3. **SalesOrderDetailsScreen** の左上隅近くに、左向き矢印アイコンを追加します。
4. 左向き矢印アイコンの **OnSelect** プロパティを [**Back**](functions/function-navigate.md) 関数に設定します。  
   
    ![](media/entity-form-control/entityform-tutorial-01-14.png)
5. **SalesOrderListScreen** で、**SalesOrderListForm** のサイズを変更し、画面全体がカバーされるようにします。
6. **SalesOrderListForm** をクリックまたはタップして選択します。
7. 右側のウィンドウの **[フィールド]** の下で、**SalesOrderId** を設定して **SalesOrderDetailsScreen** に移動するようにします。  
   
    ![](media/entity-form-control/entityform-tutorial-01-15.png)
   
    **エンティティ フォーム** コントロールが **SalesOrderId** フィールド (一覧の最初の列) の値ををリンクとして表示します。
   
    ![](media/entity-form-control/entityform-tutorial-01-16.png)  
8. F5 を押してアプリをプレビューしてから、販売注文の一覧にあるリンクをクリックまたはタップします。
   
    ![](media/entity-form-control/entityform-tutorial-01-17.png)  
   
    2 つ目の画面が開き、指定した販売注文の詳細が表示されます。
   
    ![](media/entity-form-control/entityform-tutorial-01-18.png)  
   
    別の販売注文の詳細を表示するには、左向き矢印をクリックまたはタップして一覧に戻り、詳細を表示する注文のリンクをクリックまたはタップします。

## <a name="navigate-with-a-context-variable"></a>コンテキストの変数を使用した移動
**SalesOrderDetailsForm** の **Item** プロパティは、ユーザーが **SalesOrderListForm** で選択したレコードの詳細が **SalesOrderDetailsForm** で表示されるように **SalesOrderListForm.Selected** に設定されています。 移動するフィールドを構成するためにフォームのカスタマイズ ウィンドウを使用するときに自動的に作成される **NavigationContext** コンテキストの変数を使用して、選択したレコードのコンテキストを取得することもできます。  

1. **SalesOrderDetailsForm** の **Item** プロパティを **SalesOrderListForm.Selected** に変更します。
   
    ![](media/entity-form-control/entityform-tutorial-01-19.png)
2. F5 を押してアプリをプレビューしてから、販売注文の一覧にあるリンクをクリックまたはタップします。
   
    **SalesOrderDetailsScreen** が開き、指定した販売注文の詳細が表示されます。

フォームのカスタマイズ ウィンドウによってどのように移動とコンテキストが設定されるかを見てみましょう。  

**SalesOrderListForm** の **SelectableFields** プロパティは、**SalesOrderId** を選択可能なフィールドとして指定します。

![](media/entity-form-control/entityform-tutorial-01-20.png)  

これは、フォームのカスタマイズ ウィンドウを使用して **SalesOrderId** フィールドを **SalesOrderDetailsScreen** に移動するようにしたときに、自動的に設定されています。 そのため、**SalesOrderId** フィールド内の値がリンクとして表示されます。

**SalesOrderListForm** の **OnFieldSelect** プロパティは [**If**](functions/function-if.md) 関数に設定され、これによりユーザーが**販売注文 ID**フィールド: **SalesOrderListForm.SelectedField.SalesOrderId = true** をクリックするかタップするかが決定されます。  

この関数が true として評価される場合、**SalesOrderDetailsScreen** は以前使用した **NavigationContext** というコンテキストの変数で開きます。  

これもすべて、フォームのカスタマイズ ウィンドウを使用して **SalesOrderId** フィールドを **SalesOrderDetailsScreen** に移動するようにしたときに、自動的に設定されています。  

そのため、販売注文 ID フィールドをクリックまたはタップすると、[**If**](functions/function-if.md) 関数が true に評価され、[**Navigate**](functions/function-navigate.md) 関数が対応するコンテキストで呼び出されて詳細画面が開きます。  

![](media/entity-form-control/entityform-tutorial-01-21.png)  

> [!NOTE]
> フォームのカスタマイズ ウィンドウを使用すると、**NavigationContext** が適切に決定されます。 ユーザーが **SalesOrderId** をクリックまたはタップすると、以前の数式と同様に **NavigationContext** が **SalesOrderListForm.Selected** に設定されます。 代わりに、移動に **Account** フィールドが指定されている場合は、**NavigationContext** が **SalesOrderListForm.Selected.Account** に設定されており、正しいコンテキストが渡されます。 ただし、そのコンテキストを使用するには、**エンティティ フォーム** コントロールが Common Data Service の **Account** エンティティに接続されている必要があります。

## <a name="edit-and-save-a-record"></a>レコードの編集および保存
最後に、**エンティティ フォーム** コントロールでレコードを編集し、保存する方法について見てみましょう。  

1. **SalesOrderDetailsScreen** で、編集アイコンを追加してから、その **OnSelect** プロパティを次の数式に設定します。  
   **EditForm(SalesOrderDetailsForm)**
   
    ![](media/entity-form-control/entityform-tutorial-01-22.png)
2. 編集アイコンの隣にチェックマーク アイコンを追加し、チェックマーク アイコンの **OnSelect** プロパティを次の数式に設定します。  
   **SubmitForm(SalesOrderDetailsForm)**  
   
    ![](media/entity-form-control/entityform-tutorial-01-23.png)
3. F5 キーを押してアプリをプレビューし、**販売注文 ID** リンクをクリックまたはタップして販売注文の詳細を表示してから、編集アイコンをクリックまたはタップします。  
   
    レコードを編集できるように、**エンティティ フォーム** コントロールの **Mode** が **FormMode.Edit** に設定されています。
4. **[注文状況]** を **[請求書]** に更新します。  
   
    ![](media/entity-form-control/entityform-tutorial-01-24.png)
5. **[販売担当者]** を **[WRK014]** に更新します。
   
    **[販売担当者]** の選択をサポートするため、**エンティティ フォーム** コントロールによって自動的に詳細な検索がレンダリングされます。 この検索を生成および表示するため、このコントロールでは Common Data Service の**ワーカー**エンティティの **DefaultLookup** フィールド グループが使用されます。 **[販売担当者]** フィールドの種類が **[ワーカー]** であるため、**ワーカー** エンティティが使用されます。
   
    ![](media/entity-form-control/entityform-tutorial-01-25.png)
6. チェックマーク アイコンをクリックまたはタップして、変更を保存します。

アプリで**エンティティ フォーム** コントロールを使用する方法について説明したこの記事は、この手順で終了です。 ここでご紹介した情報が**エンティティ フォーム** コントロールの使用を始めるときにお役に立てば幸いです。 **エンティティ フォーム** コントロール、およびアプリに豊富なフォームを追加する方法に関してご提供した情報についてのご意見をお待ちしております。

