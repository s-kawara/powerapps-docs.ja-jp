---
title: ソリューション コンポーネントの依存関係の追跡 (Common Data Service) | Microsoft Docs
description: 'ソリューション コンポーネントの依存関係は、ソリューションの操作の信頼性を確保するのに役立ちます。 [依存関係の表示] をクリックすることによりアプリケーション内に表示することができます'
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
# <a name="dependency-tracking-for-solution-components"></a>ソリューション コンポーネントの依存関係の追跡

ソリューションはソリューション コンポーネントで構成されます。 Common Data Service の **ソリューション** 領域を使用して、ソリューション コンポーネントを作成または追加します。 この操作をプログラムによって実行する場合は、<xref:Microsoft.Crm.Sdk.Messages.AddSolutionComponentRequest> メッセージを使用するか、`SolutionUniqueName` パラメーターを含むソリューション コンポーネントを作成または更新する任意のメッセージを使用します。  
  
 ソリューション コンポーネントは、多くの場合、他のソリューション コンポーネントに依存しています。 他のソリューション コンポーネントへの依存関係があるソリューション コンポーネントは削除できません。 たとえば、一般に、カスタマイズされたリボンにはアイコンの表示やスクリプトを使用した操作を行うためにイメージまたはスクリプト Web リソースが必要になります。 カスタマイズされたリボンがソリューションに存在する場合、そのリボンが使用する Web リソースが必要です。 Web リソースを削除する前に、カスタマイズされたリボン内の対象 Web リソースへの参照を削除する必要があります。 ソリューション コンポーネントの依存関係をアプリケーションで表示するには、**依存関係を表示します**をクリックします。  
  
 このトピックでは、ソリューションに含めることができるソリューション コンポーネントの種類と、相互の依存関係について説明します。  
  
<a name="bkmk_SolutionComponents"></a>   

## <a name="all-solution-components"></a>すべてのソリューション コンポーネント  
 使用できるソリューション コンポーネントの種類の完全な一覧は、システム `componenttype` グローバル オプション セット内にあります。 このプロパティの値のサポートされる範囲は、ファイル `OptionSets.cs` または `OptionSets.vb` がプロジェクトに含まれている場合に使用できます。 ただし、一覧にある多くのソリューション コンポーネントの種類は内部のみで使用され、一覧にはソリューション コンポーネント間の関係に関する情報は示されていません。  
  
<a name="BKMK_SolutionComponentDependencies"></a>   

## <a name="solution-component-dependencies"></a>ソリューション コンポーネントの依存関係  
 ソリューション コンポーネントの依存関係は、ソリューションの操作の信頼性を確保するのに役立ちます。 ソリューション コンポーネントの依存関係により、普通はうっかり実行してソリューションで定義されているカスタマイズを壊してしまうような操作を防ぐことができます。 ソリューションをインポートまたは削除することによってマネージド ソリューションをインストールまたはアンインストールできるかどうかは、これらの依存関係によって決まります。  
  
 ソリューション フレームワークは自動的にソリューション コンポーネントの依存関係を追跡します。 ソリューション コンポーネントを操作するたびに、システム内の他のコンポーネントへの依存関係が自動的に計算されます。 依存関係情報を使用してシステムの整合性を保つことで、不整合な状態をもたらす可能性のある操作を防ぎます。  
  
 依存関係の追跡の結果、次の動作が適用されます。  
  
- システム内の他のコンポーネントが依存しているコンポーネントの削除は禁止されます。  
  
- コンポーネントの不足により他のシステムへのソリューションのインポートが失敗する可能性がある場合、ソリューションのエクスポート時に警告が表示されます。  
  
   ソリューション開発者が、依存するコンポーネントが組織内に存在することを前提にしてソリューションをインストールした場合には、エクスポート時の警告を無視できます。 たとえば、あらかじめインストールされている「基本」ソリューション上にインストールするように設計されたソリューションを作成する場合が、これに該当します。  
  
- すべての必須コンポーネントがソリューションに含まれておらず、ターゲット システムにも存在しない場合、ソリューションのインポートは失敗します。  
  
  -   また、マネージド ソリューションをインポートする場合は、必要なすべてのコンポーネントがソリューションのパッケージの種類と一致している必要があります。 マネージド ソリューションのコンポーネントは他のマネージド コンポーネントのみに依存できます。  
  
  ソリューション コンポーネントの依存関係には 3 種類あります。  
  
  **内部ソリューション**  
  内部依存関係は Common Data Service によって管理されます。 一方のソリューション コンポーネントが存在するために、他方のソリューション コンポーネントの存在が欠かせないという関係がある場合は、内部依存関係が存在します。  
  
  **公開済み**  
  2 つのソリューション コンポーネントを関連付けて公開すると、公開済み依存関係が作成されます。 この種類の依存関係を削除するには、関連付けを削除した後、エンティティを再び公開します。  
  
  **非公開**  
  更新中の公開可能なソリューション コンポーネントの非公開バージョンには非公開依存関係が適用されます。 ソリューション コンポーネントを公開すると、公開済み依存関係になります。  
  
  内部ソリューション依存関係は、ソリューション コンポーネントの操作に他のソリューション コンポーネントの操作が必要な依存関係です。 たとえば、エンティティを削除する場合、すべてのエンティティ属性も同時に削除されることが想定されます。 他のエンティティとのエンティティの関係も削除されます。  
  
  ただし、内部依存関係は、最終的には公開済み依存関係になる可能性があり、そうした場合は手動での操作が必要です。 たとえば、エンティティ フォームに検索フィールドを含めてから関係の主エンティティを削除する場合、関連するエンティティ フォームから検索フィールドを削除してフォームを公開するまで、主エンティティの削除は完了できません。  
  
  ソリューションをプログラムによって操作する場合、`Dependency` エンティティに関連付けられたメッセージを使用できます。 コンポーネントの削除またはソリューションのアンインストールを実行する前に存在する可能性がある依存関係を特定するために使用可能なメッセージについては、[依存関係エンティティ](/reference/entities/dependency.md) を参照してください。  
  
<a name="BKMK_CheckForSolutionComponentDependencies"></a>   
## <a name="check-for-solution-component-dependencies"></a>ソリューション コンポーネントの依存関係の確認  
 ソリューションを編集する場合、他のソリューション コンポーネントとの公開済み依存関係があるために、ソリューション コンポーネントを削除できないことがあります。 または、マネージド ソリューション内のいずれかのコンポーネントが他のアンマネージド ソリューションのカスタマイズに使用されているためにマネージド ソリューションをアンインストールできない場合があります。  
  
 次の表に、ソリューション コンポーネントの依存関係に関するデータの取得に使用できるメッセージを表示します。  
  
|メッセージ|説明|  
|-------------|-----------------|  
|<xref:Microsoft.Crm.Sdk.Messages.RetrieveDependentComponentsRequest>|ソリューション コンポーネントに直接依存するソリューション コンポーネントの依存関係の一覧が返されます。<br /><br /> たとえば、このメッセージをグローバル オプション セットのソリューション コンポーネントに使用する場合、グローバル オプション セットのソリューション コンポーネントを参照するオプション セット属性を表すソリューション コンポーネントの依存関係レコードが返されます。<br /><br /> このメッセージを取引先企業エンティティのソリューション コンポーネント レコードに使用する場合、そのエンティティの属性、ビュー、およびフォームを表すすべてのソリューション コンポーネントの依存関係レコードが返されます。|  
|<xref:Microsoft.Crm.Sdk.Messages.RetrieveRequiredComponentsRequest>|他のソリューション コンポーネントが直接依存する、ソリューション コンポーネントの依存関係の一覧が返されます。 このメッセージは `RetrieveDependentComponentsRequest` メッセージの逆の処理を行います。|  
|<xref:Microsoft.Crm.Sdk.Messages.RetrieveDependenciesForDeleteRequest>|ソリューション コンポーネントの削除を妨げる可能性があるソリューション コンポーネントのすべての依存関係の一覧が返されます。|  
|<xref:Microsoft.Crm.Sdk.Messages.RetrieveDependenciesForUninstallRequest>|マネージド ソリューションのアンインストールを妨げる可能性があるソリューション コンポーネントのすべての依存関係の一覧が返されます。|  
  
<a name="BKMK_RootSolutionComponents"></a>   
## <a name="common-solution-components"></a>共通ソリューション コンポーネント  
 次に、ソリューション ページを使用してソリューション コンポーネントを追加または削除する際、ユーザーが直接操作するアプリケーションおよびコンポーネントに表示される、ソリューション コンポーネントを示します。 その他の種類のソリューション コンポーネントの存在は、これらのソリューション コンポーネントの 1 つまたは複数に依存します。  
  
||||  
|-|-|-|  
|[アプリケーション リボン (RibbonCustomization)](dependency-tracking-solution-components.md#BKMK_RibbonCustomization)|[エンティティ (Entity)](dependency-tracking-solution-components.md#BKMK_Entity)|[レポート (Report)](dependency-tracking-solution-components.md#BKMK_Report)|  
|[記事テンプレート (KBArticleTemplate)](dependency-tracking-solution-components.md#BKMK_KBArticleTemplate)|[フィールド セキュリティ プロファイル (FieldSecurityProfile)](dependency-tracking-solution-components.md#BKMK_FieldSecurityProfile)|[SDK メッセージ処理手順 (SDKMessageProcessingStep)](dependency-tracking-solution-components.md#BKMK_SDKMessageProcessingStep)|  
|[つながりロール (ConnectionRole)](dependency-tracking-solution-components.md#BKMK_ConnectionRole)|[差し込み印刷用テンプレート (MailMergeTemplate)](dependency-tracking-solution-components.md#BKMK_MailMergeTemplate)|[セキュリティ ロール (Role)](dependency-tracking-solution-components.md#BKMK_Role)|  
|[契約テンプレート (ContractTemplate)](dependency-tracking-solution-components.md#BKMK_ContractTemplate)|[オプション セット (OptionSet)](dependency-tracking-solution-components.md#BKMK_OptionSet)|[サービス エンドポイント (ServiceEndpoint)](dependency-tracking-solution-components.md#BKMK_ServiceEndpoint)|  
|[ダッシュボードまたはエンティティ フォーム (SystemForm)](dependency-tracking-solution-components.md#BKMK_SystemForm)|[プラグイン アセンブリ (PluginAssembly)](dependency-tracking-solution-components.md#BKMK_PluginAssembly)|[サイト マップ (SiteMap)](dependency-tracking-solution-components.md#BKMK_SiteMap)|  
|[電子メール テンプレート (EmailTemplate)](dependency-tracking-solution-components.md#BKMK_EmailTemplate)|[プロセス (Workflow)](dependency-tracking-solution-components.md#BKMK_Workflow)|[Web リソース (WebResource)](dependency-tracking-solution-components.md#BKMK_WebResource)|  
  
<a name="BKMK_RibbonCustomization"></a>   
### <a name="application-ribbons-ribboncustomization"></a>アプリケーション リボン (RibbonCustomization)  
 アプリケーション リボンとエンティティ リボンのテンプレートに対するリボンのユーザー設定です。 アプリケーション リボンには、エンティティ レベルまたはフォーム レベルのリボンの定義は含まれません。  
  
 カスタム アプリケーション リボンは、多くの場合 Web リソースへの公開済み依存関係があります。 Web リソースを使用してリボン ボタン アイコンおよび JavaScript 関数を定義することで、特定のリボン コントロールを使用する際にリボン要素を表示するタイミングや実行する操作を制御します。 依存関係は、リボン定義が `$webresource:` ディレクティブを使用して、Web リソースをリボンに関連付けるときにのみ作成されます。 詳細: [$webresource ディレクティブ](/dynamics365/customer-engagement/developer/web-resources#BKMK_WebResourceDirective)  
  
<a name="BKMK_KBArticleTemplate"></a>   
### <a name="article-template-kbarticletemplate"></a>記事テンプレート (KBArticleTemplate)  
 記事の標準属性を含むテンプレート。 記事テンプレートと KbArticle エンティティとの間には常に内部依存関係があります。  
  
<a name="BKMK_ConnectionRole"></a>   
### <a name="connection-role-connectionrole"></a>つながりロール (ConnectionRole)  
 2 つのレコード間の関係を記述しているロールです。 各つながりロールは、つながりロールを使用してリンクすることができるエンティティ レコードの種類を定義します。 これにより、つながりロールとエンティティ間の公開済み依存関係が作成されます。  
  
<a name="BKMK_ContractTemplate"></a>   
### <a name="contract-template-contracttemplate"></a>契約テンプレート (ContractTemplate)  
 契約の標準属性を含むテンプレート。 契約テンプレートと契約エンティティとの間には常に内部依存関係があります。  
  
<a name="BKMK_SystemForm"></a>   
### <a name="dashboard-or-entity-form-systemform"></a>ダッシュボードまたはエンティティ フォーム (SystemForm)  
 システム フォーム エンティティ レコードは、ダッシュボードおよびエンティティ フォームの定義に使用します。 SystemForm をエンティティ フォームとして使用する場合、エンティティとの内部依存関係が生じます。 SystemForm をダッシュボードとして使用する場合、内部依存関係は生じません。 エンティティ フォームとダッシュボードのいずれも、コンテンツに関連付けられた公開済み依存関係があります。 エンティティ フォームには、エンティティの関係に依存する検索フィールドがあります。 ダッシュボードとエンティティ フォームのいずれにも、グラフやサブグリッドを含めることができます。これにより、公開済み依存関係がビューに作成され、ビューはエンティティに対して内部依存関係を持つことになります。 ダッシュボードまたはフォームに表示されるコンテンツが原因で、またはフォームに JavaScript ライブラリが含まれている場合に、Web リソースへの公開済み依存関係が作成される可能性があります。 エンティティ フォームには、フォーム内のフィールドとして表示される属性への公開済み依存関係があります。  
  
<a name="BKMK_EmailTemplate"></a>   

### <a name="email-template-emailtemplate"></a>電子メール テンプレート (EmailTemplate)  
 電子メール メッセージの標準属性が設定されたテンプレートです。 通常、電子メール テンプレートには、指定されたエンティティ属性からのデータを挿入するフィールドが含まれます。 電子メール テンプレートは作成時に特定のエンティティにリンクできるため、エンティティへの内部依存関係が生じる場合があります。 グローバル電子メール テンプレートは特定のエンティティに関連付けられていませんが、データの取得に使用するエンティティ属性への、公開済み依存関係が生じる場合があります。 プロセス (ワークフロー) は、多くの場合に、ワークフローとの公開済み依存関係を作成する電子メール テンプレートを使用して電子メールを送信するように構成されます。  
  
<a name="BKMK_Entity"></a>   

### <a name="entity-entity"></a>エンティティ (Entity)  
 Common Data Service でデータをモデル化および管理する主構造です。 エンティティに関連付けられたグラフ、フォーム、エンティティ関係、ビュー、属性は、エンティティを削除したときに自動的に削除されます。これは両者に内部依存関係があるためです。 エンティティには、多くの場合、プロセス、ダッシュボード、および電子メール テンプレートとの公開済み依存関係があります。  
  
<a name="BKMK_FieldSecurityProfile"></a>   
### <a name="field-security-profile-fieldsecurityprofile"></a>フィールド セキュリティ プロファイル (FieldSecurityProfile)  
 セキュリティで保護されている属性のアクセス レベルを定義するプロファイルです。  
  
<a name="BKMK_MailMergeTemplate"></a>   
### <a name="mail-merge-template-mailmergetemplate"></a>差し込み印刷用テンプレート (MailMergeTemplate)  
 差し込み印刷文書の標準属性を備えたテンプレートです。 差し込み印刷用テンプレートには、関連付けられたエンティティへの公開済み依存関係があります。  
  
<a name="BKMK_OptionSet"></a>   
### <a name="option-set-optionset"></a>オプション セット (OptionSet)  
 オプション セットは一連のオプションを定義します。 候補リスト属性は、オプション セットを使用して提供するオプションを定義します。 複数の候補リスト属性にグローバル オプション セットを使用することで、常に同一のオプションを提供し、1 か所で管理することができます。 候補リスト属性がグローバル オプション セットを参照すると、公開済み依存関係が発生します。 候補リスト属性で使用されているグローバル オプション セットは削除できません。  
  
<a name="BKMK_PluginAssembly"></a>   
### <a name="plug-in-assembly-pluginassembly"></a>プラグイン アセンブリ (PluginAssembly)  
 プラグインの種類を 1 つ以上備えたアセンブリです。 プラグインは一般にエンティティに関連付けられているイベントに登録されます。 これにより、公開済み依存関係が作成されます。  
  
<a name="BKMK_Workflow"></a>   
### <a name="process-workflow"></a>プロセス (Workflow)  
 実行する特定のビジネス プロセス、タスク、または一連の操作の自動化に必要な手順を定義する論理ルールです。 プロセスは、プロセスによって参照される他のソリューション コンポーネントへの公開済み依存関係を作成するさまざまな操作を提供します。 各プロセスには、関連付けられているエンティティへの公開済み依存関係もあります。  
  
<a name="BKMK_Report"></a>   
### <a name="report-report"></a>レポート (Report)  
 データを要約して見やすく配置したものです。 レポートには、レポートに含まれるエンティティまたは属性データへの公開済み依存関係があります。 各レポートは、レポート関連カテゴリ (ReportCategory) と呼ばれるソリューション コンポーネントへの内部依存関係を作成するレポート カテゴリにも関連付けられている必要があります。 レポートを、親レポートとの公開済み依存関係を作成する、サブレポートとして構成することができます。  
  
<a name="BKMK_SDKMessageProcessingStep"></a>   
### <a name="sdk-message-processing-step-sdkmessageprocessingstep"></a>SDK メッセージ処理手順 (SDKMessageProcessingStep)  
 実行パイプラインの中でプラグインを実行する段階です。  
  
<a name="BKMK_Role"></a>   
### <a name="security-role-role"></a>セキュリティ ロール (Role)  
 セキュリティ特権をグループ化したものです。 Common Data Service システムへのアクセスが許可されるロールがユーザーに割り当てられます。 エンティティ フォームを特定のセキュリティ ロールに関連付けることで、フォームを表示できるユーザーを制御できます。 これにより、セキュリティ ロールとフォーム間の公開済み依存関係が作成されます。  
  
> [!NOTE]
>  組織の部署からのセキュリティ ロールのみを、ソリューションに追加できます。 これらのセキュリティ ロールへの読み取りアクセス権を持つユーザーのみが、それをソリューションに追加できます。  
  
<a name="BKMK_ServiceEndpoint"></a>   
### <a name="service-endpoint-serviceendpoint"></a>サービス エンドポイント (ServiceEndpoint)  
 連絡可能なサービス エンドポイントです。  
  
<a name="BKMK_SiteMap"></a>   
### <a name="site-map-sitemap"></a>サイト マップ (SiteMap)  
 アプリケーションのナビゲーション ウィンドウを制御するのに使用される XML データです。 サイト マップをリンクすることで、HTML Web リソースを表示したり、サイト マップ内のアイコンにイメージ Web リソースを使用したりすることができます。 `$webresource:` ディレクティブを使用してこれらの関連付けを設定すると、公開済み依存関係が作成されます。 詳細: [$webresource ディレクティブ](/dynamics365/customer-engagement/developer/web-resources#BKMK_WebResourceDirective)  
  
<a name="BKMK_WebResource"></a>   
### <a name="web-resource-webresource"></a>Web リソース (WebResource)  
 Web 開発で使用されるファイルに相当するデータです。 Web リソースはカスタム ユーザー インターフェイス要素の提供に使用されるクライアント側のコンポーネントを提供します。 Web リソースにはエンティティ フォーム、リボン、およびサイトマップとの公開済み依存関係が生じる場合があります。 `$webresource:` ディレクティブを使用してリボンまたはサイトマップに関連付けを設定すると、公開済み依存関係が作成されます。 詳細については、[$webresource ディレクティブ](/dynamics365/customer-engagement/developer/web-resources#BKMK_WebResourceDirective) を参照してください。  
  
> [!NOTE]
>  Web リソースが、相対リンクに基づいて他の Web リソースに依存することがあります。 たとえば、HTML Web リソースが CSS またはスクリプト Web リソースを使用する可能性があります。 エンティティ フォームやグラフ以外に表示される Silverlight Web リソースには、ホストする HTML Web リソースが必要です。 このような依存関係はソリューションの依存関係として追跡されません。  
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 ソリューションを使用した拡張機能のパッケージ化および配布](/dynamics365/customer-engagement/developer/package-distribute-extensions-use-solutions)   
 [ソリューションの概要](introduction-solutions.md)   
 [ソリューション開発の計画](/dynamics365/customer-engagement/developer/plan-solution-development)   
 [アンマネージド ソリューションの作成、エクスポート、またはインポート](create-export-import-unmanaged-solution.md)   
 [マネージド ソリューションの作成、インストール、および更新](create-install-update-managed-solution.md)   
 [マネージド ソリューションの作成、インストール、および更新](create-install-update-managed-solution.md)   
 [ソリューションのアンインストールまたは削除](uninstall-delete-solution.md)   
 [ソリューション エンティティ](/dynamics365/customer-engagement/developer/solution-entities)