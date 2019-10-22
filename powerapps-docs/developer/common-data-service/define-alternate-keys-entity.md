---
title: 代替キーを使用する (Common Data Service) | Microsoft Docs
description: このトピックスではエンティティの代替キーの作成方法について説明します。 代替キーはプログラムで、またはカスタマイズ ツールを使用して作成することができます
ms.custom: ''
ms.date: 06/04/2019
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
# <a name="work-with-alternate-keys"></a>代替キーに関する作業

すべての Common Data Service レコードには、GUID として定義されている一意の識別子を持っています。 これは、各エンティティの主キーです。 外部データ ストアと統合する必要がある場合は、Common Data Service 内の一意の識別子への参照を格納するために、外部データベース テーブルに列を追加できる場合があります。 これにより、Common Data Service レコードにリンクするためのローカル参照を設けることができます。 ただし、外部データベースを変更できないことがあります。 ユーザーは、現在は、代替キーを使用して、外部のデータ ストアが使用する一意の識別子 (または一意の列の組み合わせ) に一致するように、Common Data Service エンティティの属性を定義できます。 主キーの代わりにこの代替キーを使用して、Common Data Service 内のレコードを一意に識別できます。 どの属性が、レコードごとの一意の ID を表すかを定義できるようにする必要があります。 エンティティに対して一意となる属性を識別したら、それらの属性をカスタマイズ ユーザー インターフェイス (UI) によって、またはコードで、代替キーとして宣言できます。 このトピックでは、データ モデルでの代替キーの定義について説明します。  

<a name="BKMK_Declare"></a>

## <a name="create-alternate-keys"></a>代替キーの作成  

プログラムで、またはカスタマイズ ツールを使用して、代替キーを作成できます。 カスタマイズ ツールの使用の詳細については、「[CRM レコードを参照する代替キーの定義](https://technet.microsoft.com/library/29e53691-0b18-4fde-a1d0-7490aa227898.aspx)」を参照してください。  

代替キーをプログラムで定義するには、最初に <xref:Microsoft.Xrm.Sdk.Metadata.EntityKeyMetadata> (または、Web API で作業する場合は <xref href="Microsoft.Dynamics.CRM.EntityKeyMetadata?text=EntityKeyMetadata EntityType" /> を使用) の種類のオブジェクトを作成する必要があります。 このクラスには、キー属性が含まれています。 キー属性が設定されると、`CreateEntityKey` を使用してエンティティに対するキーを作成することができます。 このメッセージは、エンティティ名と `EntityKeyMetadata` 値を、キーを作成するための入力として使用します。  

代替キーを作成するときは、以下の制限に注意ください。  

- **キー定義での有効な属性**  

   以下の種類の属性のみを、代替キーの定義に含めることができます。  


  |      属性の種類      |    表示名     |
  |--------------------------|---------------------|
  | DecimalAttributeMetadata |   10 進数    |
  | IntegerAttributeMetadata |    整数     |
  | StringAttributeMetadata  | 1 行テキスト |
  | DateTimeAttributeMetadata   |      日時    |
  | LookupAttributeMetadata     |       ルックアップ        |
  | PicklistAttributeMetadata   |      [オプション セット]       |


- **有効なキーのサイズ**  

   キーの作成時に、合計のキー サイズが、キー当たり 900 バイト、キー当たり 16 列などの SQL ベースのインデックスの制約に違反しないことを含め、キーがプラットフォームによってサポートされることの確認が行われます。 キー サイズがその制約に適合しない場合は、エラー メッセージが表示されます。  

- **1 つのエンティティに対する代替キーの定義の最大数**  

   Common Data Service インスタンス内の 1 つのエンティティに対して、代替キーの定義は最大 5 つです。  

- **キー値内の Unicode 文字**

  代替キーで使用されるフィールド内のデータに `<`,`>`,`*`,`%`,`&`,`:`,`\\` などの文字が含まれている場合は、get アクションまたは patch アクションは機能しません。  一意性のみを必要とする場合はこの方法も使用することができますが、これらのキーをデータ統合の一部として使用する必要がある場合は、これらの文字を持つデータを持たないフィールド上でキーを作成するのが最善です。

<a name="BKMK_crud"></a>   

## <a name="retrieve-and-delete-alternate-keys"></a>代替キーの取得および削除  

代替キーを取得、または削除する必要がある場合は、コードを書かなくても、カスタマイズ UI を使用して、これを実行できます。 ただし、SDK は代替キーをプログラムで取得および削除するために、次の 2 つのメッセージを用意しています。  

|メッセージ要求クラス|説明|  
|---------------------------|-----------------|  
|<xref:Microsoft.Xrm.Sdk.Messages.RetrieveEntityKeyRequest>|指定した代替キーを取得します。|  
|<xref:Microsoft.Xrm.Sdk.Messages.DeleteEntityKeyRequest>|指定した代替キーを削除します。|  

1 つのエンティティのすべてのキーを取得するには、`EntityMetadata` (<xref href="Microsoft.Dynamics.CRM.EntityMetadata?text=EntityMetadata EntityType" /> または <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata> クラス) の新しい<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.Keys> プロパティを使用します。 これは、1 つのエンティティに対するキーの配列を取得します。  

<a name="BKMK_index"></a>   

## <a name="monitor-index-creation-for-alternate-keys"></a>代替キーのインデックス作成の監視  

代替キーはデータベース インデックスを使用して、一意性を実施し、検索のパフォーマンスを最適化します。 テーブルに多数のレコードが存在する場合は、インデックスの作成は長いプロセスになる可能性があります。 インデックスの作成をバックグラウンド プロセスで行うことによって、カスタマイズ UI とソリューションのインポートの応答性を向上させることができます。 `EntityKeyMetadata.AsyncJob` プロパティ (<xref href="Microsoft.Dynamics.CRM.EntityKeyMetadata?text=EntityKeyMetadata EntityType" /> または <xref:Microsoft.Xrm.Sdk.Metadata.EntityKeyMetadata>) は、インデックスの作成を実行する非同期ジョブを参照します。 `EntityKeyMetadata.EntityKeyIndexStatus` プロパティは、インデックス作成のジョブの進捗に合わせてキーの状態を指定します。 この状態は、以下のいずれかになります。  

- 保留中  
- 処理中  
- アクティブ  
- 失敗  

API を使用して代替キーを作成するとき、インデックスの作成が失敗した場合は、失敗の原因の詳細を掘り下げて、問題を修正し、`ReactivateEntityKey` (<xref href="Microsoft.Dynamics.CRM.ReactivateEntityKey?text=ReactivateEntityKey Action" /> または <xref:Microsoft.Xrm.Sdk.Messages.ReactivateEntityKeyRequest> メッセージ) を使用して、キー要求を再びアクティブ化することができます。  

インデックス作成のジョブが保留中または進行中に、代替キーが削除されると、そのジョブは取り消され、インデックスが削除されます。  

### <a name="see-also"></a>関連項目  
 [代替キーの使用](use-alternate-key-create-record.md)<br />
 [変更の追跡を使用してデータを外部システムに同期](use-change-tracking-synchronize-data-external-systems.md)<br />
 [Upsert を使用してレコードを挿入または更新](use-upsert-insert-update-record.md) [レコードを参照する代替キーの定義](../../maker/common-data-service/define-alternate-keys-reference-records.md)
