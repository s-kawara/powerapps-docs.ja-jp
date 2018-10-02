---
title: PowerApps のモデル駆動型アプリのメイン フォーム用簡易表示コントロールのプロパティ | MicrosoftDocs
description: メイン フォーム用簡易表示コントロールのプロパティについて
Keywords: Quick view control properties; Dynamics 365; Main forms
author: Mattp123
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
ms.author: matp
manager: kvivek
ms.date: 06/06/2018
ms.service: crm-online
ms.topic: article
ms.assetid: 68f68d5b-6c71-4b95-bb46-d48c59d9008e
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="model-driven-app-quick-view-control-properties"></a>モデル駆動型アプリの簡易表示コントロールのプロパティ

モデル駆動型アプリ フォームの簡易表示コントロールには、フォーム内の検索フィールドで選択されたレコードのデータが表示されます。 コントロールに表示されるデータは、簡易表示フォームを使用して定義されます。 表示されたデータは編集できませんが、主フィールドが簡易表示フォームに含まれると、関連のレコードを開くリンクになります。 詳細: [簡易表示フォームの作成および編集](create-edit-quick-view-forms.md)  

> [!div class="mx-imgBorder"] 
> ![取引先企業フォーム上の取引先担当者簡易表示フォーム](media/quick-view-form-contact.png "取引先企業フォーム上の取引先担当者簡易表示フォーム")  

PowerApps サイトから **簡易表示コントロールのプロパティ** にアクセスできます。 
1.  [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) サイトで、**モデル駆動型** (ナビゲーション ウィンドウの左下) を選択します。  

     ![モデル駆動型の設計モード](media/model-driven-switch.png)

2.  **データ**を展開して**エンティティ**を選択し、目的のエンティティを選択して**フォーム** タブを選択します。 

3. フォームの一覧で、種類が**メイン**のフォームを開きます。 次に**挿入**タブで、**簡易表示フォーム**を選択して簡易表示コントロールのプロパティを表示します。

    ![簡易表示コントロール](media/quick-view-control.png)
  
|プロパティ|説明|  
|--------------|-----------------|  
|**名前**|**必須**: スクリプト内で簡易表示フォームが参照されたとき使用される一意の名前。|  
|**ラベル**|**必須**: 簡易入力フォームに表示されるラベル。|  
|**フォームでラベルを表示する**|フォームでラベルを表示します。|  
|**検索フィールド**|フォームに含まれる検索フィールドの 1 つを選択します。|  
|**関連エンティティ**|この値は、選択する**ルックアップ フィールド**によって異なります。 通常、検索の1:N のエンティティ関連付けの主エンティティです。<br /><br /> エンティティが取引先企業か取引先担当者のいずれかを受け入れる**見込み顧客**検索を含む場合、**簡易表示フォーム**フィールドで、取引先企業と取引先担当者両方に対する簡易表示フォームを選択できます。これは、この値を変更してから別の簡易表示フォームを選択することでできます。|  
|**簡易表示フォーム**|**関連エンティティ**に簡易表示フォームがある場合は、ここで選択できます。 そうしない場合は、**新規**を選択して作成します。<br /><br /> **編集**を選択して、選択した簡易表示フォームを変更します。|  
|**追加のプロパティ**|チェック ボックスを選択して、既定のレンダリング スタイルを指定することができます。|

## <a name="next-steps"></a>次のステップ

[メイン フォームとそのコンポーネントの使用](use-main-form-and-components.md)
 
