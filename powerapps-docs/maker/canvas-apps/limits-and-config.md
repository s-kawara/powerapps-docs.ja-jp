---
title: システム要件、制限、構成値 | Microsoft Docs
description: PowerApps のシステム要件、制限、構成値
documentationcenter: na
author: skjerland
manager: kfile
editor: ''
tags: ''
ms.service: PowerApps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 03/07/2018
ms.author: sharik
ms.openlocfilehash: 5cd2fdf5150d008f905e4c5c8177e6331545848e
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="system-requirements-limits-and-configuration-values"></a>システム要件、制限、構成値
このトピックには、PowerApps についての、デバイス プラットフォーム、Web ブラウザーの要件、制限と構成値が含まれています。

## <a name="supported-platforms-for-running-apps-using-the-powerapps-app"></a>PowerApps アプリを使用してアプリを実行するためにサポートされているプラットフォーム
| **最小構成** | **推奨** |
| --- | --- |
| iOS 9.3 以降 |iOS 10 以降と少なくとも 2 GB の RAM |
| Android 5 以降 |Android 7 以降と少なくとも 4 GB の RAM |
| Windows 8.1 以降 (PC のみ) |Windows 10 Fall Creators Update と少なくとも 8 GB の RAM)|

## <a name="supported-browsers-for-running-apps"></a>アプリを実行するためのサポートされているブラウザー
| **ブラウザー** | **オペレーティング システム** |
| --- | --- |
| Google Chrome (最新バージョン)<br>(推奨) |Windows 7 SP1、8.1、および 10 <br>Android 5 以降 <br>iOS 8 以降<br>macOS |
| Microsoft Edge (最新バージョン)<br>(推奨) |Windows 10 |
| Microsoft Internet Explorer 11 (互換表示オフ) |Windows 7 SP1、8.1、および 10 |
| Mozilla Firefox (最新バージョン) |Windows 7 SP1、8.1、および 10 <br> Android 5 以降 <br>iOS 8 以降 <br>macOS |
| Apple Safari (最新バージョン) |iOS 8 以降 <br>macOS |

## <a name="supported-browsers-for-powerapps-studio-for-web"></a>PowerApps Studio for web のサポートされているブラウザー
| **ブラウザー** | **オペレーティング システム** |
| --- | --- |
| Google Chrome (最新バージョン)<br>(推奨) |Windows 7 SP1、8.1、および 10 <br>macOS |
| Microsoft Edge (最新バージョン)<br>(推奨) |Windows 10 |
| Microsoft Internet Explorer 11 (互換表示オフ) |Windows 7 SP1、8.1、および 10 |

## <a name="request-limits"></a>要求の制限
次の制限は、1 つの送信要求ごとに適用されます。

| 名前 | 制限 |
| --- | --- |
| タイムアウト |180 秒 |
| 再試行回数 |4 |

> [!NOTE]
> 再試行回数が異なる場合があります。 エラーの状況によっては、再試行は無意味です。

## <a name="ip-addresses"></a>IP アドレス
PowerApps からの要求では、アプリが存在する[環境](../../administrator/environments-overview.md)のリージョンによって、使用する IP アドレスが異なります。 PowerApps のシナリオで利用できる完全修飾ドメイン名は公開されていません。

アプリ経由で接続される API (たとえば、SQL API や SharePoint API) から行われる呼び出しでは、このトピックの後半で説明する IP アドレスを使用します。

たとえば、Azure SQL データベース用に IP アドレスをホワイトリスト登録する必要がある場合は、これらのアドレスを使用する必要があります。

| リージョン | 送信 IP |
| --- | --- |
| アジア |52.163.91.227, 52.163.89.40, 52.163.89.65, 52.163.95.29, 13.75.89.9, 13.75.91.198, 13.75.92.202, 13.75.92.124 |
| オーストラリア |13.77.7.172, 13.70.191.49, 13.70.189.7, 13.70.187.251, 13.70.82.210, 13.73.203.158, 13.73.207.42, 13.73.205.35 |
| カナダ |52.233.30.222, 52.233.30.148, 52.233.30.199, 52.233.29.254, 52.232.130.205, 52.229.126.118, 52.229.126.28, 52.229.123.56 |
| ヨーロッパ |52.166.241.149, 52.166.244.232, 52.166.245.173, 52.166.243.169, 40.69.45.126, 40.69.45.11, 40.69.45.93, 40.69.42.254 |
| インド |52.172.54.172, 52.172.55.107, 52.172.55.84, 52.172.51.70, 52.172.158.185, 52.172.159.100, 52.172.158.2, 52.172.155.245 |
| 日本 |104.214.137.186, 104.214.139.29, 104.214.140.23, 104.214.138.174, 13.78.85.193, 13.78.84.73, 13.78.85.200, 13.78.86.229 |
| 米国 |104.43.232.28, 104.43.232.242, 104.43.235.249, 104.43.234.211, 52.160.93.247, 52.160.91.66, 52.160.92.131, 52.160.95.100, 40.117.101.91, 40.117.98.246, 40.117.101.120, 40.117.100.191 |
| 米国 (早期アクセス) |52.161.26.191, 52.161.27.42, 52.161.29.40, 52.161.26.33, 13.66.213.240, 13.66.214.51, 13.66.210.166, 13.66.213.29 |

## <a name="required-services"></a>必要なサービス
この一覧で、PowerApps Studio が通信するすべてのサービスと用途を確認できます。 ネットワークでこれらのサービスをブロック**しないでください**。

| ドメイン | プロトコル | 使用するサービス |
| --- | --- | --- |
| management.azure.com |https |RP |
| msmanaged-na.azure-apim.net |https |コネクタ/API のランタイム |
| login.microsoft.com<br>login.windows.net<br>login.microsoftonline.com<br>secure.aadcdn.microsoftonline-p.com |https |ADAL |
| graph.microsoft.com<br>graph.windows.net |https |Azure Graph - ユーザー情報の取得用 (例: プロファイルの写真) |
| gallery.azure.com |https |サンプルおよびテンプレート アプリ |
| *.azure-apim.net |https |API のハブ - ロケールごとに異なるサブドメイン |
| *.powerapps.com |https |WebAuth + ポータル |
| *.azureedge.net |https |WebAuth |
| *.blob.core.windows.net |https |Blob Storage |
| vortex.data.microsoft.com |https |製品利用統計情報 |
