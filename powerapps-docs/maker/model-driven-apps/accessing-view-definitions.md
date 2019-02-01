---
title: モデル駆動型のアプリ ビュー定義にアクセス | MicrosoftDocs
description: このトピックでは、エンティティ ビューにアクセスする方法を説明します
ms.custom: ''
ms.date: 11/27/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - PowerApps
author: Mattp123
ms.assetid: 034c8bef-0d1c-4ef9-8da7-f81343c4553a
caps.latest.revision: 25
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="access-a-model-driven-app-view-definition-in-powerapps"></a>PowerApps でモデル駆動型のアプリ ビュー定義にアクセスします

 このトピックでは、プロパティを表示するためにビュー定義を開き、ビューを構成するためにオプションを開きます。 PowerApps でビュー定義にアクセスするには、次のようないくつかの方法があります。 
  
  
## <a name="open-a-view-for-editing-in-the-latest-view-designer"></a>最新のビュー デザイナーで編集するためにビューを開く

> [!IMPORTANT]
> 最新バージョンのビュー デザイナーは現在プレビュー中です。 高度なフィルター処理、カスタム コントロール、および列のプロパティなどの一部の機能はまだサポートされていません。 これらのタスクを遂行するには、[ビューをクラシック ビュー デザイナーで開きます](#open-a-view-in-solution-explorer)。

1.  [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。  


    > [!IMPORTANT]
    > **モデル駆動型** デザイン モードがない場合は、[環境の作成](https://docs.microsoft.com/powerapps/administrator/create-environment)が必要となることがあります。 

2.  **データ**を展開して、**エンティティ**を選択し、**アカウント**などの目的のエンティティを選択します。   
3. **ビュー** タブを選択します。

    > [!div class="mx-imgBorder"] 
    > ![取引先企業ビュー定義](media/account-view-definitions.png)

4. 取引先企業エンティティ **すべての取引先企業** ビューなど、開くビューを選択します。

    > [!div class="mx-imgBorder"] 
    > ![すべての取引先企業ビュー](media/account-view-designer.png)

5. ビュー エディターでは、複数のタスクを実行できます。 
 
- [リスト内のレコードの並べ替え](configure-sorting.md)
- [ビューにおける列の選択と構成](choose-and-configure-columns.md)

## <a name="open-a-view-for-editing-from-a-legacy-web-app"></a>従来の Web アプリから編集するためにビューを開く
従来の Web アプリ内のエンティティの任意のリストで、省略記号 (...) ボタンを選択すると、コマンド バーに次のコマンドが表示されます。  

- **ビュー**: 既定のソリューションの現在のビューの定義が開きます。  
  
- **新しいシステム ビュー**: 既定のソリューション内の現在のエンティティについて新しいビューを作成するためのウィンドウを新しく開きます。  
  
- **エンティティのカスタマイズ**: **ビュー**の選択を可能にする、既定のソリューション内の現在のエンティティの定義が表示されます。  
  
- **システム ビュー**: **ビュー**の選択以外は、**エンティティのカスタマイズ**と同じウィンドウが開きます。  

   ![従来の Web アプリからビュー エディターを開く](media/open-view-editor-from-view.png)

## <a name="open-a-view-for-editing-in-solution-explorer"></a>ソリューション エクスプローラーで編集するためにビューを開く 
1.  [ソリューション エクスプローラー](advanced-navigation.md#solution-explorer)を開きます。  
  
2.  **コンポーネント** で **エンティティ** を展開し、目的のエンティティを展開します。  
  
3.  **ビュー**を選択します。  
  
4.  開くビューをダブルクリックします。 これによりクラシック ビュー デザイナーが開きます。
    
    > [!div class="mx-imgBorder"] 
    > ![すべての取引先企業ビュー](media/all-accounts-view.png)

 このビューの一覧には、必要なビューをより容易に検索するために使用できる次の 4 種類のフィルターがあります。  
  
- **すべてのアクティブなビュー**  

- **アクティブな共有ビュー**  

- **非アクティブな共有ビュー**  

- **アクティブなシステム定義ビュー**  
  
 ビューに関連付けられているエンティティがアンマネージド ソリューションの一部である場合は、既定のソリューションでそのエンティティのビューを作成または編集できます。 システム ビューはエンティティに関連付けられているので、単独のソリューション コンポーネントとして使用することはできません。 ビューは、フィールドとは異なり、ソリューション内で一貫性を必要とする一意の名前にカスタマイズの接頭辞を使用しないので、ビューをソリューションのコンテキストで作成する必要はありません。 
 
## <a name="next-steps"></a>次のステップ
[ビューについて](create-edit-views.md)


