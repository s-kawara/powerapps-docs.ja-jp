---
title: レポートをモデル駆動型アプリに追加
ms.custom: ''
ms.date: 06/24/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - PowerApps
author: Mattp123
ms.assetid: b4098c96-bce1-4f57-804f-8694e6254e81
caps.latest.revision: 15
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="add-reporting-to-your-model-driven-app"></a>レポートをモデル駆動型アプリに追加

PowerApps アプリには、有益な事業情報をユーザーに提供するレポートを含めることができます。 このレポートは SQL Server Reporting Services に基づいており、典型的な SQL Server Reporting Services レポートで使用できる機能と同じ一連の機能を備えています。

> [!div class="mx-imgBorder"] 
> ![](media/progress-against-goals-report.png "目標に対しての進行状況の標準レポート")

システム レポートは、すべてのユーザーが使用できます。 ユーザーが作成または所有するレポートは、特定の同僚またはチームと共有することや、すべてのユーザーがレポートを使用できるように、組織に対してそのレポートを使用可能にすることができます。 これらのレポートは Common Data Service アプリや Dynamics 365 for Customer Engagement アプリ特有の FetchXML クエリを使用し、データを取得してレポートを作成します。 PowerApps アプリで作成したレポートは、フェッチ ベースのレポートです。

> [!NOTE]
> レポート機能は、タブレットや電話などのモバイル デバイス上で実行されているキャンバス アプリやモデル駆動型アプリでは機能しません。 

レポートは、次の方法のいずれかで作成できます。

- レポート ウィザードを使用してモデル駆動型のアプリケーションで作成する。 詳細情報: [レポート ウィザードを使用したレポートの作成または編集](/dynamics365/customer-engagement/basics/create-edit-copy-report-wizard) 
<!-- From a model-driven app using an advanced find query. To do this, you build an advanced find query and then select **Download as FetchXML**. Next, from the reports area select **New**, for **Report Type** select **Existing File**, select **Choose File** open the xml file, fill in the required fields, and save the report. More information: [Add a report](/dynamics365/customer-engagement/basics/add-existing-report) -->
- SQL Server Data Tools および Report Authoring 拡張を使用してカスタム レポートを作成する。 詳細情報: [レポートと分析ガイド](/dynamics365/customer-engagement/analytics/reporting-analytics-with-dynamics-365)


## <a name="add-reporting-to-a-unified-interface-app"></a>レポートを統一インターフェイス アプリに追加
フェッチ ベースのレポート機能をアプリに追加できます。それにより、ユーザーがレポートを実行、共有、作成、および編集できます。 これを行うためには、アプリのサイト マップにレポート エンティティを追加します。 

1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインし、編集用の既存アプリを開きます。 
2. アプリ デザイナーで、**サイト マップ**の隣りの![サイト マップ編集のための鉛筆アイコン](media/ccf-pencil-icon.png)を選択します。 
3. サイトマップ デザイナーで**追加**を選択し、その後**領域**を選択します。 
4. **タイトル** ボックスに、*レポート*などの領域のタイトル名を入力します。 
5. 前の手順で名前を付けた領域を選択し、**追加**、**グループ**の順に選択して、グループ内の**タイトル** ボックスに*レポート*などのグループ タイトル名を入力します。 
6. 前の手順で名前を付けたグループを選択し、**追加**、**サブエリア**の順に選択して、次のプロパティを含めます。 

   - **Type**。 **エンティティ**を選択します。
   - **エンティティ**。 エンティティの一覧から**レポート** エンティティを選択します。  
   - **タイトル**。 *レポート*など、わかりやすいタイトルを入力します。

      ![サイトマップにレポートを追加](media/report-entity-sitemap.png)

7. **保存して閉じる**を選択してアプリ デザイナーに戻ります。 


8. アプリ デザイナーで**保存**を選択し、**公開**を選択します。


これでアプリには**レポート**領域が表示され、ユーザーはアクセス許可を持つレポートを表示、実行、割り当て、共有、および編集できます。また、レポート ウィザードを使って新しいレポートを作成することもできます。 

> [!div class="mx-imgBorder"] 
> ![](media/report-feature-in-app.png "レポート ビュー")

### <a name="see-also"></a>関連項目
[レポートの実行](/dynamics365/customer-engagement/basics/run-report)
