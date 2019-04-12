---
title: エンティティのライセンス要件 | Microsoft Docs
description: Common Data Service 内のエンティティのライセンス要件の詳細。
author: lancedMicrosoft
manager: kfile
ms.service: powerapps
ms.component: cds
ms.topic: conceptual
ms.date: 05/01/2018
ms.author: lanced
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="license-requirements-for-entities"></a>エンティティのライセンス要件
アプリ作成者は Common Data Service 内で使用可能なエンティティのほとんどを使用し (カスタム エンティティと、Common Data Service の部分であるエンティティ)、PowerApps Plan 1 または Microsoft Flow Plan 1 を持つユーザーのアプリとフローを作成できます。 場合によっては、エンティティは、複雑なビジネス ロジックが含まれるか、アプリ ユーザーに特定のライセンスを求める Dynamics 365 アプリケーションに連結されます。 


|エンティティ    |説明    |要件    |
|---------|---------|---------|
|複雑なビジネス ロジックを持つエンティティ   | これらは、複雑なサーバー側ビジネス ロジックを使用するエンティティです。 たとえば、リアルタイムのワークフローまたはプラグイン コードを使用するエンティティ。       |  [PowerApps Plan 2](https://powerapps.microsoft.com/pricing/) または [Flow Plan 2](https://flow.microsoft.com/pricing/)        |
|制限付きエンティティ  |  これらは Common Data Service の標準ではなく、Dynamics 365 Customer Engagement アプリケーションまたはサード パーティ ソリューションに含まれているエンティティです。 たとえば、サポート情報記事、目標、権利エンティティなどです。     |  [Dynamics 365 プラン](https://dynamics.microsoft.com/pricing/)      | 


> [!NOTE]
> これらのエンティティを使うアプリとフローでは、アプリやフローの作成者や開発者ではなくアプリやフローのユーザーが適切なライセンスを持っている必要があります。

## <a name="entities-with-complex-business-logic"></a>複雑なビジネス ロジックを持つエンティティ
次の複数のサーバー側ロジックを含むエンティティは、これらのエンティティを使用するアプリまたはフローのユーザーに、PowerApps Plan 2 または Microsoft Flow Plan 2 ライセンスを要求します。

* コード プラグイン (詳細については「[プラグイン開発](https://docs.microsoft.com/dynamics365/customer-engagement/developer/plugin-development)」を参照)
* リアルタイム ワークフロー (詳細については「[ワークフロー プロセス](https://docs.microsoft.com/dynamics365/customer-engagement/customize/workflow-processes)」を参照)

    > [!NOTE]
    >  リアルタイムのワークフローに変換されるワークフローのみ、リアルタイムおよび同期と見なされます。 バックグラウンドで実行されるワークフローは、適切な PowerApps プラン計画でも使用でき、追加ライセンスは必要ありません。

エンティティに複雑なビジネス ロジックを追加するかどうかを調べるには、環境で設定されたプラグイン アセンブリおよびワークフローの一覧を確認します。 Dynamics 365 アプリケーションのインストール後にサーバー側ロジックが含まれる可能性があるエンティティの一覧については、「[PowerApps Plan 2 ライセンスが必要な複雑なエンティティ](data-platform-complex-entities.md)」を参照してください。  

### <a name="impacting-license-requirements-when-adding-complex-business-logic"></a>複雑なビジネス ロジックを追加するときに影響を与えるライセンスの要件
アプリ作成者は Common Data Service 内のエンティティにプラグイン コードとリアルタイム ワークフローを追加できますが、そうすると、既に展開されたアプリのユーザーに対するライセンス要件が変わる可能性があります。 アプリ作成者は、複雑なビジネス ロジックをエンティティに追加するときに注意してください。まず、エンティティを使用するアプリと、これらのアプリのユーザーが適切なライセンスを持っているかを確認する必要があります。

## <a name="restricted-entities"></a>制限付きエンティティ
Dynamics 365 アプリケーション機能に関連付けられた特定のエンティティを使用するには、エンティティ内のレコードを作成、更新、または削除する場合は、アプリ ユーザーがそのアプリケーションに対応するライセンスを持っている必要があります。 制限付きエンティティの全一覧については、「[Dynamics 365 のライセンスを必要とする制限付きエンティティ](data-platform-restricted-entities.md)」を参照してください。

## <a name="licensing-examples"></a>ライセンスの例
Barb と Isaac は Common Data Service を使用して PowerApps でアプリを作成してデータを保存します。

Barb は、2 つのキャンバス アプリを作成します。

* アプリ 1 &ndash; 関連情報が格納されるユーザー定義エンティティとともに予定エンティティを使用します。
* アプリ 2 &ndash; 制限付きエンティティであるサポート案件エンティティとともに予定エンティティを使用します。

Isaac は、2 つのモデル駆動型アプリを作成します。

* アプリ 3 &ndash; 関連情報が格納されるユーザー定義エンティティとともに予定エンティティを使用します。
* アプリ 4 &ndash; 制限付きエンティティであるサポート案件エンティティとともに予定エンティティを使用します。

Barb と Isaac には、以下のライセンスが必要です。
* Barb が Common Data Service を使用してキャンバス アプリを作成するには PowerApps Plan 1 ライセンスが必要です。 データベースを作成するか、カスタム エンティティを作成する必要がある場合、PowerApps Plan 2 ライセンスが必要です。

* Isaac がモデル駆動型アプリを構築するには PowerApps Plan 2 ライセンスが必要です。

アプリ ユーザーには、以下のライセンスが必要です。
* アプリ 1 ユーザーに必要なのは、PowerApps Plan 1 または Plan 2 ライセンスのみです。このアプリには複雑なビジネス ロジックまたは制限付きエンティティを持つエンティティが含まれていないためです。

* アプリ 2 ユーザーには、Dynamics 365 for Customer Service Enterprise Edition ライセンス (または Dynamics 365 や Dynamics 365 Customer Engagement プラン) が必要です。このアプリには制限付きエンティティが含まれているためです。

* アプリ 3 ユーザーには、PowerApps Plan 2 ライセンスが必要です。モデル駆動型アプリであるためです。

* アプリ 4 ユーザーには、Dynamics 365 for Customer Service Enterprise Edition ライセンス (または Dynamics 365 や Dynamics 365 Customer Engagement プラン) が必要です。このアプリには制限付きエンティティが含まれているためです。

    Dynamics 365 for Customer Service プランには、ユーザーがモデル駆動型アプリを実行できようにする PowerApps Plan 2 ライセンスが含まれています。

ここで、Isaac と Barb の両方がアプリで使用しているユーザー定義エンティティにリアルタイム ワークフローを追加するとどうなるかを見てみましょう。

Barb と Isaac には、以下のライセンスが必要です。
* Barb が Common Data Service を使用してキャンバス アプリを作成するにも PowerApps Plan 1 ライセンスが必要です。

* Isaac がモデル駆動型アプリを構築するにも PowerApps Plan 2 ライセンスが必要です。

アプリ ユーザーには、以下のライセンスが必要です。
* アプリ 1 ユーザーには、PowerApps Plan 2 ライセンスが必要になります。このアプリケーションにはリアルタイム ワークフローを持つエンティティが含まれているためです。

* アプリ 2 ユーザーには、引き続き Dynamics 365 for Customer Service Enterprise Edition ライセンス (または Dynamics 365 や Dynamics 365 Customer Engagement プラン) が必要です。このアプリには制限付きエンティティが含まれているためです。 

* アプリ 3 ユーザーには、引き続き PowerApps Plan 2 ライセンスが必要です。モデル駆動型アプリであるためです。

* アプリ 4 ユーザーには、引き続き Dynamics 365 for Customer Service Enterprise Edition ライセンス (または Dynamics 365 や Dynamics 365 Customer Engagement プラン) が必要です。このアプリには制限付きエンティティが含まれているためです。

    Dynamics 365 for Customer Service プランには、ユーザーがモデル駆動型アプリを実行できようにする PowerApps Plan 2 ライセンスが含まれています。

この変更によって影響を受ける唯一のアプリは、アプリ 1 です。PowerApps Plan 1 ライセンスが必要でしたが、PowerApps Plan 2 ライセンスが必要になりました。複雑なビジネス ロジックを持つエンティティが含まれているためです。 

## <a name="more-about-licensing"></a>ライセンスの詳細
PowerApps と Dynamics 365 ライセンスの詳細については、「[ライセンスの概要](../../administrator/pricing-billing-skus.md)」をご覧ください。
