---
title: 単一テナント型のサーバー間認証を使用する (アプリ用 Common Data Service) | Microsoft Docs
description: <Description>
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: paulliew
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-single-tenant-server-to-server-authentication"></a>単一テナント型のサーバー間認証を使用する


単一テナント型サーバー間シナリオは通常、認証に Active Directory フェデレーション サービス (AD FS) を使用した複数のアプリ用 Common Data Service (CDS) 環境を持つエンタープライズ組織に対して適用されます。 ただしアプリケーションが他の環境に配布されない場合は、環境によって適用することが可能です。  
  
 エンタープライズは単一テナント向けのすべてのアプリ用 CDS 環境へ接続する Web アプリケーションまたは サービスを作成できます。  
  
## <a name="differences-from-multi-tenant-scenario"></a>マルチテナント型シナリオの違い  
 単一テナント型サーバー間認証の Web アプリケーションまたはサービスの作成は、マルチテナント型の組織で使用される作成と類似していますが、いくつかの重要な違いがあります。  
  
-   すべての組織がテナント内にあるため、テナント管理者が同意を許可する必要はありません。 アプリケーションが既にテナントに登録されています。  
  
-   キーよりもむしろ証明書を使用することもできます。  
  
### <a name="see-also"></a>関連項目  
 [マルチ テナント型でのサーバー間認証の使用](use-multi-tenant-server-server-authentication.md)   
 [サーバー間 (S2S) の認証を使用して Web アプリケーションを作成する](build-web-applications-server-server-s2s-authentication.md)

<!--

 Can this scenario be hightlighted here: https://crmtipoftheday.com/767/server-to-server-authentication-is-here/

-->