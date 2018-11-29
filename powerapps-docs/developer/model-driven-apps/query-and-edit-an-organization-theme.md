---
title: 組織のテーマのクエリと編集 (モデル駆動型アプリ) | Microsoft Docs
description: 組織の視覚的なテーマの定義と適用について説明します。 これは、アプリケーションに組織のロゴと色の選択を適用する、サポートされている方法を提供します。
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
# <a name="query-and-edit-an-organization-theme"></a>組織のテーマのクエリと編集

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/query-and-edit-an-organization-theme -->

組織に対して視覚的なテーマを定義して適用できます。 これは、アプリケーションに組織のロゴと色の選択を適用する、サポートされている方法を提供します。 カスタマイズされていないモデル駆動型アプリ システムで提供される既定の色と視覚要素を変更して、自分のアプリケーションに合わせて、ユーザー定義のテーマを作成できます。 たとえば、個人用の製品ブランドの作成、会社ロゴの追加、エンティティ固有の色の指定を行うことができます。 テーマ色は、一部の従来の領域を除く、アプリケーション全体にグローバルに適用されます。  
  
<!-- [!NOTE]
> [!INCLUDE[cc_feature_included_with_2015_update_1_admins](../../includes/cc-feature-included-with-2015-update-1-admins.md)]  -->
  
 テーマのカスタマイズは、このリリースでは、Web アプリケーションに対してのみサポートされます。 組織のテーマに対する変更は、組織からエクスポートされるソリューションには含まれません。 複数のテーマを定義できますが、既定のテーマとして設定して公開できるのは 1 つだけです。  
  
 ビデオ: [テーマに合わせての構成](http://go.microsoft.com/fwlink/p/?LinkId=529568)  
  
<a name="BKMK_QueryTheme"></a>

## <a name="query-the-current-theme"></a>現在のテーマのクエリ
 組織に対するテーマの選択に適用する HTML Web リソースを使用したソリューションがある場合、クライアント側のコードを使用して現在のテーマをクエリすることが必要な場合があります。 次のクエリを Web API で使用して、その情報を取得できます。  

 **要求:** 

```http
GET [Organization URI]/api/data/v9.0/themes?$filter=isdefaulttheme eq true&$select=defaultentitycolor,defaultcustomentitycolor,controlborder,controlshade,selectedlinkeffect,globallinkcolor,processcontrolcolor,headercolor,logotooltip,hoverlinkeffect,navbarshelfcolor,navbarbackgroundcolor
```

 **応答:**

```json
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0

{  
    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#themes(defaultentitycolor,defaultcustomentitycolor,controlborder,controlshade,selectedlinkeffect,globallinkcolor,processcontrolcolor,headercolor,logotooltip,hoverlinkeffect,navbarshelfcolor,navbarbackgroundcolor)",  
    "value": [  
        {  
            "defaultentitycolor": "#001CA5",  
            "defaultcustomentitycolor": "#006551",  
            "controlborder": "#CCCCCC",  
            "controlshade": "#F3F1F1",  
            "selectedlinkeffect": "#B1D6F0",  
            "globallinkcolor": "#1160B7",  
            "processcontrolcolor": "#D24726",  
            "headercolor": "#1160B7",  
            "logotooltip": "Model-driven apps",  
            "hoverlinkeffect": "#D7EBF9",  
            "navbarshelfcolor": "#DFE2E8",  
            "navbarbackgroundcolor": "#002050",  
            "themeid": "f499443d-2082-4938-8842-e7ee62de9a23"  
        }  
    ]  
}  
```

 詳細: [Web API を使用するクエリ データ](../common-data-service/webapi/query-data-web-api.md)
  
<a name="BKMK_EditAndPublish"></a>

## <a name="edit-and-publish-theme-data"></a>テーマ情報の編集と公開

 テーマの作成には、UI のカスタマイズ ツールを使用します。開発者はコードを記述する必要はありません。 これらのカスタマイズの適用方法の詳細については、「[TechNet: 組織のブランドに合わせて配色を変更またはロゴを追加する](/dynamics365/customer-engagement/customize/change-color-scheme-add-logo-match-organizations-brand)」を参照してください。  

 ほとんどのテーマ データは、テーマ エンティティに格納されます。 特定のエンティティ用にカスタマイズされた色が、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.EntityColor> に含まれています にバインドされます。 このデータは、エンティティがソリューションに含まれている場合は、エンティティといっしょにエクスポートされます。

 次の表は、テーマに対して有効であり、テーマによって適用されるデータを格納している `Theme` エンティティ属性について説明しています。  

|スキーマ名|種類​​|既定のテーマの値|内容|  
|-----------------|----------|----------------------------|-----------------| 
|AccentColor|String|#E83D0F|プロセス コントロールで使用される統一インターフェイスのセカンダリ テーマの色。| 
|BackgroundColor|String|#FFFFFF|内部のみで使用。|
|ControlBorder|String|#BDC3C7|コントロールで境界線に使用される色。|  
|ControlShade|String|#FFFFFF|アイテムにカーソルを置いたときに、それを示すために使用するコントロールの色。|  
|DefaultCustomEntityColor|String|#00CCA3|色が割り当てられていない場合の、ユーザー定義エンティティの既定の色。|  
|DefaultEntityColor|String|#666666|色が割り当てられていない場合の、システム エンティティの既定の色。|  
|GlobalLinkColor|String|#1160B7|電子メール アドレスや検索などのリンクの色。|  
|HeaderColor|String|#1160B7|フォーム タブのラベルなど、ヘッダー テキストの色。|  
|HoverLinkEffect|String|#E7EFF7|アイテムにカーソルを置いたときにコマンドまたはリストで使用される色。|  
|ImportSequenceNumber|Integer|null|このレコードを作成したインポートのシーケンス番号です。|
|IsDefaultTheme|Boolean|正|カスタム テーマの既定値は false です。|
|LogoId|String|null|ループとして使用される Web リソースの名前。 推奨のサイズは、高さ 50 ピクセル、最大幅 400 ピクセルです。|  
|LogoToolTip|String|モデル駆動型アプリ|ロゴのツールヒントと alt テキストとして使用されるテキスト。| 
|MainColor|String|#3B79B7|メイン コマンド バー、ボタン、タブで使用される統一インターフェイスのプライマリ テーマの色。| 
|Name|String|MDA 既定のテーマ|テーマ エンティティの名前。|  
|NavBarBackgroundColor|String|#002050|プライマリ ナビゲーション バーの色。|  
|NavBarShelfColor|String|#DFE2E8|セカンダリ ナビゲーション バーの色。|  
|OverriddenCreatedOn|日時|null|レコードが移行された日時です。|  
|PageHeaderBackgroundColor|String|#E0E0E0|ページ ヘッダーの背景色。|  
|PanelHeaderBackgroundColor|String|#F3F3F3|パネル ヘッダーの背景色。|  
|ProcessControlColor|String|#41A053|プロセス コントロールのプライマリ カラーの選択。|  
|SelectedLinkEffect|String|#F8FAFC|コマンドまたはリストで選択されたアイテムを示すために使用される色。| 
|TransactionCurrencyId|検索|null|テーマに関連付けられている通貨の、基本通貨に対する為替レートです。| 
 
 変更を適用した後、<xref href="Microsoft.Dynamics.CRM.PublishTheme?text=PublishTheme Action" /> または <xref:Microsoft.Crm.Sdk.Messages.PublishThemeRequest> クラスを使用して、テーマ レコードの 1 つを現在のテーマにします。  

<a name="BKMK_ExportingAndImportingThemes"></a>

## <a name="exporting-and-importing-themes"></a>テーマのエクスポートとインポート

 テーマはソリューションの一部として含まれないので、組織間でテーマを転送するには、Configuration Migration ツールを使用して、テーマを生成し、テーマ データをエクスポートし、それを別の組織にインポートできます。 このツールの使用方法の詳細については、「[Configuration Migration ツールを使用して構成データを移動](/dynamics365/customer-engagement/admin/manage-configuration-data)」を参照してください。  

### <a name="see-also"></a>関連項目

 [テーマ エンティティ](../common-data-service/reference/entities/theme.md) <br/>
 [テーマの作成](/dynamics365/customer-engagement/customize/change-color-scheme-add-logo-match-organizations-brand) <br/>
 [開発者用カスタマイズ ガイド](/dynamics365/customer-engagement/developer/customize-dev/customize-applications)
