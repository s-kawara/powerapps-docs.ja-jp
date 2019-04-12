---
title: カスタマイズ ファイルを編集するとき (モデル駆動型アプリ) | MicrosoftDocs
description: このトピックでは、カスタマイズを編集するとき、およびそれを行う可能なさまざまな方法を扱います
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="when-to-edit-the-customizations-file"></a>カスタマイズ ファイルを編集するとき

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/when-edit-customization-file -->

アンマネージド ソリューションの一部としてエクスポートされた customizations.xml ファイルは、特定のカスタマイズ タスクを実行するように編集できます。 ファイルを編集した後、アンマネージド ソリューションでエクスポートされる他のファイルとともに変更されたファイルを圧縮できます。 変更されたアンマネージド ソリューションをインポートして変更を適応します。  
  
 customizations.xml ファイルのような複雑な XML ファイルを編集するには、スキーマ検証をサポートするように設計されたプログラムを使用すれば、簡単にエラーを減らすことができます。 メモ帳のような単純なテキスト エディタを使用してこのファイルを編集することは可能ですが、このファイルの編集を熟知していない限りお勧めできません。 詳細については、「[スキーマ検証を使用したカスタマイズ ファイルの編集](edit-customizations-xml-file-schema-validation.md)」を参照してください。  
  
> [!IMPORTANT]
>  ソリューション コンポーネントの無効な XML または不適正な定義は、手動で編集されたアンマネージド ソリューションをインポートするときエラーが生じる可能性があります。  
  
## <a name="supported-tasks"></a>サポートするタスク  
 次のタスクを行うために、customization.xml ファイルを編集できます。  
  
 **リボンの編集**  
 このドキュメントでは、customization.xml ファイルを直接編集することでリボンを編集するプロセスについて説明します。 リボンの編集を簡単にするためのユーザー インターフェイスを提供するリボン エディターは、複数の担当者によって作成されました。 これまで最も好評なのが[リボン ワークベンチ](https://www.develop1.net/public/rwb/ribbonworkbench.aspx)です。 このプログラムのサポートについては、プログラムの発行元にお問い合わせください。  
  
 customization.xml を手動で編集することによるリボンの編集の詳細については、[リボンのカスタマイズ](customize-commands-ribbon.md) を参照してください。  
  
 **サイト マップの編集**  
 SDK では、customization.xml ファイルを直接編集することで SiteMap を編集するプロセスについて説明します。 ただし、サイト マップを作成または更新するには、モデル駆動型アプリでサイト マップ デザイナーを使用することをお勧めします。 詳細: [チュートリアル: サイト マップ デザイナーを使用してアプリのモデル駆動型アプリ サイト マップを作成する](../../maker/model-driven-apps/create-site-map-app.md)  
  
 [XrmToolBox Site Map Editor](https://www.xrmtoolbox.com/plugins/MsCrmTools.SiteMapEditor/) など、コミュニティで開発されたサイト マップ エディターを使用することもできます。   
  
 詳細については、「[SiteMap を使用してアプリケーションのナビゲーションを変更する](/developer/customize-dev/change-application-navigation-using-sitemap.md)」を参照してください。  
  
 **FormXml を編集**  
 FormXml は、エンティティ フォームとダッシュボードを定義するために使用されます。 アプリケーションのフォーム エディターおよびダッシュボード デザイナーは、この目的のために最もよく使用されるツールです。 customizations.xml ファイルを編集する方法もあります。 詳細については、[エンティティ フォームのカスタマイズ](customize-entity-forms.md) および [ダッシュボードの作成](create-dashboard.md) を参照してください。  
  
 **保存済みクエリの編集**  
 エンティティのビューの定義を customizations.xml ファイルに含め、手動で編集することができます。 アプリケーションのビュー エディターは、この目的ため最もよく使用されるツールです。 customizations.xml ファイルを編集する方法もあります。 詳細については、[エンティティ ビューのカスタマイズ](customize-entity-views.md) を参照してください。  
  
 **ISV.Config の編集**  
  Common Data Service では、リボンがアプリケーションの拡張方法を提供します。 ISV.Config に引き続き残っている唯一の機能は、サービス カレンダーの外観をカスタマイズすることです。 詳細については、[サービス カレンダーの外観の構成](/dynamics365/customer-engagement/developer/customize-dev/service-calendar-appearance-configuration) を参照してください。  
  
## <a name="unsupported-tasks"></a>サポートされないタスク  
 エクスポートされた customizations.xml ファイルを編集することで、他のソリューション コンポーネントを定義することはサポートされていません。 このフェーズでは次のタスクを実行します。  
  
-   エンティティ  
  
-   属性  
  
-   エンティティの関連付け  
  
-   エンティティ メッセージ  
  
-   オプション セット  
  
-   Web リソース  
  
-   プロセス (Workflow)  
  
-   プラグイン アセンブリ  
  
-   SDK メッセージ処理手順  
  
-   サービス エンドポイント  
  
-   [レポート]  
  
-   つながりロール  
  
-   記事テンプレート  
  
-   契約テンプレート  
  
-   電子メール テンプレート  
  
-   差し込み印刷用テンプレート   
  
-   セキュリティ ロール  
  
-   Field Security Profiles  
  

### <a name="see-also"></a>関連項目  
 [カスタマイズ XML リファレンス](customization-xml-reference.md)   
 [カスタマイズ ソリューション ファイルのスキーマ](../common-data-service/customization-solutions-file-schema.md)   
 [リボン コアのスキーマ](ribbon-core-schema.md) [リボン タイプのスキーマ](ribbon-types-schema.md) [リボン WSS のスキーマ](ribbon-wss-schema.md)   
 [Form XML schema](form-xml-schema.md)   
 [カスタマイズ ファイルのスキーマ サポート](edit-customizations-xml-file-schema-validation.md)
