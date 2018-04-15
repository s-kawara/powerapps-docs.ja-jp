---
title: 開発者向けのモデル駆動型アプリの概要 | Microsoft Docs
description: 開発者がどのような価値をモデル駆動型アプリに付加できるか説明します。
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
ms.date: 03/17/2018
ms.author: jdaly
ms.openlocfilehash: 4e8a935dbef2c46478f99ecbf82a7fc837feb284
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="model-driven-apps-developer-overview"></a>モデル駆動型アプリの概要

PowerApps は、ユーザー、企業、パートナー、独立系ソフトウェア ベンダー (ISV)、およびシステム インテグレーター (SI) が基幹業務アプリを構築するために使用する強力なプラットフォームです。 このリリースでは、新しい Common Data Service for Apps を使用してビルドされたモデル駆動型アプリが PowerApps に新しく追加されています。 Common Data Service for Apps に Dynamics 365 Customer Engagement アプリケーションのコア機能が含まれるようになりました。 モデル駆動型アプリでは、それらのアプリケーションと同じ拡張機能を使用するアプリをビルドできます。

モデル駆動型アプリは、ノーコードまたはローコードのコンポーネントに焦点を当てたアプリ開発の手法です。 開発者はアプリケーションを拡張するという価値を提供できます。 コードを記述する前に、まず、モデル駆動型アプリの構築方法と、コードなしにどのようなオプションを追加できるか学んでください。 

## <a name="get-started"></a>はじめる
Dynamics 365 Customer Engagement に習熟している場合、その経験をモデル駆動型アプリのビルドに活かすことができます。 いくつか新しいデザイナーが提供されており、概念はほとんど同じです。

> [!NOTE]
> モデル駆動型アプリが、Common Data Service for Apps に接続します。 サービス レベルで開発者がどのように価値を追加できるかの詳細については、「[Common Data Service for Apps Developer の概要](../common-data-service/overview.md)」を参照してください。
> このセクションの内容は、モデル駆動型アプリのユーザー用に、開発者が適用できる拡張機能についてのみ言及しています。 

このセクションのトピックでは、Dynamics 365 Customer Engagement アプリケーションを初めて使用する開発者に、モデル駆動型アプリで作業を開始する際の重要な概念の概要を説明します。 

> [!NOTE]
> Common Data Service for Apps と Dynamics 365 Customer Engagement は、同じプラットフォームを使用しているため、開発者向けには、「[Dynamics 365 Customer Engagement 開発者ガイド](/dynamics365/customer-engagement/developer/developer-guide)」により詳細な情報があります。 これらのトピックでは、概要と、より詳細な開発者ガイドおよびその他のガイドへのリンクがあります。


## <a name="community-tools-for-model-driven-apps"></a>モデル駆動型アプリ用のコミュニティ ツール

Dynamics 365 コミュニティでは、ツールを作成しています。 人気が高いツールの多くは、[XrmToolBox](https://www.xrmtoolbox.com/) から配布されています。 XrmToolBox は、カスタマイズ、構成、操作タスクを容易にするツールを提供する、Common Data Service for Apps に接続する、Windows アプリケーションです。 これには、管理、カスタマイズまたは構成タスクを簡単に、またより少ない時間で行えるようにするプラグインが 30 以上付属しています。

モデル駆動型アプリを操作するとき使用できる、XrmToolBox から配布される厳選されたコミュニティ ツールの一覧を次に示します。

|ツール  |説明  |
|---------|---------|
|[Easy Translator](https://www.xrmtoolbox.com/plugins/MsCrmTools.Translator/)|コンテキストに応じた情報を使用して、変換をエクスポートおよびインポートできます。|
|[Excel にエクスポート](https://www.xrmtoolbox.com/plugins/Ryr.XrmToolBox.ExportToExcel/)|レコードを選択されたビュー/fetchxml から Excel に簡単にエクスポートできます。|
|[Iconator](https://www.xrmtoolbox.com/plugins/MscrmTools.Iconator/)|1 つの画面でユーザー定義のエンティティ アイコンを管理できます。|
|[Ribbon Workbench 2016](https://www.xrmtoolbox.com/plugins/RibbonWorkbench2016/)|XrmToolbox 内で、Dynamics CRM リボンまたはコマンド バーを編集できます。|
|[ビュー デザイナー](https://www.xrmtoolbox.com/plugins/Cinteros.XrmToolBox.ViewDesigner/)|ビューのレイアウトを設計し、FetchXML Builder を使用してクエリを簡単に変更できる UI が用意されています。|
|[View Layout Replicator](https://www.xrmtoolbox.com/plugins/MsCrmTools.ViewLayoutReplicator/)|1 回の操作で、同じエンティティの複数のビューに同じレイアウトを適用できます。|
|[WebResources Manager](https://www.xrmtoolbox.com/plugins/MsCrmTools.WebResourcesManager/)|Web リソースを簡単に管理できます。|

XrmToolBox からの配布ではないもう 1 つのツールに、Jason Lattimer 氏の [CRM REST Builder](https://github.com/jlattimer/CRMRESTBuilder) があります。 このツールは、Web API で使用する JavaScript コードを生成します。

> [!NOTE]
> コミュニティで作成されるツールは、Microsoft ではサポートしていません。 コミュニティ ツールに関するご質問や問題については、そのツールの発行元にお問い合わせください。




