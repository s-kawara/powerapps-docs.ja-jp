---
title: ソリューションをアンインストールまたは削除する (Common Data Service) | Microsoftのドキュメント
description: このドキュメントでは、Dynamics 365 の管理対象ソリューションとアンマネージドソリューションのアンインストールと削除の操作について説明します。
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
# <a name="uninstall-or-delete-a-solution"></a>ソリューションのインストールまたは削除

マネージド ソリューションとアンマネージド ソリューションは同じ方法で削除できますが、その結果として行われる処理が大きく異なります。 マネージド ソリューションの場合、削除したマネージド ソリューションはアンインストールされます。  
  
<a name="BKMK_DeleteSolution"></a>   
## <a name="delete-a-solution"></a>ソリューションの削除  
 削除するソリューションの種類によって、次のどちらかの**削除の確認**メッセージが表示されます。  
  
 **マネージド ソリューション**  
 マネージド ソリューションを削除しようとしています。 ソリューションとそのコンポーネントのすべてが削除されます。 この操作を元に戻すことはできません。 このソリューションがアンインストールされるまでに数分かかる場合があります。 アンインストール開始後は、この操作を取り消すことはできません。 続行しますか?  
  
 **アンマネージド ソリューション**  
 アンマネージド ソリューションを削除しようとしています。 ソリューションは削除されますが、このソリューションに含まれるコンポーネントは削除されません。 この操作を元に戻すことはできません。 続行しますか?  
  
 ソリューションをプログラムから削除する場合は、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Delete*>   メソッド。 詳細: [ソリューションを削除する](work-solutions.md#BKMK_DeleteSolution)  
  
<a name="BKMK_UinstallAManagedSolution"></a>   
### <a name="uninstall-a-managed-solution"></a>管理ソリューションのアンインストール  
 マネージド ソリューションの場合、削除したソリューションはアンインストールされます。 ソリューションで定義されるすべてのコンポーネントが削除されます。  
  
> [!IMPORTANT]
>  マネージド ソリューションをアンインストールすると、ソリューションの一部となっているユーザー定義のエンティティに格納したデータや、ソリューションの一部となっているシステム エンティティのユーザー定義属性に格納したデータは失われます。  
  
<a name="BKMK_DeleteUnmanagedSolution"></a>   
### <a name="delete-an-unmanaged-solution"></a>アンマネージド ソリューションの削除  
 アンマネージド ソリューションは、ソリューション コンポーネントのグループです。 ソリューションを削除すると、データベースから単一のソリューション レコードが削除されます。 ソリューション コンポーネントは、削除されたソリューションに影響されず、システムに残ります。  
  
<a name="BKMK_AccessSolutionsGridWithUrl"></a>   
## <a name="access-the-solutions-list-with-a-url"></a>URL を使用したソリューション一覧へのアクセス  
 ソリューションの一覧に直接移動する必要がある場合は、次の URL を使用できます。  
  
```http
<organization root url>/tools/Solution/home_solution.aspx?etn=solution  
```  
  
### <a name="see-also"></a>関連項目  
 [拡張機能のパッケージ化および配布](/dynamics365/customer-engagement/developer/package-distribute-extensions-use-solutions)   
 [ソリューションの削除](work-solutions.md#BKMK_DeleteSolution)   
 [ソリューションの概要](introduction-solutions.md)   
 [ソリューション開発の計画](/dynamics365/customer-engagement/developer/plan-solution-development)   
 [ソリューション コンポーネントおよび依存関係の追跡](dependency-tracking-solution-components.md)   
 [マネージド ソリューションの作成](create-install-update-managed-solution.md#BKMK_CreateManagedSolution)   
 [アンマネージド ソリューションのエクスポート](create-export-import-unmanaged-solution.md#BKMK_UnmanagedSolution)   
 [アンマネージド ソリューションのインポート](create-export-import-unmanaged-solution.md#BKMK_ImportUnmanagedSolution)   
 [マネージド ソリューションの作成](create-install-update-managed-solution.md#BKMK_CreateManagedSolution)   
 [複数の言語をサポートするソリューションの作成](create-solutions-support-multiple-languages.md)   
 [マネージド ソリューションのインストール](create-install-update-managed-solution.md#BKMK_InstallManagedSolution)
