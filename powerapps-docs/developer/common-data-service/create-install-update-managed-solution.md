---
title: マネージド ソリューションの作成、インストール、および更新 (Common Data Service) | Microsoft Docs
description: <Description>
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: shmcarth
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-install-and-update-a-managed-solution"></a>管理ソリューションの作成、インストール、および更新

アンマネージド ソリューションをマネージド ソリューションとしてエクスポートして、マネージド ソリューションを作成します。 マネージド ソリューションを使用する組織では、マネージド ソリューションと、そのマネージド ソリューション用に作成した更新をインストールします。  
  
 詳細: [カスタマイズでのソリューションの使用](/dynamics365/customer-engagement/customize/use-solutions-for-your-customizations)。  
  
<a name="BKMK_CreateManagedSolution"></a>   

## <a name="create-a-managed-solution"></a>マネージド ソリューションの作成  
 マネージド ソリューションを作成するには、まず、アンマネージド ソリューションを作成する必要があります。 アンマネージド ソリューションを作成する方法の詳細については、[アンマネージド ソリューションの作成](create-export-import-unmanaged-solution.md#BKMK_CreateUnmanagedSolution) を参照してください。  
  
 マネージド ソリューションをエクスポートするときに、**パッケージの種類**ダイアログ ボックスの**管理**オプションを選択して、マネージド ソリューションを作成します。  
  
 管理ソリューションには、カスタマイズ済みのカスタマイズ可能なソリューション コンポーネントのみが含まれます。 これは、ソリューションがインストールされているシステムの既存のソリューション コンポーネントが誤って変更されるのを防ぐだけではなく、管理ソリューションのサイズをより小さい状態に保ちます。  
  
 マネージド ソリューションを作成する最後の手順を実行する前に、マネージド ソリューションをインストールするユーザーに実行を許可しないカスタマイズ機能が含まれていないかどうかを調べる必要があります。 各ソリューション コンポーネントには、実行を許可するカスタマイズ機能を制御する一連の管理プロパティが含まれています。 既定の設定ではすべてのカスタマイズ機能が許可されます。 詳細: [マネージド プロパティの使用](use-managed-properties.md)  
  
 <xref:Microsoft.Crm.Sdk.Messages.ExportSolutionRequest> メッセージを使用して、マネージド ソリューションをプログラムで作成できます。 詳細: [ソリューションのエクスポートまたはパッケージ化](work-solutions.md#BKMK_ExportPackageSolution)  
  
> [!IMPORTANT]
>  マネージド ソリューションの作成に使用した組織に、そのマネージド ソリューションをインポートし直すことはできません。  
  
<a name="BKMK_InstallManagedSolution"></a>   

## <a name="install-a-managed-solution"></a>マネージド ソリューションのインストール  
 マネージド ソリューションをインストールする方法は、アンマネージド ソリューションをインポートする方法と同じです。 ただし、ソリューションのパッケージ方法に違いがあります。  
  
> [!IMPORTANT]
>  ソリューションをインストールまたはカスタマイズを公開すると、標準システム操作を妨げる可能性があります。 ユーザーに対する影響が最小であるうちに、ソリューションのインポートを予定することを推奨します。  
  
 ソリューションが正常にインポートされなかった場合は、ダイアログ ボックスの**ログのダウンロード**をクリックしてレポートをダウンロードできます。このレポートには、マネージド ソリューションのインポート中に発生したエラーについての情報が記載されています。 このログ ファイルは XML ドキュメントで、Office Excel で開くように構成されています。  
  
 <xref:Microsoft.Crm.Sdk.Messages.ImportSolutionRequest> メッセージを使用して、マネージド ソリューションをプログラムでインポートまたは更新できます。 このメッセージを使用しているときは、正常に実行されたインポートについての詳細情報を含む `ImportJob` エンティティ レコードの参照を要求することができます。 詳細: [ソリューションのインストールまたはアップグレード](work-solutions.md#BKMK_InstallUpgradeSolution)  
  
 <xref:Microsoft.Crm.Sdk.Messages.ImportSolutionRequest> は <xref:Microsoft.Xrm.Sdk.Messages.ExecuteAsyncRequest> を使用して呼び出すことができます。 詳細: [バックグラウンドのメッセージを実行する (非同期)](/dynamics365/customer-engagement/developer/org-service/use-messages-request-response-classes-execute-method#bkmk_executeasync)  
  
 インストールできるソリューションのサイズには制限があります。 詳細: [インポートするソリューションの最大サイズ](create-export-import-unmanaged-solution.md#BKMK_MaxSizeOfSolution)  
  
<a name="BKMK_UpdateManagedSolution"></a>   

### <a name="update-a-managed-solution"></a>マネージド ソリューションの更新  
 インストールするマネージド ソリューションが既に組織に存在していると、ソリューションのインポート ダイアログに、次のオプションが表示されます。  
  
 **カスタマイズを維持 (推奨)**  
 このオプションは、コンポーネントに対して実行された非管理カスタマイズをすべて維持します。その代わり、このソリューションに含まれる更新によっては有効にならない場合があります。  
  
 **カスタマイズを上書き**  
 このオプションは、このソリューションに含まれるコンポーネントに対してこれまでに実行された非管理カスタマイズをすべて上書きします。 このソリューションに含まれるすべて更新が有効になります。  
  
> [!NOTE]
>  カスタマイズとソリューションの動作の競合に関する問題を調査するときは、マネージド ソリューションをインストールするユーザーに**カスタマイズを上書き**オプションを使用するように指示した方が適切であると考えられます。 必ず、最初にアンマネージド ソリューションをエクスポートして、必要に応じて、それらを再適用できるようにしておく必要があります。  
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 ソリューションを使用した拡張機能のパッケージ化および配布](/dynamics365/customer-engagement/developer/package-distribute-extensions-use-solutions)   
 [ソリューションの概要](introduction-solutions.md)   
 [ソリューション開発の計画](/dynamics365/customer-engagement/developer/plan-solution-development)   
 [ソリューション コンポーネントおよび依存関係の追跡](dependency-tracking-solution-components.md)   
 [アンマネージド ソリューションの作成、エクスポート、またはインポート](create-export-import-unmanaged-solution.md)   
 [ソリューションのアンインストールまたは削除](uninstall-delete-solution.md)   
 [カスタマイズ ソリューション ファイルのスキーマ](/dynamics365/customer-engagement/developer/customize-dev/customization-solutions-file-schema)