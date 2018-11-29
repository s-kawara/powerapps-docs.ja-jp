---
title: コードを使用した重複データの検出 (アプリ用 Common Data Service) | Microsoft Docs
description: 重複データ検出により、組織は重複データ検出ポリシーを設定し、ビジネス エンティティとユーザー定義エンティティに対する重複データ検出ルールを作成することができます
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
# <a name="detect-duplicate-data-using-code"></a>コードを使用した重複データの検出

組織で重複データ検出ポリシーを設定し、ビジネス エンティティとユーザー定義エンティティに対する重複データ検出ルールを作成することができます。 このルールはアプリ用 Common Data Service (CDS) のさまざまな種類のレコードに対して適用できます。 たとえば、ある潜在顧客と取引先担当者の名前および電話番号が同じである場合、その潜在顧客は取引先担当者の重複データであると定義することができます。 ユーザーが新しいレコードを作成したり既存レコードを更新したりするときに、管理者の設定した重複データ検出ルールに基づいて、ユーザーに重複データの可能性があることが警告されます。 データ品質を維持するために、特定の条件を満たすレコードすべてに対して重複データのチェックを実行する重複データ検出ジョブをスケジュール設定することができます。 重複データ検出ジョブで検出された重複データは、削除、非アクティブ化、または統合することで消去できます。

> [!NOTE]
> ユーザー インターフェイス (UI) を使用して重複データを検出するためのルールの作成方法およびシステム ジョブの実行方法については、 [重複データを検出して修正または削除できるようにする](/dynamics365/customer-engagement/admin/detect-duplicate-data) を参照してください。

Web API および組織サービスを使用して重複データを検出できます。 このセクションのトピックでは、両方の Web サービスを使用して重複データを検出する方法についての情報を提供します。 

### <a name="see-also"></a>関連項目

[重複データ検出の有効化と無効化](enable-disable-duplicate-detection.md)<br/>
[重複データ検出を実行する](run-duplicate-detection.md)<br/>
[重複データ検出のメッセージ](duplicate-detection-messages.md)<br/>
[重複ルール エンティティ](duplicaterule-entities.md)

