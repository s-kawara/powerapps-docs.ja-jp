---
title: Enable および Disable 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Enable および Disable 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: f3932d21683b83008e95f03ba2aae646d2b8e491
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61551079"
---
# <a name="enable-and-disable-functions-in-powerapps"></a>PowerApps の Enable および Disable 関数
[シグナル](signals.md) を有効または無効に切り替えます。

## <a name="overview"></a>概要
いくつかのシグナルは頻繁に変化する場合があるため、アプリはその度に再計算を行う必要があります。  長期間にわたる頻繁な変更によって、デバイスのバッテリが消耗することがあります。 これらの関数を使用すると、手動でシグナルを有効または無効にすることができます。

シグナルは使用されていない場合、自動的に無効になります。

## <a name="description"></a>説明
**Enable** 関数と **Disable** 関数はそれぞれ、シグナルを有効および無効に切り替えます。

これらの関数は、現在、 **[Location](signals.md)** シグナルのみに有効です。

これらの関数には、戻り値がありません。 これらの関数は、[動作の数式](../working-with-formulas-in-depth.md)内でのみ使用できます。

## <a name="syntax"></a>構文
**Enable**( *Signal* )<br>**Disable**( *Signal* )

* *Signal* - 必須。  有効または無効にするシグナル。

