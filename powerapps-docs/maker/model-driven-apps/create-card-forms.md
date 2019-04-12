---
title: PowerApps でカード フォームを作成 | MicrosoftDocs
description: PowerApps でカード フォームの作成および使用する方法を説明します
keywords: ''
ms.date: 03/05/2019
ms.service: powerapps
ms.custom: null
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - PowerApps
author: Mattp123
ms.assetid: be93b9d7-f1c2-4ee7-8d7c-0f5c34dfa5f7
ms.author: matp
manager: kvivek
ms.reviewer: null
ms.suite: null
ms.tgt_pltfrm: null
topic-status: Drafting
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-a-card-form"></a>カード フォームの作成
カード フォームは統一インターフェイス アプリのビューで使用されます。 カード フォームはモバイル デバイスに適したコンパクトな形式で情報を表示するように設計されています。 たとえば、自分のアクティブな取引先企業ビューの既定のカード フォームは、各取引先企業レコードに表示される情報を定義します。 

> [!div class="mx-imgBorder"] 
> ![](media/account-cardform-for-myactiveaccounts-view.png "自分のアクティブな取引先企業ビュー向けの取引先企業カード フォーム")

カード フォームは他のフォーム タイプと同じ方法で作成および編集できますが、カード フォームはアプリへの追加方法が異なります。 フォームをアプリのコンポーネントとして追加する代わりに、ユーザー定義のカードフォームが **読み取り専用グリッド** コントロールを使用してビューに追加されます。 

## <a name="create-a-card-form"></a>カード フォームの作成
1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインしてカード フォームを作成します。 
2. **データ** を展開して **エンティティ** を選択し、目的のエンティティを選択して **フォーム** タブを選択します。
3. ツールバーの **フォームの追加** を選択し、そして **カード フォーム** を選択します。 または、編集する **カード** フォームである既存の **フォームの種類** を開きます。
4. 必要なフィールドを追加します。 小さい画面にフォームをうまく表示するため、フィールドの数を制限することをお勧めします。 
5. **保存** を選び、そして **公開** を選択します。 

## <a name="add-a-card-form-to-a-view"></a>ビューにカード フォームを追加します 
1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。
2. **データ** を展開して、必要なエンティティを選択し、そして **ビュー** タブを選択します。
3. 必要なビューを選択して、そしてビュー デザイナーのツールバーで **クラシックに切り替え** を選択します。
4. **一般的なタスク** ウィンドウで **カスタム コントロール** 選択します。
5. コントロールの一覧から **コントロールの追加** を選択して **読み取り専用グリッド** を選択し、そして **追加** を選択します。

   > [!NOTE]
   > 読み取り専用グリッド コントロールは 2 つあります。 **読み取り専用グリッド (既定)** という名前の既定の読み取り専用グリッド コントロールは、ユーザー定義のカード フォームをサポートしていません。 

6. **読み取り専用グリッド** プロパティ ページから次のプロパティを構成し、そして **OK** を選択します。 
   - **カード フォーム**。 ![コントロール プロパティの編集](media/ccf-pencil-icon.png) の鉛筆のアイコンを選択し、そしてビューに表示するカード フォームを選択します。 既定で、ビューに関連付けられた主エンティティがすでに選択されていますが、これは変更できます。 
   - **リフロー動作**。 サイズ変更時にカードフォームを表示するかどうか変更したい場合は、![コントロール プロパティの編集](media/ccf-pencil-icon.png) の鉛筆のアイコンを選択します。 詳細: [グリッドのリストへのリフローを可能にする](specify-properties-for-unified-interface-apps.md#allow-grid-to-reflow-into-list)  
   - **読み取り専用グリッド** コントロールを表示すべき場所で、クライアントの種類、**Web**、**電話**、もしくは **タブレット** を選択します。

     ![カード フォームの読み取り専用グリッド](media/read-only-grid-for-cardform.png)

7. **OK** を選択して **カスタム コントロール** プロパティ ページを閉じます。 
8. クラシック ビュー デザイナーのツールバーで、**保存して閉じる** を選択します。 

## <a name="see-also"></a>関連項目
[モデル駆動型アプリのデータのビジュアル化のためのカスタム コントロールの使用](use-custom-controls-data-visualizations.md)



