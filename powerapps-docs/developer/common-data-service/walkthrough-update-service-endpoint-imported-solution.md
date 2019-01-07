---
title: 'チュートリアル: ソリューションからインポートしたサービス エンドポイントの更新 (アプリ用 Common Data Service for Apps) | Microsoft Docs'
description: チュートリアルは、ソリューションからインポートしたサービス エンドポイントの更新方法を示します。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 66795838-3b15-bfb3-6f59-68cfe2fe988e
author: brandonsimons
ms.author: jdaly
manager: ryjones
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="tutorial-update-a-service-endpoint-imported-from-a-solution"></a>チュートリアル: ソリューションからインポートしたサービス エンドポイントの更新

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-update-service-endpoint-imported-solution -->

1 つ以上の SAS 認証用に構成したサービス エンドポイントが含まれるソリューションを組織にインポートした後には、特別な手順が必要です。 サービス エンドポイントが含まれるソリューションをエクスポートすると、エクスポートしたソリューションには、各サービス エンドポイントに対する SAS キーは含まれません。 組織へのソリューションのインポート後、各サービス エンドポイントに SAS キーを提供するために追加の手順を実行する必要があります。  
  
 ソリューションのインポート後、各サービス エンドポイントに対して SAS キーを設定するには、次の手順を実行します。  
  
### <a name="update-the-sas-key"></a>SAS キーの更新  
  
1.  Dynamics CRM 2016 Service Pack 1 設置型 (以降) SDK ダウンロードの Tools フォルダにあるプラグイン登録ツールを実行します。 ツールの以前のリリースは SAS 認証をサポートしていません。  
  
2.  ツールを使用して、インポートされたソリューションが含まれる組織にサインインします。  
  
3.  組織のタブ ビューで対象のサービス エンドポイントを選択します。  
  
4.  **更新**を選択します。 入力済のフィールドを使用して、次のフォームが表示されます。  
  
 ![サービス エンドポイント SAS key 値を更新](media/sas-key.PNG "サービス エンドポイント SAS key 値を更新")  
  
5.  **SAS キー**フィールドに ******* の値が表示されます。  その値を正しい SAS キー値に置き換えます。 Azure [クラシック ポータル](http://manage.windowsazure.com) から、Azure メッセージング エンティティ (キュー、トピックなど) の SAS キーを入手できます。  
  
6.  **保存**を選びます。  
  
### <a name="see-also"></a>関連項目  
[Dynamics 365 との Azure 統合](azure-integration.md)

 [Service Bus の認証および承認](https://azure.microsoft.com/en-us/documentation/articles/service-bus-authentication-and-authorization/)
