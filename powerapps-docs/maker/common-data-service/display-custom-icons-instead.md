---
title: PowerApps のリスト ビューに値の代わりにカスタム アイコンを表示する | MicrosoftDocs
description: ビューにカスタム アイコン画像を表示する方法を説明します。
ms.custom: ''
ms.date: 06/21/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
author: Mattp123
ms.assetid: af866aed-2586-4b6f-bb1c-3519baae3645
caps.latest.revision: 25
ms.author: matp
manager: kvivek
ms.openlocfilehash: 592d2ad73b192d7f03c552563c4f91d52f3d201d
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39691326"
---
# <a name="display-custom-icons-instead-of-values-in-list-views"></a>リスト ビューに値の代わりにカスタム アイコンを表示する

<a name="GridIcons"></a>   

 PowerApps 環境管理者およびカスタマイザーは、ビューに画像を追加し、JavaScript を使用して列値に基づいて、画像を選択するロジックを確立できます。 テキストや数値の代わりに、一部の列にアイコンを表示するリスト ビューの表示機能は、リレーションシップ インサイトで導入されました。 
  
> [!NOTE]
>  グリッド アイコンは、Web インターフェイスのみで表示されます。 [!INCLUDE[pn_Outlook_short](../../includes/pn-outlook-short.md)] やモバイル アプリでは表示されません。  
  
### <a name="add-custom-graphics-and-javascript-as-web-resources"></a>Web リソースとしてカスタム画像や JavaScript を追加する  
  
1.  カスタマイズに必要な新しい画像ファイルを作成します。 アイコンのサイズには 16 x 16 ピクセル (これより大きい画像は縮小されます) を推奨します。  
  
2.  どの値にどのアイコンを表示するか定めるには、JavaScript 関数を 1 つ以上記述します (カスタマイズしたい列ごとに、通常 1 つの関数が必要です)。 各関数は、入力として行データ オブジェクトと言語 (LCID) コードを受け取り、画像名とツールヒントのテキストの配列を返す必要があります。 関数の例については、このトピックで後述する「[サンプルの JavaScript 関数](#SampleJavascript)」を参照してください。  
  
3.  管理者として環境にサインインし、[ソリューション エクスプローラー](../model-driven-apps/advanced-navigation.md#solution-explorer)を開きます。  
  
4.  **[既定のソリューション]** ポップアップ ウィンドウが開きます。 ここで **[コンポーネント]** > **[Web リソース]** に移動します。  
  
5.  ここで Web リソースを 1 つずつカスタム画像としてアップロードします。 ツールバーで **[新規]** ボタンを選択し、新しい Web リソースを作成します。 リソースを作成するための別のポップアップ ウィンドウが開きます。 次を実行します。  
  
    1.  新しいリソースに意味のある**名前**を付けます。 ご自分の JavaScript コードからは、この名前を使用して各画像を参照することになります。  
  
    2.  **[種類]** に、画像ファイルを保存するために使用した画像形式 (PNG、JPEG または GIF) を設定します。  
  
    3.  **[ファイルの選択]** を選択し、ファイル ブラウザー ウィンドウを開きます。 これを使用して画像ファイルを検索および選択します。  
  
    4.  **[表示名]** と必要な場合は **[説明]** を追加します。  
  
    5.  **[保存]** を選択し、**[Web リソース]** ウィンドウを閉じます。  
  
6.  所持している各画像ファイルに対し、前の手順を繰り返します。  
  
7.  ここで、JavaScript を最終的な Web リソースとして追加します。 ツールバーで **[新規]** を選択し、新しい Web リソースを作成します。 リソースを作成するための別のポップアップ ウィンドウが開きます。 次を実行します。  
  
    1.  新しいリソースに意味のある**名前**を付けます。  
  
    2.  **[種類]** を **[スクリプト (JScript)]** に設定します。  
  
    3.  テキスト エディター ウィンドウを開くために、(**[種類]** 設定の横にある) **[テキスト エディター]** を選択します。 ここにご自分の Javascript コードを貼り付け、**[OK]** を選択して保存します。  
  
    4.  **[表示名]** と必要な場合は **[説明]** を追加します。  
  
    5.  **[保存]** を選択し、**[Web リソース]** ウィンドウを閉じます。  
  
8.  **[既定のソリューション]** ポップアップ ウィンドウが開いた状態で **[コンポーネント]** > **[エンティティ]** ツリーを展開し、カスタマイズするエンティティを探します。  
  
9. エンティティを展開し、その **[ビュー]** アイコンを選択します。  
  
10. これで選択したエンティティのビュー一覧が表示されます。 一覧からビューを選択します。 次いで、ツールバーの **[その他のアクション]** ドロップダウン リストを開き、**[編集]** を選択します。  
  
11. 選択したビューを編集するコントロールがあるポップアップ ウィンドウが開きます。 これには、ビューの一部である各列が表示されます。 対象列を選択し、**[タスク]** ボックスの **[プロパティの​​変更]** を選択します。 **[列のプロパティの変更]** ダイアログが開きます。ここで以下の設定を行います。  
  
    - **Web リソース**: JavaScript 関数を保持するために作成した Web リソースの名前を指定します (一覧から選択するには、**[参照]** を選択します)。  
  
    - **関数名**: 選択した列およびビューを変更するために記述した関数の名前を入力します。  
  
12. **[OK]** を選択して **[列のプロパティの変更]** ダイアログを閉じます。  
  
13. **[保存して閉じる]** を選択し、ビューを保存します。  
  
14. 各エンティティ、ビューおよび列に対して、必要に応じてこれらの手順を繰り返します。  
  
15. 準備ができたら、**[すべてのカスタマイズの公開]** を選択して変更を公開します。 次いで、**[既定のソリューション]** ウィンドウを閉じます。  
  
<a name="SampleJavascript"></a>   

### <a name="sample-javascript-function"></a>サンプルの JavaScript 関数  
 カスタム アイコンとツールヒントを表示する JavaScript 関数では、layoutxml で指定した行オブジェクト全体と呼び出し元のユーザーのロケール ID (LCID) の 2 つの引数を使用します。 LCID パラメーターを使用すると、複数の言語でツールヒントを指定できます。 環境でサポートしている言語の詳細については、「[言語を有効にする](https://docs.microsoft.com/dynamics365/customer-engagement/admin/enable-languages)」と [Dynamics 365 の言語パックのインストールまたはアップグレード](https://technet.microsoft.com/library/hh699674.aspx)に関する記事を参照してください。 コードで使用できるロケール ID (LCID) 値の一覧については、[Microsoft によって割り当てられているロケール ID](https://go.microsoft.com/fwlink/?linkid=829588) に関する記事を参照してください。

  
 事前定義されているオプション セットが少ないタイプの属性のオプション セットにカスタム アイコンを追加する場合、ラベルではなく、オプションの整数値を必ず使用し、ローカライズに関係する問題を回避するようにしてください。  
  
 次のサンプル コードでは、opportunityratingcode (評価) 属性の 3 つの値のうちの 1 つ (1: Hot、2: Warm、3: Cold) を使用してアイコンとツールヒントを表示します。 このサンプル コードは、ローカライズされたツールヒント テキストを表示する方法も示します。 このサンプルが動作するには、new_Hot、new_Warm および new_Cold という名前の 16 x 16 の 3 つの画像 Web リソースを作成する必要があります。  
  
```  
function displayIconTooltip(rowData, userLCID) {      
    var str = JSON.parse(rowData);  
    var coldata = str.opportunityratingcode_Value;  
    var imgName = "";  
    var tooltip = "";  
    switch (parseInt(coldata,10)) { 
        case 1:  
            imgName = "new_Hot";  
            switch (userLCID) {  
                case 1036:  
                    tooltip = "French: Opportunity is Hot";  
                    break;  
                default:  
                    tooltip = "Opportunity is Hot";  
                    break;  
            }  
            break;  
        case 2:  
            imgName = "new_Warm";  
            switch (userLCID) {  
                case 1036:  
                    tooltip = "French: Opportunity is Warm";  
                    break;  
                default:  
                    tooltip = "Opportunity is Warm";  
                    break;  
            }  
            break;  
        case 3:  
            imgName = "new_Cold";  
            switch (userLCID) {  
                case 1036:  
                    tooltip = "French: Opportunity is Cold";  
                    break;  
                default:  
                    tooltip = "Opportunity is Cold";  
                    break;  
            }  
            break;  
        default:  
            imgName = "";  
            tooltip = "";  
            break;  
    }  
    var resultarray = [imgName, tooltip];  
    return resultarray;  
}  
```  
  
 これにより、各行の値に依存するツールヒント付きのアイコンが **[評価]** 行に表示されます。 このような結果になります。  
  
 ![カスタム列画像の例](media/custom-column-graphics-example.png "カスタム列画像の例")  
 
 ### <a name="see-also"></a>関連項目
 [ビューの作成または編集](../model-driven-apps/create-edit-views.md)
