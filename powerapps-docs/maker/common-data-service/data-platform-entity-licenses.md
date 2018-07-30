---
title: エンティティのライセンス要件 | Microsoft Docs
description: Common Data Service (CDS) for Apps 内のエンティティのライセンス要件の説明です。
author: clwesene
manager: kfile
ms.service: powerapps
ms.component: cds
ms.topic: conceptual
ms.date: 07/25/2018
ms.author: clwesene
ms.openlocfilehash: 758d5b5ff2c552a4c4ccbf210062f35d4e53209c
ms.sourcegitcommit: efea7ed5ad8e80c87ba423fb094fa94b4e864d75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2018
ms.locfileid: "39265512"
---
# <a name="license-requirements-for-entities"></a>エンティティのライセンス要件
アプリの作成者は、Common Data Service (CDS) for Apps 内で利用可能なほとんどのエンティティ (Common Data Model の一部であるエンティティやカスタム エンティティを含む) を使用して、PowerApps プラン 1 または Microsoft Flow プラン 1 のライセンスを所有するユーザーのアプリやフローを作成することができます。 場合によっては、エンティティに複雑なビジネス ロジックが含まれていたり、エンティティがアプリ ユーザーに特定のライセンスを求める Dynamics 365 アプリケーションに関連付けられていたりすることがあります。 


|組織  |説明  |要件  |
|---------|---------|---------|
|複雑なビジネス ロジックを含むエンティティ  | 複雑なサーバー側のビジネス ロジックを使用するエンティティです。 たとえば、リアルタイム ワークフローまたはコード プラグインを使用するエンティティです。     | [PowerApps プラン 2](https://powerapps.microsoft.com/pricing/) または [Flow プラン 2](https://flow.microsoft.com/pricing/)  | 
|制限付きエンティティ    | これらは Common Data Service for Apps では標準ではないエンティティですが、Dynamics 365 Customer Engagement アプリケーションやサードパーティのソリューションに含まれます。 たとえば、ナレッジ記事、目標、権利のエンティティです。    | [Dynamics 365 プラン](https://dynamics.microsoft.com/pricing/)    |


> [!NOTE]
> これらのエンティティを使用するアプリとフローでは、アプリまたはフローの作成者や開発者ではなく、アプリとフローのユーザーに適切なライセンスを与える必要があります。

## <a name="entities-with-complex-business-logic"></a>複雑なビジネス ロジックを含むエンティティ
次の複雑なサーバー側ロジックを含むエンティティでは、これらのエンティティを使用するアプリまたはフローのユーザーに PowerApps プラン 2 または Microsoft Flow プラン 2 のライセンスが求められます。

* コード プラグイン (詳細については、「[プラグインの開発](https://docs.microsoft.com/dynamics365/customer-engagement/developer/plugin-development)」を参照)
* リアルタイム ワークフロー (詳細については、[ワークフロー プロセス](https://docs.microsoft.com/dynamics365/customer-engagement/customize/workflow-processes)に関するページを参照)。

    > [!NOTE]
    >  リアルタイム ワークフローに変換されるワークフローのみが、リアルタイムかつ同期と見なされます。 バックグラウンドで実行されるワークフローは、適切な PowerApps プランで引き続き使用でき、追加のライセンスは必要ありません。

エンティティに複雑なビジネス ロジックを追加したかどうかを知るには、ご利用の環境で構成されているプラグイン アセンブリとワークフローのリストを確認します。 Dynamics 365 アプリケーションをインストールした後、サーバー側のロジックを含めることができるエンティティの一覧については、[PowerApps プラン 2 ライセンスを必要とする複雑なエンティティ](data-platform-complex-entities.md)に関するページを参照してください。 

### <a name="impacting-license-requirements-when-adding-complex-business-logic"></a>複雑なビジネス ロジックを追加する場合のライセンス要求への影響
アプリの作成者はコード プラグインとリアルタイム ワークフローを CDS for Apps 内のエンティティに追加できますが、それにより、既に展開されているアプリのユーザーのライセンス要件が変わる可能性があります。 アプリの作成者はエンティティに複雑なビジネス ロジックを追加する際に注意する必要があります。まず、エンティティを使用するアプリと、そのアプリのユーザーが適切なライセンスを持っているかどうかを確認する必要があります。

## <a name="restricted-entities"></a>制限付きエンティティ
Dynamics 365 アプリケーションの機能に関連付けられている特定のエンティティでは、アプリ ユーザーがエンティティ内のレコードを作成、更新、削除する場合に、そのアプリケーションに対応するライセンスが求められます。 制限付きエンティティの一覧については、「[Restricted entities requiring Dynamics 365 licenses](data-platform-restricted-entities.md)」(Dynamics 365 ライセンスを必要とする制限付きのエンティティ) を参照してください。

## <a name="licensing-examples"></a>ライセンスの例
Barb と Isaac はデータを格納するために CDS for Apps を使用して、PowerApps でアプリを作成しています。

Barb は次の 2 つのキャンバス アプリを作成しています。

* アプリ 1 &ndash; 関連情報を格納するカスタム エンティティと共に Contact エンティティを使用します。
* アプリ 2 &ndash; 制限付きエンティティである Incident エンティティと共に Contact エンティティを使用します。

Isaac は次の 2 つのモデル駆動型アプリを作成しています。

* アプリ 3 &ndash; 関連情報を格納するカスタム エンティティと共に Contact エンティティを使用します。
* アプリ 4 &ndash; 制限付きエンティティである、Incident エンティティと共に Contact エンティティを使用します。

Barb と Isaac には次のライセンスが必要です。
* Barb には、CDS for Apps を使用してキャンバス アプリを作成するための PowerApps プラン 1 のライセンスが必要です。 Barb はデータベースまたはカスタム エンティティを作成する必要がある場合、PowerApps プラン 2 のライセンスが必要になります。

* Isaac には、モデル駆動型アプリを作成するための PowerApps プラン 2 のライセンスが必要です。

アプリ ユーザーには次のライセンスが必要です。
* アプリ 1 のユーザーに必要なのは PowerApps プラン 1 またはプラン 2 のライセンスのみです。これは、アプリに、複雑なビジネス ロジックがあるエンティティや制限付きエンティティが含まれていないためです。

* アプリ 2 のユーザーには Dynamics 365 for Customer Service, Enterprise edition のライセンス (あるいは Dynamics 365 または Dynamics 365 Customer Engagement プラン) が必要です。これは、アプリに制限付きエンティティが含まれているためです。

* アプリ 3 のユーザーには、PowerApps プラン 2 のライセンスが必要です。これは、アプリがモデル駆動型であるためです。

* アプリ 4 のユーザーには Dynamics 365 for Customer Service, Enterprise edition のライセンス (あるいは Dynamics 365 または Dynamics 365 Customer Engagement プラン) が必要です。これは、アプリに制限付きエンティティが含まれているためです。

    Dynamics 365 for Customer Service プランには PowerApps プラン 2 のライセンスが含まれているため、ユーザーはモデル駆動型アプリを実行できます。

ここで、Barb と Isaac の両方がアプリで使用しているカスタム エンティティに、Isaac がリアルタイム ワークフローを追加した場合にどのようになるかを確認してみましょう。

Barb と Isaac には次のライセンスが必要です。
* Barb には、CDS for Apps を使用してキャンバス アプリを作成するための PowerApps プラン 1 のライセンスが引き続き必要です。

* Isaac には、モデル駆動型アプリを構築するための PowerApps プラン 2 のライセンスが引き続き必要です。

アプリ ユーザーには次のライセンスが必要です。
* 現在、アプリ 1 のユーザーには PowerApps プラン 2 のライセンスが必要です。これは、リアルタイム ワークフローがあるエンティティがアプリに含まれているためです。

* アプリ 2 のユーザーには Dynamics 365 for Customer Service, Enterprise edition のライセンス (あるいは Dynamics 365 または Dynamics 365 Customer Engagement プラン) が引き続き必要です。これは、アプリに制限付きエンティティが含まれているためです。 

* アプリ 3 のユーザーには、PowerApps プラン 2 のライセンスが引き続き必要です。これは、アプリがモデル駆動型であるためです。

* アプリ 4 のユーザーには Dynamics 365 for Customer Service, Enterprise edition のライセンス (あるいは Dynamics 365 または Dynamics 365 Customer Engagement プラン) が引き続き必要です。これは、アプリに制限付きエンティティが含まれているためです。

    Dynamics 365 for Customer Service プランには PowerApps プラン 2 のライセンスが含まれているため、ユーザーはモデル駆動型アプリを実行できます。

この変更によって影響を受けるアプリはアプリ 1 のみです。このアプリにはこれまで PowerApps プラン 1 のライセンスが必要でしたが、現在は PowerApps プラン 2 のライセンスが必要です。これは、複雑なビジネス ロジックがあるエンティティがアプリに含まれているためです。 

## <a name="more-about-licensing"></a>ライセンス
PowerApps および Dynamics 365 のライセンスの詳細については、「[ライセンスの概要](../../administrator/pricing-billing-skus.md)」を参照してください。
