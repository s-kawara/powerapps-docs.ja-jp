---
title: 特定のバージョンのソリューションをエクスポートする (アプリ用 Common Data Service) | Microsoft Docs
description: ソリューションに対してエクスポートする Dynamics 365 のバージョンを対象にして管理する方法を学習します。
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
# <a name="export-a-solution-for-a-specific-version"></a>特定のバージョンのソリューションをエクスポートする

> [!NOTE]
>  このトピックでは、アプリ用 Common Data Service のメジャー バージョンに対するマイナー バージョンの更新で利用できる機能について説明します。 この機能は、アプリ用 CDS の初回リリースでは利用できませんが、マイナー バージョンの更新時に追加機能が含まれます。  

 各アプリ用 CDS の新しいバージョンには、以前のバージョンにはない機能が含まれています。 新しい機能を使用するソリューションは、以前のバージョンの組織にインポートできません。 旧バージョンの組織からエクスポートしたソリューションは新しいバージョンの組織にインポートできます。  

 ソリューションの定義に使用する組織をアップグレードした後も、以前のバージョンを対象とするソリューションをエクスポートできます。 下位のターゲットのバージョンを選択すると、そのバージョン以降に導入された機能に依存するソリューション コンポーネントは、エクスポートするソリューションに含まれません。  

> [!NOTE]
>  既定のソリューションをエクスポートするときに、以前のバージョンは選択できません。  

<a name="BKMK_ExportSolutionForVersion"></a>   

## <a name="target-a-specific-version-when-you-export-a-solution"></a>ソリューションをエクスポートするとき、特定のバージョンを対象にする  
 アプリ用 CDS からソリューションをエクスポートする場合、特定の Dynamics 365 バージョンのソリューションを対象にするオプションがあります。 Dynamics 365 8.2.0.0 バージョンの場合、オプションは 8.2 (既定)、8.1 および 8.0 です。 8.0 を選択すると、8.1.0.0 で導入されたすべての新しい機能はエクスポートされたソリューションには含まれず、以前の 8.1.0.0 バージョンを使用しているすべての組織はそのソリューションをインストールできます。  

 以前のバージョンを対象とするソリューションをエクスポートするときに、エクスポート ダイアログ ボックスは 2 つのメッセージを表示する場合があります。  

 **このソリューションは、対象の Dynamics 365 バージョンをサポートしています。**  
 これは、ソリューション内のソリューション コンポーネントが、そのバージョン以降に導入された機能やソリューション コンポーネントに依存しないことを意味します。  

 **エクスポートの一部として、次のコンポーネントが削除または変更されます**  
 このメッセージの下の表は、変更された、またはエクスポートしたソリューションに含まれていないソリューション コンポーネントの項目を示します。  

 ダイアログ ボックスに表示される情報は、エクスポートしたソリューション ファイルにもあります。 特定のバージョンを対象にソリューションをエクスポートすると、ファイルの名前は、次の名前付け規則を使用して、対象のソリューションを指定します: *ソリューション名*<em>*Solution_Version_Number*_target_CRM\\</em>*対象の Dynamics 365 バージョン番号*.zip。 たとえば、バージョン 8.0 を対象にエクスポートされる、ソリューションのバージョンが 2.0 で、名前がサンプル ソリューションのアンマネージド ソリューションの場合は、SampleSolution_2_0_target_CRM_8.0.zip という名前になります。 この圧縮されたファイルの内容を抽出するときに、どのアクションが実行されたかの詳細なデータを含む filteredcomponents.xml ファイルがあることに気づきます。 Excel を使用してこのファイルを開き、どのソリューション コンポーネントが編集または削除されたかのレポートを表示できます。  

<a name="BKMK_Changes"></a>   

## <a name="what-changes-are-applied-to-a-solution-exported-for-an-earlier-version"></a>どのような変更は、以前のバージョンのためにエクスポートするソリューションに適用されますか。  
 Dynamics 365 6.0.0.0 リリース以降は、各タイプのソリューション コンポーネントには、`IntroducedVersion` プロパティがあります。 この値は、作成時に、ソリューション コンポーネントが関連付けられたソリューションの現在のバージョン番号を取り込みます。 Microsoft によって導入されたすべてのソリューション コンポーネントは、バージョン番号がアプリ用 CDS バージョンに対応する非表示のシステム ソリューションの一部です。  

<!--
| IntroducedVersion Value |                                                             Solution components introduced                                                             |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|         5.0.0.0         | Before [!INCLUDE[pn_crm_2013_shortest](../includes/pn-crm-2013-shortest.md)] and [!INCLUDE[pn_crm_online_fall13](../includes/pn-crm-online-fall13.md)] |
|         6.0.0.0         |    [!INCLUDE[pn_crm_2013_shortest](../includes/pn-crm-2013-shortest.md)] and [!INCLUDE[pn_crm_online_fall13](../includes/pn-crm-online-fall13.md)]     |
|         6.1.0.0         |     [!INCLUDE[pn_crm_2013_sp](../includes/pn-crm-2013-sp.md)] and [!INCLUDE[pn_v6_online_ur1_shortest](../includes/pn-v6-online-ur1-shortest.md)]      |
|         7.0.0.0         |                                  [!INCLUDE[pn_crm_2015_and_online_full](../includes/pn-crm-2015-and-online-full.md)]                                   |
|         7.1.0.0         |                                  [!INCLUDE[pn_crm_online_2015_update_1](../includes/pn-crm-online-2015-update-1.md)]                                   |
|         8.0.0.0         |               [!INCLUDE[pn_crm_online_2016_update_shortest](../includes/pn-crm-online-2016-update-shortest.md)] and CRM 2016 on-premises               |
|         8.1.0.0         |          [!INCLUDE[pn_crm_8_1_0_online](../includes/pn-crm-8-1-0-online.md)] and [!INCLUDE[pn_crm_8_1_0_op](../includes/pn-crm-8-1-0-op.md)]           |
|         8.2.0.0         |                                            [!INCLUDE[pn_crm_8_2_0_both](../includes/pn-crm-8-2-0-both.md)]                                             |
|         9.0.0.0         |                                          [!INCLUDE[pn_crm_9_0_0_online](../includes/pn-crm-9-0-0-online.md)]                                           |
-->

 `IntroducedVersion`データは、対象のバージョンと一致するソリューションをエクスポートするときに使用されます。 これにより、次の 3 つのアクションが実行される可能性があります。  

 **削除**  
 対象のバージョンに存在しない、または対象のバージョンで動作できないコンポーネントとの依存関係が含まれているソリューション コンポーネントは、ソリューションに追加できません。  

 **修正**  
 削除されたソリューション コンポーネントとソリューション コンポーネントが依存していると、可能な場合は、ソリューション コンポーネントは変更されて依存関係が削除されます。 たとえば、フォーム定義がそのバージョンに存在しない属性を参照する場合、フォームが変更されて参照が削除されます。 ソリューション コンポーネントを変更して依存関係を削除できない場合は、ソリューション コンポーネントが削除されます。  

 **置換**  
 ソリューション コンポーネントが対象のバージョンに存在していたが、削除されるソリューション コンポーネントとの依存関係を持つように変更さた場合、ソリューション コンポーネントは対象とするバージョンに定義されたソリューション コンポーネントの定義で上書きされます。  

<a name="BKMK_TargetVersion"></a>   

## <a name="select-a-target-version-programmatically"></a>プログラムで対象とするバージョンを選択する  

 ソリューションをプログラムでエクスポートするには、<xref:Microsoft.Crm.Sdk.Messages.ExportSolutionRequest> を使用します。 Dynamics 365 6.0.0.0 以降、このメッセージには新しいオプションの<xref:Microsoft.Crm.Sdk.Messages.ExportSolutionRequest.TargetVersion>`String` プロパティが含まれ、以前のバージョンにエクスポートしたい場合、これを使用して「8.0.0.0」に設定できます。  

### <a name="see-also"></a>関連項目  
 [ソリューションを使用した拡張機能のパッケージ化および配布](/dynamics365/customer-engagement/developer/package-distribute-extensions-use-solutions)   
 [アンマネージド ソリューションの作成、エクスポート、またはインポート](create-export-import-unmanaged-solution.md)   
 [マネージド ソリューションの作成、インストール、および更新](create-install-update-managed-solution.md)   
 [マネージド ソリューションの保守](maintain-managed-solutions.md)   
 [カスタマイズ ガイド: カスタマイズでのソリューションの使用](http://go.microsoft.com/fwlink/p/?LinkID=322003)
