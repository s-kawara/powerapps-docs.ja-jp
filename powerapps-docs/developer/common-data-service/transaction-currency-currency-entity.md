---
title: トランザクション通貨 (通貨) エンティティ (Common Data Service for Apps) | Microsoft Docs
description: ユーザーが複数の通貨で金融取引を実行できるようにする、複数通貨機能である取引通貨について。 基本通貨を使用すると、さまざまな取引通貨の複数レコードを 1 つの通貨で集計、比較、または分析できます。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: mayadumesh
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="transaction-currency-currency-entity"></a>トランザクション通貨 (通貨) エンティティ

Common Data Service for Apps は、複数通貨システムを使用して、各レコードを独自の通貨に関連付けることができます。 この通貨を、*取引*通貨と呼びます。 複数通貨機能を使用すると、営業案件、見積もり、受注、請求書などの財務取引を複数の通貨で実行できます。 また、この機能を使用することにより、エンド ユーザーは財務取引に使用する通貨を選択できます。  
  
 為替レートを使用すると、さまざまな取引通貨の複数レコードを 1 つの通貨で集計、比較、または分析できます。 これを、*基本通貨*と呼びます。 まず、組織の基本通貨を定義した後、為替レートを定義することによって、基本通貨と取引通貨とを関連付けます。 基本通貨は、他の通貨の基準となる通貨です。 為替レートは取引通貨の値で、1 つの基本通貨と等しくなっています。  
  
 取引通貨のプロパティを使用すると、次のことを実行できます。  
  
- 営業案件、見積もり、受注、および請求書の定義や処理に使用する通貨を選択する。  
  
- 基本通貨を基準とした通貨為替レートを定義する。  
  
- 取引通貨を定義したり、基本通貨と取引通貨を関連付けるための為替レートを定義する。  
  
- すべての財務取引の取引額を、基本通貨および取引通貨で取得する。  
  
- 通貨ごとの製品価格表を定義する。  
  
複数の通貨を使用するには、組織で使用する基本通貨を、サーバーのインストール中や組織のセットアップ中に定義しておく必要があります。 組織に基本通貨が設定された後で、変更することはできません。 この値は `Organization.BaseCurrencyID` 属性に格納されます。  
  
取引通貨は、システム設定の一部として定義されます。 取引通貨の定義数に制限はありません。 取引通貨は、通貨為替レートの定義によって基本通貨に関連付けられます。  
  
基本通貨と取引通貨を定義したら、通貨に対応する価格表を定義する必要があります。 1 つの組織に複数の価格表を関連付けることができます。これらは、地理上の対象マーケットごとに現地通貨で定義されるのが一般的です。  
  
財務取引に関係するすべてのエンティティは、取引通貨をサポートしています。 通常、通貨は取引先企業や営業案件などから継承されますが、必要に応じて変更できます。  
  
取引通貨には、`TransactionCurrency.CurrencyPrecision` 属性を使用して精度を指定できます。 金額の属性の種類に精度の基準を指定するには、<xref:Microsoft.Xrm.Sdk.Metadata.MoneyAttributeMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.MoneyAttributeMetadata.PrecisionSource>  属性を使用します。  
  
同一の取引通貨がレコード内のすべての金額プロパティで共有されます。たとえば、`Account.CreditLimit` 属性では、 Common Data Service for Apps では、エンティティ内の金額属性ごとに、システムにより計算された読み取り専用の金額属性が自動的に作成されます。これを "基準" と呼びます。 これは、対応する属性の値が対応する基本通貨で格納される金額属性です。例として `Account.CreditLimit_Base` 属性で説明します。  
  
次の計算式を使用して基準値を計算します。  
  
```csharp  
creditlimit_base = creditlimit / exchangerate  
```  
  
次に、取引通貨を定義できるエンティティの一覧を示します。  
  
-   Account  
  
-   AnnualFiscalCalendar  
  
-   キャンペーン   
  
-   CampaignActivity  
  
-   競合企業  
  
-   取引先担当者   
  
-   契約   
  
-   ContractDetail  
  
-   割引  
  
-   DiscountType  
  
-   FixedMonthlyFiscalCalendar  
  
-   請求書   
  
-   InvoiceDetail  
  
-   リード​​  
  
-   一覧取得  
  
-   MonthlyFiscalCalendar  
  
-   営業案件​​  
  
-   OpportunityClose  
  
-   OpportunityProduct  
  
-   PriceLevel  
  
-   製品   
  
-   ProductPriceLevel  
  
-   QuarterlyFiscalCalendar  
  
-   見積もり   
  
-   QuoteDetail  
  
-   受注  
  
-   SalesOrderDetail  
  
-   SemiAnnualFiscalCalendar  
  
-   usersettings  
  
### <a name="see-also"></a>関連項目  
 [TransactionCurrency エンティティ](reference/entities/transactioncurrency.md)   
 [サンプル: 通貨為替レートの取得](org-service/samples/retrieve-currency-exchange-rate.md)   
 [事業部管理エンティティ](/dynamics365/customer-engagement/developer/business-management-entities)