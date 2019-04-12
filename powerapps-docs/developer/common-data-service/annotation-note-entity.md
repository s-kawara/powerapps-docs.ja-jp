---
title: 注釈 (メモ) エンティティ (Common Data Service) | Microsoft Docs
description: データベース内の任意のレコードに追加的な情報を付加する簡便な手段を提供する注釈 (メモ) エンティティについて。 コメント エンティティはコメントを表します。このエンティティには、コメントのテキスト、コメントの作成者および変更者、コメントの添付ファイルの有無などの情報が含まれます。
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
# <a name="annotation-note-entity"></a>コメント (Annotation) (メモ) エンティティ

*注釈 (メモ)* は Common Data Service データベース内の任意のレコードに追加的な情報を付加する簡便な手段を提供するものです。 注釈 (メモ) は Common Data Service の任意のエンティティに関連付けることができるテキスト エントリです。 ただし、注釈は、<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest.HasNotes> プロパティを <xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest> クラスで `true` に設定して作成したカスタム エンティティにのみ関連付けることができます。 メモで有効になっていないカスタム エンティティは、<xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest>.<xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest.HasNotes> プロパティを `true` に設定することにより、メモを使用するよう更新することができます。  

Web APIを使用して、<xref:Microsoft.Dynamics.CRM.EntityMetadata> EntityType の `HasNotes` プロパティをこれコントロールするように設定します。
  
 `Annotation` エンティティは注釈 (メモ) を表し、以下の情報を持ちます。  
  
-   注釈 (メモ) テキスト  
  
-   注釈 (メモ) の作成者または変更者  
  
-   注釈 (メモ) にファイルが添付されているかどうか  
  
 添付ファイルは、Office Wordドキュメント、Office Word スプレッドシート、CAD ファイル、PDF ファイルなどの、標準形式の任意のコンピューター ファイルです。 添付ファイルは、注釈 (メモ) を除く Common Data Service の任意のオブジェクトに関連付けることができます。  
  
 添付ファイルをアップロードまたは削除するには、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*> メソッドまたは<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> メッセージを使用して、`Annotation.Filename` および `Annotation.MimeType` プロパティを設定します。 このメッセージは、base64 文字列形式にデコードされた添付ファイルをアップロードします。 [System.Convert.ToBase64String](https://msdn.microsoft.com/library/system.convert.tobase64string.aspx) メソッドで、データ ファイルの内容を base64 形式の文字列に変換できます。 アップロードできる最大ファイル サイズは、**Organization.MaxUploadFileSize** プロパティによって決まります。 このプロパティは、Dynamics 365 アプリケーションの**システム設定**の**電子メール**タブで設定します。 この設定で電子メール メッセージ、メモ、および Web リソースに添付できるファイルのサイズを制限します。 既定の設定は 5 MB です。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [サンプル: 添付ファイルのアップロード、取得、およびダウンロード](/dynamics365/customer-engagement/developer/sample-upload-retrieve-download-attachment)  
  
### <a name="see-also"></a>関連項目 
 [コメント エンティティ](reference/entities/annotation.md)   
 [ビジネス データのモデル化](/dynamics365/customer-engagement/developer/model-business-data)   
 [UserQuery (保存されているビュー) エンティティ](/dynamics365/customer-engagement/developer/userquery-saved-view-entity)