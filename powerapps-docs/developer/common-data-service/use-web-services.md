---
title: Common Data Service for Apps Web サービスの使用 | Microsoft Docs
description: 開発者が Common Data Service for Apps Web サービスを利用する方法について説明します。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: faisalmo
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/26/2018
ms.author: jdaly
ms.openlocfilehash: 7f89a74b37ebf322137d680e165c007cd8fa6d26
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="use-common-data-service-for-apps-web-services"></a>Common Data Service for Apps Web サービスの使用

Common Data Service for Apps には、データの操作に使用できる 2 つの Web サービスがあります。 要件とスキルに最適なサービスを選んでください。 詳細情報: [Dynamics 365 Customer Engagement 開発者ドキュメント: Dynamics 365 Customer Engagement 用開発スタイルの選択](/dynamics365/customer-engagement/developer/choose-development-style)

## <a name="web-api"></a>Web API
Web API は OData v4 RESTful エンドポイントです。 OAuth 2.0 を使用した HTTP 要求と認証をサポートする任意のプログラミング言語に使用してください。

詳細情報: [Dynamics 365 Customer Engagement 開発者ドキュメント: Dynamics 365 Customer Engagement Web API を使用する](/dynamics365/customer-engagement/developer/use-microsoft-dynamics-365-web-api)

## <a name="organization-service"></a>組織のサービス

組織のサービスは、Common Data Service for Apps プラットフォームの中心となる部分です。 これは Windows Communication Foundation (WCF) サービスであり、現在は SOAP エンドポイントのみを公開しています。 .NET 開発者は SDK アセンブリを使用してデータ操作を実行できます。 プラグイン内では、組織のサービスは SDK アセンブリ経由でのみ使用できます。
> [!NOTE]
> 開発者は .NET SDK アセンブリを使用せずに組織のサービスの SOAP エンドポイントを使用できますが、Web API が持つ RESTful の特性を考慮すると、Web API の方がはるかに優れています。

詳細情報: [Dynamics 365 Customer Engagement 開発者ドキュメント: Dynamics 365 組織サービスを使用](/dynamics365/customer-engagement/developer/use-microsoft-dynamics-365-organization-service)

## <a name="about-the-web-services-and-the-platform"></a>Web サービスとプラットフォームの概要

組織のサービスは、プラットフォームを定義するものであると認識することが重要です。 Web API では RESTful プログラミング機能を利用できますが、すべてのデータ操作は、最終的に基となる組織のサービスを経由します。 

組織のサービスには、サポートする操作がメッセージとして定義されています。 各メッセージには名前があります。 SDK アセンブリ内の各メッセージには、対応する *&lt;メッセージ名&gt;*`Request` と *&lt;メッセージ名&gt;*`Response` クラスがあります。 `Microsoft.Xrm.Sdk.dll` の [IOrganizationService インターフェイス](/dotnet/api/microsoft.xrm.sdk.iorganizationservice)には、一般的な CRUD 操作のためのいくつかのヘルパー メソッドと、メッセージの呼び出しに使用できる [Execute メソッド](/dotnet/api/microsoft.xrm.sdk.iorganizationservice.execute)が定義されています。 すべてのメッセージは、基となる [OrganizationRequest クラス](/dotnet/api/microsoft.xrm.sdk.organizationrequest)を使用しています。

Web API では、組織のサービスと同じ操作を使用できますが、OData v4 プロトコルを使用して RESTful スタイルで提示します。 OData v4 は、*関数*または*アクション*を介して名前付き操作を提供します。 組織のサービスで利用できるほぼすべてのメッセージは、対応する名前付き関数またはアクションとして公開されています。 CRUD 操作に対応するメッセージは Web API で使用できません。これは、RESTful サービスとして GET、POST、PATCH、および DELETE HTTP メソッドを使用する実装があるためです。

組織のサービスの SOAP エンドポイント用 .NET SDK アセンブリは、[IOrganizationService インターフェイス](/dotnet/api/microsoft.xrm.sdk.iorganizationservice)に基づき、基となるプラットフォーム サービスを詳細にモデル化するように設計されています。 ただし、これらは同じコンポーネントではないので混同しないでください。 

組織のサービスの SOAP エンドポイントは 2011 で導入されましたが、Microsoft は非推奨になることを発表しました。 つまり、SOAP エンドポイントは削除されるまで引き続き機能し、サポートされます。 また、SOAP エンドポイントが削除された後も、Microsoft は .NET SDK アセンブリが引き続き機能するように更新することを発表しました。 つまり、SOAP エンドポイントが削除されるまでは、更新された SDK アセンブリを入手できます。開発者は、これらの新しいアセンブリを使用するために、今後どこかの時点でコードを更新する必要があります。

## <a name="discovery-services"></a>探索サービス

各 Common Data Service for Apps ユーザーは、複数の Common Data Service for Apps インスタンスにアクセスできます。 探索サービスでは、使用する Microsoft アカウントに基づいて、ユーザーが接続できるインスタンスの一覧をユーザーに表示するコードを記述できます。 各インスタンスには、選択したインスタンスに接続するために使用できる URL が含まれています。 

探索サービスには、Web API または組織のサービスのいずれかを介してアクセスします。

- Web API の詳細情報: [Dynamics 365 Customer Engagement 開発者ドキュメント: Web API を使用して組織の URL を検出します](/dynamics365/customer-engagement/developer/webapi/discover-url-organization-web-api)
- 組織のサービスの詳細情報: [Dynamics 365 Customer Engagement 開発者ドキュメント: 探索サービスを使用して組織の URL を検出する](/dynamics365/customer-engagement/developer/org-service/discover-url-organization-organization-service)

## <a name="use-custom-actions"></a>カスタム アクションの使用

プロセスで使用できる宣言型オプションの 1 つは、*カスタム アクション*を作成することです。 カスタム アクションは、基本的に組織のサービスに新しいメッセージを作成することです。 カスタム アクションを使用すると、一連の操作を組み合わせて名前付きの再利用可能な 1 つの操作にすることができます。 たとえば、重要な顧客に重大な問題が発生したときに、適切な人に通知するための標準的な一連の操作を組み合わせた *new_Escalate* という新しいメッセージを作成できます。

カスタム アクションを定義する場合、入力パラメーターと、返される結果に含めるプロパティを定義することで、操作のシグネチャを選択します。 カスタム アクションは、デザイナーまたはコードを使用して宣言型プロセスから呼び出すことができます。 

カスタム アクション独自の価値は、開発者ではない個人がデザイナーを使用して、他のプロセスやプロセスを呼び出すコードに影響を与えることなく、カスタム アクションに含まれている特定の操作を変更できることです。  この点は、アクションのシグネチャが変わらない場合にも当てはまります。 異なる入力パラメーターまたは出力プロパティが必要な場合は、既存のアクションを使用してプロセスやコードを壊さないように、新しいカスタム アクションを作成する必要があります。

環境内にカスタム アクションが定義されている場合、Web API を使用して新しい OData v4 アクションを使用できます。また、組織のサービス内では、[OrganizationRequest クラス](/dotnet/api/microsoft.xrm.sdk.organizationrequest)を直接使用するか、*コード生成ツール (CrmSvcUtil.exe)* を使用して生成され、厳密に型指定されたクラスを使用して、カスタム アクションを呼び出すことができます。

詳細情報: 
- [Dynamics 365 Customer Engagement カスタマイズ ガイド: 操作の概要](/dynamics365/customer-engagement/customize/actions)
- [Dynamics 365 Customer Engagement 開発者ドキュメント: 独自のアクションの作成](/dynamics365/customer-engagement/developer/create-own-actions)
- [Dynamics 365 Customer Engagement 開発者ドキュメント: Web API アクションの使用 > カスタム アクションの使用](/dynamics365/customer-engagement/developer/webapi/use-web-api-actions#use-a-custom-action)

## <a name="metadata-services"></a>メタデータ サービス

Web API と組織のサービスのいずれにも、エンティティ スキーマ上で CRUD 操作を実行する機能が含まれています。 これらの操作はコードを使用して実行できますが、通常はデザイナーを使用してカスタム スキーマ要素の追加、更新、または削除を行います。 スキーマの変更を適用するにはユーザーに管理者特権が必要ですが、メタデータの読み取りはすべてのユーザーが実行できます。

メタデータ サービスのより一般的な使用方法は、拡張機能が実行されている環境に関するメタデータを取得することです。 すべての環境は異なる可能性があり、スキーマのメタデータには環境の構成方法に関する多くの情報が含まれているため、拡張機能がその環境で採用されている他のカスタマイズに適応できるように、この情報を取得する必要があります。

次に例をいくつか示します。
- optionset 属性で使用できるオプションの数は変わる可能性があります。 環境内の値をハードコーディングするのではなく、異なるオプションが存在するかどうかを検討してください。 現在の環境に異なるオプションがあるかどうかは、システムに対してクエリを実行して判断できます。
- エンティティの表示名は変わる可能性があります。 アカウント エンティティの既定の表示名は *Account* です。 この名前は *Company* に変更される可能性があります。 ユーザーにメッセージを表示してエンティティの名前を参照する場合は、この値をハードコーディングせず、ユーザーが見慣れているものと一致する値を使用し、エンティティのメタデータから取得した表示名を使用することをお勧めします。

システムのメタデータについて理解を深めると、Common Data Service for Apps プラットフォームの仕組みを理解するために役立ちます。 メタデータを編集できるデザイナーでは、メタデータ内のすべての詳細情報を表示することはできません。 *メタデータ ブラウザー*と呼ばれるモデル駆動型アプリをインストールすると、システム内にあるすべての非表示エンティティとメタデータ プロパティを表示できます。 

詳細情報: [Dynamics 365 Customer Engagement 開発者ドキュメント: 組織のメタデータの参照](/dynamics365/customer-engagement/developer/browse-your-metadata)

プログラムでメタデータを操作する方法の詳細については、以下を参照してください。
- [Dynamics 365 Customer Engagement 開発者ドキュメント: Web API をメタデータで使用する](/dynamics365/customer-engagement/developer/webapi/use-web-api-metadata)
- [Dynamics 365 Customer Engagement 開発者ドキュメント: Dynamics 365 メタデータと共に組織サービスを使用する](/dynamics365/customer-engagement/developer/org-service/use-organization-service-metadata)
 
### <a name="see-also"></a>関連項目

[Common Data Service for Apps Developer の概要](overview.md)

