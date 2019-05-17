---
title: 'サンプル: XRM ツール API のクイック スタート (Common Data Service)| Microsoft Docs'
description: ''
ms.custom: ''
ms.date: 03/27/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: samples
applies_to:
  - Dynamics 365 (online)
ms.assetid: 060d45bb-b7fd-48bd-ab8f-629c1b8bc1dc
caps.latest.revision: 20
author: MattB-msft
ms.author: nabuthuk
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-quick-start-for-xrm-tooling-api"></a>サンプル: XRM ツール API のクイック スタート

クイックスタート サンプルは、XRM ツール API を使用して Common Data Service インスタンスに接続し、作成、更新、取得、削除などエンティティでの基本的な操作方法を表す .NET Framework マネージド コード サンプルです。 XRM ツールの詳細については、「[XRM ツールを使用して Windows のクライアント アプリケーションを作成](build-windows-client-applications-xrm-tools.md)」を参照してください。

サンプルのダウンロード: [XRM ツール API に関する作業](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/Xrm%20Tooling/Quick%20start%20for%20XRM%20Tooling)。

## <a name="how-to-run-the-sample"></a>サンプルを実行する方法

1. [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/Xrm%20Tooling/Quick%20start%20for%20XRM%20Tooling) からサンプルをダウンロードして展開します。  
1. `Quick start for XRM Tooling\C#\QuickStartXRMToolingWPFClient.sln` ファイル Visual Studio で開きます。  
1. **F5** キーを押して、プログラムをコンパイルして実行します。  


## <a name="demonstrates"></a>説明

- このサンプル コードは、共通ログイン コントロールに対して認証と資格情報のキャッシュと再利用の組み込みのサポートを提供する、**CRM 用 WPF アプリケーション** SDK テンプレートを使用して作成されます。 Visual Studio の共通ログイン コントロールおよび SDK テンプレートの使用方法の詳細については、[XRM ツール共通ログイン コントロールを使用する](use-xrm-tooling-common-login-control-client-applications.md)を参照してください。  
- ヘルパー コードは、Common Data Service への接続を確立するために使用されません。  
- Common Data Service に接続後、このサンプルは、取引先企業エンティティに対して、基本的な作成、更新、取得、および削除操作を行います。  
- サンプルが初めて実行されるとき、ユーザーの資格情報を `c:\Users\`*`<username>`*`\AppData\Roaming\Microsoft\QuickStartXRMToolingWPFClient` フォルダーの構成ファイル (`Default_QuickStartXRMToolingWPFClient.exe.config`) に保存し、その後、Common Data Service にサインインするために、ユーザーが保存された資格情報を使用するか、新しい資格情報を使用するかを実行時に求めます。  
- 問題が発生した場合、トラブルシューティングを助けるために、次のログ ファイルを生成します。  
- Login_ErrorLog.log: サインイン エラーを報告するため。 このファイルは、`C:\Users\`*`<username>`*`\AppData\Roaming\Microsoft\QuickStartXRMToolingWPFClient` にあります。  
- QuickStartXRMToolingWPFClient.log: 操作エラーを報告するため。 このファイルは、実行可能ファイルと同じ場所の、自分の Visual Studio プロジェクトのデバッグ フォルダーで使用できます。  

### <a name="see-also"></a>関連項目

[XRM ツール共通ログイン コントロールを使用する](use-xrm-tooling-common-login-control-client-applications.md)<br />
[XRM ツールを使用して Windows のクライアント アプリケーションを作成する](build-windows-client-applications-xrm-tools.md)<br />

