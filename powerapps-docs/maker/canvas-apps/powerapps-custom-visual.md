---
title: Power BI 用の PowerApps カスタム ビジュアル | Microsoft Docs
description: 同じデータ ソースを使用し、Power BI の他のレポート項目と同様にフィルタリングできるキャンバス アプリの埋め込みに関する手順と制限
author: mgblythe
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 03/15/2018
ms.author: mblythe
ms.openlocfilehash: 0da480a482415ad174f10204f14f31adbd3607f2
ms.sourcegitcommit: e3f5a2bef64085d02aec82e62ff94ae8a4d01d24
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2018
ms.locfileid: "39469996"
---
# <a name="powerapps-custom-visual-for-power-bi"></a>Power BI 用の PowerApps カスタム ビジュアル

Power BI を利用すると、データの洞察と適切な意思決定を行うことができ、同時に PowerApps を使用して、すべてのユーザーが、ビジネス データに接続するアプリを構築して使用することができます。 PowerApps カスタム ビジュアルを使用すると、状況に応じたデータをキャンバス アプリに渡すことができます。キャンバス アプリは、レポートを変更するとリアルタイムで更新されます。 これで、アプリ ユーザーは、ビジネスの動向を把握し、Power BI レポートとダッシュ ボードから直接アクションを実行できます。

## <a name="using-the-powerapps-custom-visual"></a>PowerApps のカスタム ビジュアルを使用する

PowerApps カスタム ビジュアルを Power BI レポートで使用するための手順を見てみましょう。

1. [AppSource](https://appsource.microsoft.com/product/power-bi-visuals/WA104381378?tab=Overview) からカスタム ビジュアルを取得したり、Power BI サービスに直接インポートしたりします。

    ![Marketplace のカスタム ビジュアル](./media/powerapps-custom-visual/powerapps-store.png) 

2. PowerApps ビジュアルをレポートに追加し、それに関連付けられているデータ フィールドを設定します。

    ![レポート データの選択](./media/powerapps-custom-visual/add-visual-set-data.png)

3. 既存のアプリを選択するか、作成することができます。 アプリを作成する場合は、それを作成する環境を選択できます。

    ![新規または既存のアプリ](./media/powerapps-custom-visual/create-new-or-choose-app.png)

    既存のアプリを使用する場合は、ビジュアルによって PowerApps でアプリを開くように求められます。 ビジュアルは、Power BI が PowerApps にデータを送信できるように、アプリで必要なコンポーネントが設定されます。

    新しいアプリを作成する場合、PowerApps は既にセットアップされている必要なコンポーネントで簡単なアプリを作成します。

    ![新しいアプリ](./media/powerapps-custom-visual/new-app.png)

4. 現在、PowerApps Studio では、手順 2. で設定するデータ フィールドを使用できます。 `PowerBIIntegration` オブジェクトは他の PowerApps 読み取り専用データ ソースまたはコレクションと同様に動作します。 オブジェクトを使用して、すべてのコントロールに入力できるほか、他のデータ ソースを結合したりフィルタリングしたりすることができます。

    ![ユーザー定義式](./media/powerapps-custom-visual/custom-formula.png)

    この数式は、顧客のデータ ソースと Power BI のデータを結合します。`LookUp(Customer,Customer_x0020_Name=First(PowerBIIntegration.Data).Customer_Name)`

   Power BI レポートと起動された PowerApps Studio のインスタンスは、ライブ データの接続を共有します。 これらは、どちらも開かれていますが、レポートのデータをフィルタリングまたは変更し、更新されたデータが PowerApps Studio でアプリにすぐに反映されるようにすることができます

5. アプリの構築または変更を完了した後で、PowerApps でアプリを保存および公開し、Power BI レポートにアプリを表示します。

6. 変更が完了したら、PowerApps アプリをレポートのユーザーと共有していることを確認し、レポートを保存します。

7. これで、ユーザー アクションを実行してデータから洞察を得ることができるレポートが作成されました。

    ![レポートの操作](./media/powerapps-custom-visual/working-report.gif)

    アプリを変更する必要がある場合は、編集モードでレポートを開き、PowerApps ビジュアルの **[その他のオプション]** (**. . .**) をクリックまたはタップし、**[編集]** を選択します。

    ![アプリの編集](./media/powerapps-custom-visual/edit-app.png)

## <a name="limitations-of-the-powerapps-custom-visual"></a>PowerApps のカスタム ビジュアルの制限

PowerApps のカスタム ビジュアルはプレビューで使用でき、次の制限があります。

- Power BI Desktop、Internet Explorer、Mozilla Firefox で PowerApps のカスタム ビジュアルを使用する場合は、アプリを作成または変更することはできません。 まず、Power BI サービスにレポートを公開することをお勧めします。 その後で、Microsoft Edge または Google Chrome を使用して、新しいアプリを作成し、アプリを変更します。
- ビジュアルに関連付けられているデータ フィールドを変更する場合、省略記号 (...) を選択し、**[編集]** を選択して Power BI サービス内でアプリを編集する必要があります。 それ以外の場合、PowerApps に変更が反映されず、アプリは予期しない方法で動作します。
- PowerApps のカスタム ビジュアルは、Power BI のレポートまたは Power BI データ ソースの更新をトリガーできません。 アプリからデータを、レポートと同じデータ ソースに書き戻す場合、変更内容はすぐに反映されません。 変更は、次回のスケジュールされた更新で反映されます。
- PowerApps のカスタム ビジュアルは、データをフィルター処理したり、データをレポートに送信したりできません。
- レポートとは別に PowerApps アプリを共有する必要があります。 [PowerApps でのアプリの共有](share-app.md)の詳細を参照してください。
- Power BI 用モバイル アプリでは、PowerApps のカスタム ビジュアルをサポートしていません。

## <a name="next-steps"></a>次の手順

* 単純な[ステップ バイ ステップ チュートリアル](embed-powerapps-powerbi.md)を実行する。
* [ビデオ](https://aka.ms/powerappscustomvisualvideo)を参照する。