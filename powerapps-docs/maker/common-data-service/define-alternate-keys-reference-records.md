---
title: アプリ用 Common Data Service でレコードを参照する代替キーを定義 | MicrosoftDocs
description: アプリ用 Common Data Service で、レコードを参照するために使用できる代替キーを定義する方法を説明します
ms.custom: ''
ms.date: 06/06/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: 29e53691-0b18-4fde-a1d0-7490aa227898
caps.latest.revision: 10
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="define-alternate-keys-to-reference-records"></a>レコードを参照する代替キーの定義

*代替キー*は、外部システムとデータを統合するための効率のよい正確な方法を提供します。 外部システムが、アプリ用 Common Data Service のレコードを一意に識別するグローバル一意識別子 (GUID) の ID を保存していない場合には、サポート案件が不可欠です。 

データの統合システムは、代替キーを使用し、固有の組み合わせを表す 1 つ以上のエンティティ フィールド値を使用してレコードを一意に識別します。 各代替キーには一意の名前があります。 

たとえば、代替キーを使用してアカウント レコードを識別するには、変更しない値を持つ他のフィールドと組み合わせて、アカウント番号または取引先企業番号フィールドを使用できます。

> [!NOTE]
> PowerApps で代替キーを定義できますが、コード内でプログラムのみ使用できます。 プログラムで代替キーを使用する場合の詳細については、以下を参照してください。   
> - [開発者向けドキュメント: 代替キーを使用してレコードを作成](/dynamics365/customer-engagement/developer/use-alternate-key-create-record) 
> - [開発者向けドキュメント: 代替キーを使用して Web API でレコードを取得](/dynamics365/customer-engagement/developer/webapi/retrieve-entity-using-web-api#retrieve-using-an-alternate-key)

代替キーの機能の利点には、次のものが含まれます。  
  
- レコードのより迅速な検索。  
- より堅牢なデータの一括操作。  
- レコード ID を使用せずに、外部システムからのデータによる簡易なプログラミング。  
  

## <a name="creating-an-alternate-key"></a>代替キーの作成

代替キーを作成するために使用できる 2 人のデザイナーがいます。

|デザイナー| 説明|
|--|--|
|[PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)|簡単な優れたエクスペリエンスを提供しますが、一部のオプションは使用できません。<br />詳細: [PowerApps ポータルを使用した代替キーの定義](define-alternate-keys-portal.md)|
|ソリューション エクスプローラー|簡単ではありませんが、一般的な要件が少ない割に柔軟性が高くなっています。<br />詳細: [ソリューション エクスプローラーを使用した代替キーの定義](define-alternate-keys-solution-explorer.md) |

> [!NOTE]
> 以下を使用して、お客様の環境に代替キーを作成することもできます。
> - 代替キーの定義を含むソリューションをインポートします。
> - 開発者はコードを記述して作成することもできます。 詳細: [開発者向けドキュメント: エンティティの代替キーの定義](/dynamics365/customer-engagement/developer/define-alternate-keys-entity)

このトピックの情報は、使用できるデザイナーの選択に役立ちます。 

次のいずれかの要件に対処する必要がない限り、[PowerApps portal ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)を使用して代替キーを作成する必要があります。

- アプリ用 Common Data Service の既定のソリューション以外のソリューション内で代替キーを作成する
- サポート インデックスの作成の進行状況を追跡するシステム ジョブを簡単に追跡します


## <a name="limits-in-creating-alternate-keys"></a>代替キーを作成する際の制限

代替キーの作成には制約があります。

### <a name="fields-that-can-be-used-for-alternate-keys"></a>代替キーに使用できるフィールド

これらの種類のフィールドのみ代替キーを作成するために使用することができます。
 - [小数]
 - 整数
 - 1 行テキスト (文字列)

### <a name="number-of-keys"></a>キーの番号

1 つのエンティティに対して最大 5 つの異なるキーを定義できます。
 
### <a name="valid-key-size"></a>有効なキーのサイズ

キーの作成時に、合計のキー サイズが、キー当たり 900 バイト、キー当たり 16 列などの SQL ベースのインデックスの制約に違反しないことを含め、キーがプラットフォームによってサポートされることの確認が行われます。 キー サイズがその制約に適合しない場合は、エラー メッセージが表示されます。

### <a name="unicode-characters-in-key-value"></a>キー値内の Unicode 文字

代替キーで使用されるフィールド内のデータに `<`、`>`、`*`、`%`、`&`、`:`、`\\` のいずれかが含まれる場合、patch または upsert アクションは動作しません。 

一意性のみを必要とする場合はこの方法も使用することができますが、これらのキーをデータ統合の一部として使用する必要がある場合は、これらの文字を持つデータを持たないフィールド上でキーを作成するのが最善です。

## <a name="track-the-status-of-the-creation-of-the-alternate-key"></a>代替キーの作成状態を追跡する

代替キーが作成されると、システム ジョブが開始され、データベース テーブルにインデックスが作成され、代替キーによって使用されるフィールドに一意の制約が適用されます。 代替キーは、これらのインデックスが作成されるまで有効ではありません。 これらのインデックスの作成には、システム内のデータ量に応じて時間がかかることがあります。 

システム ジョブの状態によって代替キーの状態が決まります。 代替キーは次の状態を持つことができます。
- **保留**
- **処理中**
- **Active**
- **失敗**

システム ジョブが完了すると、代替キーの状態は**アクティブ**になり使用可能になります。

システム ジョブが失敗した場合は、システム ジョブを見つけてエラーを表示します。 システム ジョブでは、以下のパターンに従う名前があります。`Create index for {0} for entity {1}`ここで `0` は代替キーの**表示名**であり、`1` はエンティティの名前です。


> [!NOTE]
> システム ジョブの状態を監視するには、ソリューション エクスプローラーを使用してインデックスを作成する必要があります。 それを監視できるように、システム ジョブへのリンクを含みます。 詳細: [(任意) インデックスのシステム ジョブ追跡の作成を表示](define-alternate-keys-solution-explorer.md#optional-view-the-system-job-tracking-creation-of-indexes)
  
  
### <a name="see-also"></a>関連項目  

[PowerApps ポータルを使用した代替キーの定義](define-alternate-keys-portal.md)<br />
[ソリューション エクスプローラーを使用した代替キーの定義](define-alternate-keys-solution-explorer.md)<br />
[開発者向けドキュメント: エンティティの代替キーを定義](/dynamics365/customer-engagement/developer/define-alternate-keys-entity)<br />
[開発者向けドキュメント: 代替キーを使用してレコードを作成](/dynamics365/customer-engagement/developer/use-alternate-key-create-record)
