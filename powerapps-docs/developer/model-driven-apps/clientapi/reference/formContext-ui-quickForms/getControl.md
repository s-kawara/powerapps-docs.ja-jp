---
title: モデル駆動型アプリの getControl (クライアント API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 57eb6b4b-90c1-4d56-b4b0-a7160af17f8f
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getcontrol-client-api-reference"></a>getControl (クライアント API 参照)



[!INCLUDE[./includes/getControl-description.md](./includes/getControl-description.md)]

## <a name="syntax"></a>構文

`quickViewControl.getControl(arg);`

## <a name="parameter"></a>パラメーター

**引数**: オプション。 簡易表示コントロール内の構成コントロールの名前またはインデックス値として引数を渡すことによって、構成コントロール コレクション内の単一のコントロールにアクセスできます。 たとえば、`quickViewControl.getControl("firstname")` や `quickViewControl.getControl(0)` などです。


## <a name="return-value"></a>戻り値

**種類**: オブジェクトまたはオブジェクト コレクション。

**説明** : パラメーターを指定してメソッドを使用する場合はオブジェクトであり、パラメーターなしでメソッドを使用する場合はオブジェクト コレクションです。

## <a name="remarks"></a>備考

簡易表示コントロールでスタッフ コントロールの取得後、スタッフ コントロール データを変更しないスタッフ コントロールにモデル駆動型アプリのコントロールをサポートしている任意のメソッドを使用できます。 これは、簡易表示コントロールの構成コントロールが読み取りなためです。 たとえば、次を使用できます。 

`quickViewControl.getControl(0).getAttribute()` 

コントロールがサポートするメソッドの詳細については、「[コントロール](../controls.md)」を参照してください。

>[!IMPORTANT]
>[getAttribute](../controls/getAttribute.md) または構成コントロール上の関連メソッドのデータは、メイン フォーム [OnLoad](../events/form-onload.md) イベントで動作しない可能性があります。メイン フォームが読み込まれたとき、バインドされている簡易表示フォームが完全には読み込まれていないためです。 簡易表示コントロール インスタンスの [isLoaded](isLoaded.md) メソッドを使用すると、バインドされている簡易表示フォームの読み込みが完了したかどうかを特定するのに役立ちます。 

>または、フォームの簡易表示フォームの構成コントロールを新しいフォーム レンダリング エンジンを使用して取得する方法は、レガシ フォームの場合とは異なります。 レガシ フォームを使用して簡易表示コントロールで構成コントロールを対象としているコードがある場合は、新しいフォーム レンダリング エンジンを使用することを決定する場合にコードを更新する必要があります。

### <a name="related-topics"></a>関連トピック

[formContext.ui.quickForms](../formContext-ui-quickForms.md)



