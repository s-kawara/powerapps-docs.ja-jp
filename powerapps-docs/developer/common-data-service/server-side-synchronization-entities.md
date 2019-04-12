---
title: サーバー側開発のエントリー (Common Data Service) | Microsoft Docs
description: サーバーサイドの同期は、Common Data Service と、受信電子メール用の 1 台以上の Exchange サーバーまたは POP3 サーバーの間、および送信電子メール用の 1 台以上の SMTP または Exchange サーバーの間のインターフェイスを提供します。
ms.custom: ''
ms.date: 02/21/2019
ms.reviewer: kvivek
ms.service: powerapps
ms.topic: article
author: mayadumesh
ms.author: mayadu
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="server-side-synchronization-entities"></a>サーバー側の同期エンティティ

PowerApps では、サーバーサイドの同期は、Common Data Service と、受信電子メール用の 1 台以上の Exchange サーバーまたは POP3 サーバーの間、および送信電子メール用の 1 台以上の SMTP または Exchange サーバーの間のインターフェイスを提供します。 これは、Common Data Service に関連性のある電子メールを取得して評価し、それに応じて、Common Data Service で対応する電子メール活動を作成します。 また、Common Data Service から電子メールを選択し、 ユーザーおよびキューの構成された電子メールサーバーを介してその電子メールが送信されます。 また、Exchange Server 2010 と Exchange Server 2013 の予定、取引先担当者、およびタスクの同期を有効にします。  
  
 一元化された電子メール構成によって、Common Data Service エンティティのモデルは、ユーザー、キュー、および転送用メールボックスに関する共通のユーザー インタフェース (UI) 設定 (ユーザー名、パスワード、電子メール アドレス、および同期方法など) を使用できます。 各ユーザーまたはキューは、サーバー側の同期または Microsoft Dynamics 365 for Outlook で監視することができるメールボックスを持つことができます。 [EmailServerProfile](/powerapps/developer/common-data-service/reference/entities/emailserverprofile) のエンティティは、組織の電子メール サーバープロファイルを表します。 [Mailbox](/powerapps/developer/common-data-service/reference/entities/mailbox) のエンティティはメールボックスの予定、取引先担当者、およびタスク配信方法を表します。 現在、ユーザーエンティティは、次の図に示すように、キューごとに1つのメールボックスのみを持つように、ユーザーとキュー エンティティごとに、1つのみのメールボックスのレコードに限定されます。  
  
 ![電子メール コネクタ エンティティ モデル](media/email-connector-entity-model.png "電子メール コネクタ エンティティ モデル")  
  
 サーバー側の同期では、次の機能を提供します:  
  
- 関連するメールボックスレコードから電子メール アドレス、電子メールの配信方法、資格情報を使用してユーザーおよびキューの電子メールを処理します。  
  
- 予定、取引先担当者、およびタスクを処理します。  
  
- 転送用メールボックスとしては受信メソッドを持つユーザーおよびキューの電子メールを処理するには、メールボックスのレコードを使用します。  
  
- メールボックスすべての電子メールを処理するために、関係する電子メール プロファイル レコードからの情報を使用します。  
  
- 非アクティブなメールボックスまたは関連付けられた電子メール プロファイルのないメールボックスに対する電子メールの処理を防ぎます。  
  
- ユーザーまたはキューがサーバー側の同期として設定した電子メールの配信方法で作成される場合、自動的に既定の電子メール プロファイルに、関連する電子メールボックスを関係付けます。  
  
- フォルダー レベルの追跡ルールに基づいて、ユーザーの PowerApps で  Microsoft Exchange の電子メールを自動的に追跡します。  
  
### <a name="related-topics"></a>関連トピック  
 [フォルダー レベルの追跡ルールの構成](configure-exchange-folder-level-tracking-rules.md) 