---
title: PowerApps のモデル駆動型アプリのフォーム用タブ プロパティ | MicrosoftDocs
description: メイン フォームのタブ プロパティについて
Keywords: Tab properties; Dynamics 365; Main forms
author: matp
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
ms.author: Mattp123
manager: kvivek
ms.date: 06/07/2018
ms.service: crm-online
ms.topic: article
ms.assetid: e0790865-c5a4-4e86-bce2-584af2b8ed93
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="tab-properties-for-model-driven-app-forms-overview"></a>モデル駆動型アプリのフォーム用タブのプロパティの概要

 フォームの本文で、タブにより水平方向の分離が提供されます。 タブには、表示可能なラベルがあります。 ラベルが表示されている場合、ラベルを選択して、タブを展開したり閉じたりして、コンテンツを表示または非表示にすることができます。  
  
 タブには 3 個まで列を含めることができ、各列の幅は全体の幅の割合で設定できます。 新しいタブを作成すると、各列はセクションで事前入力されています。  

PowerApps サイトから **タブ プロパティ** にアクセスできます。 
1.  [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) サイトで、**モデル駆動型** (ナビゲーション ウィンドウの左下) を選択します。  

     ![モデル駆動型の設計モード](media/model-driven-switch.png)

2.  **データ**を展開して**エンティティ**を選択し、目的のエンティティを選択して**フォーム** タブを選択します。  

3.  フォームの一覧で、種類が**メイン**のフォームを開きます。 次に、フォーム キャンバス上でいずれかのタブ内をダブルクリックして、タブのプロパティを表示します。

    ![タブのプロパティ](media/tab-properties.png)
  
 次の表はフォーム上のタブに設定できるプロパティを示します。
  
|タブ​​|プロパティ|説明|  
|---------|--------------|-----------------|  
|**表示**|**名前**|**必須**: スクリプト内でタブが参照されたとき使用される一意の名前。 名前には、英数字とアンダースコアのみを使用できます。|  
||**ラベル**|**必須**: ユーザーに表示されるタブのローカライズ可能なラベル。|  
||**このタブのラベルをフォーム上に表示**|ラベルが表示されたら、ユーザーはラベルを選択して、タブを展開したり折りたたんだりすることもできます。 ラベルを表示するかどうかを選択します。|  
||**既定でこのタブを展開する**|フォーム スクリプトを使用するか、ラベルを選択して、タブの状態を展開または折りたたみに切り替えることができます。 タブの既定の状態を選択します。|  
||**既定で表示**|タブの表示は任意で、スクリプトを使用して管理します。 タブが表示されるようにするかどうかを選択します。 詳細情報: [表示オプション](visibility-options-legacy.md)|  
||**使用可否**|タブを電話で使用できるようにするかどうかを選択します。|  
|**形式**|**レイアウト**|タブには最大 3 つの列があります。 これらのオプションを使用して、タブの数とそのタブが占める幅全体の割合を定義します。|  
|**イベント**|**フォーム ライブラリ**|タブの `TabStateChange` イベント ハンドラーで使用される JavaScript Web リソースを指定します。<br /><br />|  
||**イベント ハンドラー**|タブの `TabStateChange` イベントに要求されるライブラリの関数を構成します。 詳細情報: [イベント ハンドラーを構成する](configure-event-handlers-legacy.md)|  
  
## <a name="next-steps"></a>次のステップ

[メイン フォームとそのコンポーネントの使用](use-main-form-and-components.md)
