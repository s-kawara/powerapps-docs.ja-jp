---
title: ソリューションを使用してモデル駆動型アプリを配布する | MicrosoftDocs
description: ソリューションを使用してモデル駆動型アプリを配布する方法について説明します
keywords: ''
ms.date: 08/06/2018
ms.service: powerapps
ms.custom: null
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
ms.assetid: e82e7f64-37ad-41e5-acd7-16309881c6a2
author: Mattp123
ms.author: matp
manager: kvivek
ms.reviewer: null
ms.suite: null
ms.tgt_pltfrm: null
caps.latest.revision: 9
topic-status: Drafting
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="distribute-a-model-driven-app-using-a-solution"></a>ソリューションを使用してモデル駆動型アプリを配布する

モデル駆動型アプリはソリューション コンポーネントとして配布されます。 モデル駆動型アプリの作成後、そのアプリをソリューションにパッケージ化した後、ZIPファイルにエクスポートすることにより、別の環境でそのアプリを使用できるようになります。 ソリューション (.zip ファイル) がターゲット環境で適切にインポートされると、パッケージ化されたアプリが使用可能になります。 
  
## <a name="add-an-app-to-a-solution"></a>ソリューションへのアプリの追加
アプリを配布するために、ソリューションを作成してアプリをエクスポート用にパッケージできるようにします。

1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。

2. **ソリューション** を選択し、**新しいソリューション** を選択します。
3. **新しいソリューション** ページのフィールドに入力し、**保存** を選択します。 詳細: [ソリューションの作成](../common-data-service/create-solution.md)
4. **ソリューション** ページが表示されます。 **既存の追加** を選択して **アプリ** を選択し、ソリューションに追加するアプリを選択して **OK** を選択します。 

    ![ソリューション コンポーネントの選択](media/select-solution-components.png)

5. **不足している必須コンポーネント** ページが表示された場合、**はい、必須コンポーネントを含めます** を選択し、アプリの一部であるエンティティ、ビュー、フォーム、グラフ、サイト マップなどの必須コンポーネントを追加することをお勧めします。 **OK** を選びます。
6. **ソリューション** ページで、**保存して閉じる** を選択します。

## <a name="export-a-solution"></a>ソリューションのエクスポート
アプリを配布して他の環境にインポートできるようにしあり、[Microsoft AppSource](https://appsource.microsoft.com/) で使用できるようにするには、ソリューションを zip ファイルにエクスポートします。 次に、アプリおよびコンポーネントを含む zip ファイルを他の環境にインポートできます。

1. [ソリューション ページj](advanced-navigation.md#solutions)を開きます。 
2. エクスポートするソリューションを選択し、ツール バーで **エクスポート** を選択します。 
3. **カスタマイズの公開** ページで、**次へ** を選択します。
4. **カスタマイズの公開** ページが表示された場合、**次へ** を選択します。 
5. **システム設定のエクスポート** ページで、含めるオプション機能を選択し、**次へ** を選択します。 
6. **パッケージの種類** ページで、**アンマネージド** または **管理** を選択し、**エクスポート** を選択します。 ソリューション パッケージの種類の詳細については、「[ソリューションの概要](../common-data-service/solutions-overview.md)」を参照してください。
7. ブラウザーおよび設定に応じて、.zip パッケージ ファイルが構築され、既定のダウンロード フォルダーにコピーされます。 パッケージのファイル名は、ソリューションの一意の名前に下線とソリューションのバージョン番号を付けたものです。

    > [!NOTE]
    > ソリューションを使用してアプリをエクスポートするとき、アプリ URL はエクスポートされません。
  
## <a name="import-a-solution"></a>ソリューションのインポート  
インポートするアプリを含むソリューション ZIP ファイルを受け取ったとき、ソリューションのコンポーネント ページを開いて、ソリューションをインポートします。 ソリューションが正常にインポートされると、環境でアプリを使用できるようになります。

1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。

2. **ソリューション** を選択し、ツール バーで **インポート** を選択します。
3. インポートするファイルを参照し、**次へ** を選択します。
4. **インポート**を選択します。

## <a name="see-also"></a>関連項目
[ソリューション発行者の接頭辞の変更](../common-data-service/change-solution-publisher-prefix.md)
