---
title: 'チュートリアル: プラグイン登録ツールを使用した Azure 対応プラグインの登録 (アプリ用 Common Data Service) | Microsoft Docs'
description: 'このチュートリアルでは、プラグイン登録ツールを使用して、サービス エンドポイントの手順を登録する方法について説明します。 '
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: b5ef50fa-8085-f425-3968-804d012fc840
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

# <a name="tutorial-register-an-azure-aware-plug-in-using-the-plug-in-registration-tool"></a>チュートリアル: プラグイン登録ツールを使用した Azure 対応プラグインの登録

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-azure-aware-plug-in-using-plug-in-registration-tool -->

このチュートリアルでは、プラグイン登録ツールを使用して、サービス エンドポイントの手順を登録する方法について説明します。 構成したならば、Dynamics 365 (online) アプリ用 Common Data Service は Azure ソリューション エンドポイントに現在の操作の実行コンテキストに投稿できます。 このチュートリアルでは、このステップを登録して、`Account` エンティティ向けの <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> メッセージの実行コンテキストを Azure Service Bus に投稿します。  
  
 このチュートリアルを開始する前に、次の前提条件を満たしておく必要があります。  
  
-   プラグイン登録ツールにアクセスします。 [!INCLUDE[proc-download-plugin-registration-tool](../../includes/proc-download-plugin-registration-tool.md)]
  
-   Dynamics 365 システム ユーザー アカウントにはシステム カスタマイザー ロールまたはシステム管理者ロールが必要です。 
  
-   Dynamics 365 からのメッセージの送信先となる、SAS 認証に対して構成された Azure プラットフォーム サービス名前空間へのアクセス権を取得します。  
  
  
-   例えば、リレーなどのキュー以外の他の何らかの Azure メッセージング エンティティを使用するように計画する場合、Dynamics 365 が正常に Azure Service Bus に投稿する指定されたソリューション エンドポイントをアクティブにリッスンするリスナー アプリケーションが存在する必要があります。 詳細については、「[Azure ソリューション用のリスナーの記述](write-listener-application-azure-solution.md)」を参照してください。  
  
-   SAS 承認で構成されたサービス エンドポイントが対象組織で使用できます。 詳細: [チュートリアル: Dynamics 365 との統合のための Microsoft Azure (SAS) の構成](walkthrough-configure-azure-sas-integration.md)。  
  
## <a name="steps"></a>手順  
 このチュートリアルには次の手順が含まれます。  
  
1.  [Dynamics 365 Server に接続する](#BKMK_Connect)  
  
2.  [イベントのサービス エンドポイントの手順を登録する](#BKMK_Register)  
  
3.  [エンドポイント登録のテスト](#BKMK_Test)  
  
<a name="BKMK_Connect"></a>   
## <a name="connect-to-the-dynamics-365-server"></a>Dynamics 365 Server に接続する  
 プラグイン登録ツールを使用して Dynamics 365 Server に接続するには、次の手順に従います。  
  
1.  プラグイン登録ツールを実行します。  
  
2.  **新しい接続の作成**をクリックします。  
  
3.  **ログイン**ダイアログ ボックスで、サービス エンドポイントを登録する Dynamics 365 Server に対応する、展開の種類のラジオボタンを選択します。 **設置型**ラジオ ボタンには、IFD の展開が含まれます。オンラインボタンはのプロバイダー用です。**Office 365**ボタンは、Dynamics 365 (online) の Microsoft Online Service プロバイダー用です。  
  
    |||  
    |-|-|  
    |![オンライン展開のログイン フォーム](media/crm-v6s-pr.png "オンライン展開のログイン フォーム")<br />オンライン展開のログイン フォーム|![設置型展開のログイン ウィンドウ](media/crm-v6s-pr-login-onprem.png "設置型展開のログイン ウィンドウ")<br />設置型展開のログイン フォーム|  
  
4.  **使用可能な組織の一覧を表示する**チェックボックスをオンにする場合、**ログイン**をクリックした後、所属している組織の一覧が表示されます。 これにより、サービス エンドポイントを登録する組織を選択することができます。 選択しない場合は、既定の組織が使用されます。  
  
5.  サーバーおよびログインのアカウントに関する指示される情報を入力し、**ログイン**をクリックします。  
  
<a name="BKMK_Register"></a>   
## <a name="register-a-service-endpoint-step-for-an-event"></a>イベントのサービス エンドポイントの手順を登録する  
 サービス エンドポイントのイベントのための手順を登録するには、次の手順に従います。  
  
1.  対象組織のタブのタブの既存のサービス エンドポイントを選択します。  
  
2.  **登録**メニューに移動し、**新しい手順の登録**をクリックします。  
  
3.  次の図のように、**新しい手順の登録**ダイアログ ボックスにアカウント作成イベントの情報を入力します。

 ![サービス エンドポイントの手順の作成](media/crm-v6s-pr-service-endpoint-step.png "サービス エンドポイントの手順の作成")
  
4.  **新しい手順の登録** をクリックします。  
  
 これで、Dynamics 365 はアカウントが作成されるたびに実行コンテキストを含んだ現在のメッセージをサービス バスに送信するようになります。 送信は非同期で実行され、すぐには実行されません。  
  
<a name="BKMK_Test"></a>   
## <a name="test-the-endpoint-registration"></a>エンドポイント登録のテスト  
 エンドポイントを登録した後、それをテストできます。 プラグインからのサービス バス送信が実行されるには、ターゲット エンドポイント上でリスナーが実行されているか、またはキューが利用可能になっている必要があります。  
  
1.  サービス エンドポイントを登録したのと同じ組織に対して Dynamics 365 Web アプリケーションを開きます。  
  
2.  **作成**ボタン![[作成] ボタン](media/crm-v6s-wa-create-icon.PNG "[作成] ボタン")をクリックし、**取引先企業**をクリックします。  
  
3.  **アカウント名**フィールドにアカウント名 (例: `Adventure Works Cycle`) を入力してから、**保存**をクリックします。  
  
4.  Azure Service Bus 投稿が実行されるまで 10 秒ほど待ちます。  
  
5.  **設定 > システム ジョブ**をクリックします。  
  
6.  サービス エンドポイントに対して指定したのと同じ名前のシステム ジョブを開きます。 ステータスをチェックして、送信が成功、待機、失敗のいずれの状態かを確認します。  
  
 必要な場合は、エンドポイントの登録を解除できます。解除するには、ツールのツリー ビューでエンドポイントを選択し、**登録を解除**をクリックします。  
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 との Azure 統合](azure-integration.md)
 
 [Microsoft Azure と Dynamics 365 との統合の概要](azure-integration.md)
