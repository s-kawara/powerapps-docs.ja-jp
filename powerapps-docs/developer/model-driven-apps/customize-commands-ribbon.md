---
title: コマンドとリボンのカスタマイズ (モデル駆動型アプリ) | MicrosoftDocs
description: Common Data Service は、エンティティおよびクライアントに応じてさまざまな方法でコマンドを表示します。 Web アプリケーションの大抵の場所で、リボンの代わりにコマンド バーが表示されます。 また、タブレット PC 用 Dynamics 365 はリボンとして定義されたデータを使用して、タッチ操作のために最適化されたコマンド バーを使用してどのコマンドを使用できるかコントロールします。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 926364b0-ede6-00e9-39d4-5aae5e00be0b
author: JimDaly
ms.author: jdaly
manager: shilpas
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="customize-commands-and-the-ribbon"></a>コマンド、およびリボンをカスタマイズする

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/customize-commands-ribbon -->

 Common Data Service は、エンティティおよびクライアントに応じてさまざまな方法でコマンドを表示します。 Web アプリケーションの大抵の場所で、リボンの代わりに*コマンド バー*が表示されます。 また、Dynamics 365 for Tablets はリボンとして定義されたデータを使用して、タッチ操作のために最適化されたコマンド バーを使用してどのコマンドを使用できるかコントロールします。  
  
 コマンド バーは、より良いパフォーマンスを提供します。 リボンは、特定のエンティティ フォームでは Web アプリケーションで引き続き表示され、Dynamics 365 for Outlook のリスト ビューにも使用されます。  
  
 コマンド バーとリボンの両方が同じ基礎となる XML データを使用して、表示するコマンド、コマンドを有効にする時期、およびコマンドの実行内容を定義します。  
  
 このセクションのトピックでは、理解しておく必要のある重要な概念と、コマンド バーまたはリボンをカスタマイズするときに実行する一般的なタスクについて説明します。  
  
> [!NOTE]
>  基礎となる XML スキーマはリボンとしてコマンドを表示するように設計されているため、*リボン* という用語はドキュメントで引き続き使用されます。  
  
 SDK では、customization.xml ファイルを直接編集することでリボンを編集するプロセスについて説明します。 リボンの編集を簡単にするためのユーザー インターフェイスを提供するリボン エディターは、複数の担当者によって作成されました。 現在、Codeplex と他の場所で使用できるプロジェクトは以下のとおりです。  
  
- [リボン ワークベンチ](http://www.develop1.net/public/rwb/ribbonworkbench.aspx)  
  
- [MS CRM 2011 : Pragma Toolkit : Ribbon, Site Map Editor (MS CRM 2011 : Pragma Toolkit : リボン、サイト マップのエディター)](http://pragmatoolkit.codeplex.com/)  
  
- [CRM 2011 Visual Ribbon Editor (CRM 2011 Visual のリボン エディター)](http://crmvisualribbonedit.codeplex.com/)  
  
  これらのプログラムを使用するためのサポートまたヘルプを得るには、プログラムの発行元にお問い合わせください。  
  
  
## <a name="see-also"></a>関連項目  

 [リボン コアのスキーマ](ribbon-core-schema.md)  
 [リボン タイプのスキーマ](ribbon-types-schema.md)  
 [リボン WSS のスキーマ](ribbon-wss-schema.md)<br/> 
 [サンプル: リボン定義をエクスポートする](sample-export-ribbon-definitions.md)<br/> 
 [モデル駆動型アプリでクライアント スクリプトを使用してビジネス ロジックを適用](client-scripting.md)
