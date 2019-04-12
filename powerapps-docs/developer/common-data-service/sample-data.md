---
title: サンプル データの追加と削除 (Common Data Service) | Microsoft Docs
description: Web API または組織サービスを使用して、サンプル データをインストールまたはアンインストールする方法
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="add-and-remove-sample-data"></a>サンプル データの追加と削除

メッセージ `InstallSampleData` および `UninstallSampleData` を使用して、組織用のサンプル データをプログラム経由でインストールおよびアンインストールできます。 

|Web API アクション |組織サービス クラス|
|--|--|
|<xref href="Microsoft.Dynamics.CRM.InstallSampleData?text=InstallSampleData Action" /> |<xref:Microsoft.Crm.Sdk.Messages.InstallSampleDataRequest>|
|<xref href="Microsoft.Dynamics.CRM.UninstallSampleData?text=UninstallSampleData Action" />|<xref:Microsoft.Crm.Sdk.Messages.UninstallSampleDataRequest>|

## <a name="using-the-web-api"></a>Web API の使用

<xref href="Microsoft.Dynamics.CRM.InstallSampleData?text=InstallSampleData Action" /> を使用してサンプル データをインストールします。

### <a name="request"></a>要求

```http
POST [Organization URI]/api/data/v9.0/InstallSampleData HTTP/1.1
Accept: application/json
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
```
### <a name="response"></a>応答

```http
HTTP/1.1 204 No Content
OData-Version: 4.0
```

<xref href="Microsoft.Dynamics.CRM.UninstallSampleData?text=UninstallSampleData Action" /> を使用してサンプル データをアンインストールします。

### <a name="request"></a>要求

```http
POST [Organization URI]/api/data/v9.0/UninstallSampleData HTTP/1.1
Accept: application/json
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
```
### <a name="response"></a>応答

```http
HTTP/1.1 204 No Content
OData-Version: 4.0
```

## <a name="using-the-organization-service"></a>組織サービスの使用

<xref:Microsoft.Crm.Sdk.Messages.InstallSampleDataRequest> を使用してサンプル データをインストールします

```csharp
var request = new InstallSampleDataRequest();
service.Execute(request);
```

<xref:Microsoft.Crm.Sdk.Messages.UninstallSampleDataRequest> を使用してサンプル データをアンインストールします

```csharp
var request = new UninstallSampleDataRequest();
service.Execute(request);
```

> [!NOTE]
> これらの操作により返される <xref:Microsoft.Crm.Sdk.Messages.InstallSampleDataResponse> クラスまたは <xref:Microsoft.Crm.Sdk.Messages.UninstallSampleDataResponse> クラスのどちらにも調べるべきプロパティは含まれていません。

### <a name="see-also"></a>関連項目

[データのインポート](import-data.md)