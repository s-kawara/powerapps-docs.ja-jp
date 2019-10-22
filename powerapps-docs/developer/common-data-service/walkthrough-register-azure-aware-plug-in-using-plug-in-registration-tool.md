---
title: 'チュートリアル: プラグイン登録ツールを使用する Azure 対応プラグインの登録ツールの登録 (Common Data Service) | Microsoft Docs'
description: 'このチュートリアルでは、プラグイン登録ツールを使用して、サービス エンドポイントの手順を登録する方法について説明します。 '
keywords: ''
ms.date: 06/01/2019
ms.service: powerapps
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

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/walkthrough-register-azure-aware-plug-in-using-plug-in-registration-tool -->

このチュートリアルでは、プラグイン登録ツールを使用して、サービス エンドポイントの手順を登録する方法について説明します。 構成すると、Common Data Service (CDS) は、現在の操作中の実行コンテキストを Azure ソリューションのエンドポイントに投稿できるようになります。 このチュートリアルでは、このステップを登録して、`Account` エンティティ向けの <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> メッセージの実行コンテキストを Azure Service Bus に投稿します。  
  
このチュートリアルを開始する前に、次の前提条件を満たしておく必要があります。  
  
- プラグイン登録ツールにアクセスします。 [!INCLUDE[proc-download-plugin-registration-tool](../../includes/proc-download-plugin-registration-tool.md)]
- CDS システム ユーザー アカウントには、システム カスタマイザー ロールまたはシステム管理者ロールが必要です。 
- CDS からのメッセージの送信先となる、 SAS または CDS 認証に対して構成された、 Azure プラットフォーム サービス名前空間へのアクセス権を取得します。  
- 例えば、リレーなどのキュー以外の他の Azure メッセージング エンティティを使用する計画を立てる場合、CDS が正常に Azure Service Bus に投稿されるための指定のソリューション エンドポイントをアクティブにリスニングするリスナー アプリケーションが存在する必要があります。 詳細については、「[Azure ソリューション用のリスナーの記述](write-listener-application-azure-solution.md)」を参照してください。  
- SAS 承認で構成されたサービス エンドポイントが対象組織で使用できます。 詳細: [チュートリアル: CDS との統合用の Microsoft Azure (SAS) を構成します](walkthrough-configure-azure-sas-integration.md)。  
  
## <a name="steps"></a>手順

このチュートリアルには次の手順が含まれます。  
  
1. [CDS に接続](#BKMK_Connect)  
1. [イベントのサービス エンドポイントの手順を登録する](#BKMK_Register)  
1. [エンドポイント登録のテスト](#BKMK_Test)
  
<a name="BKMK_Connect"></a>

## <a name="connect-to-cds"></a>CDS に接続
 
プラグイン登録ツールを使用して CDS に接続するには、次の手順に従います。  
  
1. プラグイン登録ツールを実行します。  
1. **新しい接続の作成** をクリックします。  
1. **ログイン** ダイアログ ボックスで、**Office 365** を選択します。

    ![オンライン展開のログイン フォーム](media/crm-v6s-pr.png "オンライン展開のログイン フォーム")

1. **使用可能な組織の一覧を表示する**チェックボックスをオンにする場合、**ログイン**をクリックした後、所属している組織の一覧が表示されます。 これにより、サービス エンドポイントを登録する組織を選択することができます。 選択しない場合は、既定の組織が使用されます。  
1. サーバーおよびログインのアカウントに関する指示される情報を入力し、**ログイン**をクリックします。  
  
<a name="BKMK_Register"></a>

## <a name="register-a-service-endpoint-step-for-an-event"></a>イベントのサービス エンドポイントの手順を登録する

サービス エンドポイントのイベントのための手順を登録するには、次の手順に従います。  
  
1. 対象組織のタブのタブの既存のサービス エンドポイントを選択します。  
1. **登録**メニューに移動し、**新しい手順の登録**をクリックします。  
1. 次の図のように、**新しい手順の登録**ダイアログ ボックスにアカウント作成イベントの情報を入力します。

    ![サービス エンドポイントの手順の作成](media/crm-v6s-pr-service-endpoint-step.png "サービス エンドポイントの手順の作成")
  
1. **新しい手順の登録** をクリックします。  
  
これで、CDS はアカウントが作成されるたびに実行コンテキストを含んだ現在のメッセージを Service Bus に投稿するようになります。 送信は非同期で実行され、すぐには実行されません。  
  
<a name="BKMK_Test"></a>

## <a name="test-the-endpoint-registration"></a>エンドポイント登録のテスト

エンドポイントを登録した後、それをテストできます。 プラグインからのサービス バス送信が実行されるには、ターゲット エンドポイント上でリスナーが実行されているか、またはキューが利用可能になっている必要があります。  
  
1. サービス エンドポイントを登録したのと同じ組織に関するキャンバスまたはモデル駆動型 Web アプリケーションを開きます。  
1. アカウント エンティティ レコードの新規作成
1. **取引先企業名** フィールドに、「Adventure Works Cycle」 などの取引先企業名を入力し、**保存** をクリックします。  
1. Azure Service Bus 投稿が実行されるまで 10 秒ほど待ちます。  
1. **Dynamics 365 - カスタム** 駆動型のアプリで、**設定 > システム > システム ジョブ**選択します。  
1. サービス エンドポイントに対して指定したのと同じ名前のシステム ジョブを開きます。 ステータスをチェックして、送信が成功、待機、失敗のいずれの状態かを確認します。  
  
必要な場合は、エンドポイントの登録を解除できます。解除するには、ツールのツリー ビューでエンドポイントを選択し、**登録を解除**をクリックします。  
  
### <a name="see-also"></a>関連項目

[CDS のための Azure 統合](azure-integration.md)<br />
[CDS での Microsoft Azure 統合の概要](azure-integration.md)
