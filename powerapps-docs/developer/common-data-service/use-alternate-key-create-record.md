---
title: 代替キーを使用してレコードを作成 (Common Data Service) | Microsoft Docs
description: 代替キーを使用して、エンティティおよび EntityReference クラスのインスタンスを作成できます。 このトピックでは、使用パターンと、代替キー使用時にスローされる可能性のある例外について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-an-alternate-key-to-create-a-record"></a>代替キーを使用してレコードを作成

代替キーを使用して、<xref:Microsoft.Xrm.Sdk.Entity> および <xref:Microsoft.Xrm.Sdk.EntityReference> クラスのインスタンスを作成できます。 このトピックでは、使用パターンと、代替キー使用時にスローされる可能性のある例外について説明します。 エンティティに対して代替キーを定義する方法については、「[エンティティの代替キーの定義](define-alternate-keys-entity.md)」を参照してください。  
  
<a name="BKMK_entity"></a>   
## <a name="using-alternate-keys-to-create-an-entity"></a>エンティティを作成するための代替キーの使用  
 プライマリ ID または単一の`KeyAttribute` があれば、コンストラクターを使用して、1 回の呼び出しで、<xref:Microsoft.Xrm.Sdk.Entity> を作成できます。  
  
```csharp  
public Entity (string logicalName, Guid id) {…}    
public Entity (string logicalName, string keyName, object keyValue) {…}  
public Entity (string logicalName, KeyAttributeCollection keyAttributes) {…}  
  
```  
  
 更新操作に使用される有効な <xref:Microsoft.Xrm.Sdk.Entity> には、エンティティの論理名と次のいずれかが含まれています。  
  
-   ID の値 (主キーの GUID 値) (または)  
  
-   そのエンティティに定義されているキーに一致する有効な属性セットを持つ <xref:Microsoft.Xrm.Sdk.KeyAttributeCollection>。  
  
<a name="BKMK_EntityReference"></a>   
## <a name="using-alternate-keys-to-create-an-entityreference"></a>EntityReference の作成に代替キーを使用  
 また、プライマリ ID がなくても、単一の  `KeyAttribute` があれば、新しいコンストラクターを使用して、1 回の呼び出しで、<xref:Microsoft.Xrm.Sdk.EntityReference> を作成することもできます。  
  
```csharp  
public EntityReference(string logicalName, Guid id) {…}    
public EntityReference(string logicalName, string keyName, object keyValue) {…}    
public EntityReference(string logicalName, KeyAttributeCollection keyAttributeCollection) {…}  
  
```  
  
 有効な <xref:Microsoft.Xrm.Sdk.EntityReference> には、エンティティの論理名とつぎのいずれかが含まれています。  
  
-   ID の値 (主キーの GUID 値) または、  
  
-   そのエンティティに対して定義されているキーに一致する有効な属性セットを持つ <xref:Microsoft.Xrm.Sdk.KeyAttributeCollection> コレクション。  
  
<a name="BKMK_input"></a>   
## <a name="alternative-input-to-messages"></a>メッセージへの代替入力  
 エンティティを <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> および <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> に渡すとき、<xref:Microsoft.Xrm.Sdk.EntityReference> を使用する検索属性のために提供された値は、<xref:Microsoft.Xrm.Sdk.EntityReference> を <xref:Microsoft.Xrm.Sdk.EntityReference.KeyAttributes> で定義された代替キーと共に使用して、関連レコードを指定することができるようになります。  これらは解決され、メッセージが処理される前にプライマリ ID ベースのエンティティ参照に置き換えられます。  
  
<a name="BKMK_Exceptions"></a>   
## <a name="exceptions-when-using-alternate-keys"></a>代替キー使用時の例外  
 代替キーを使用するときは、以下のような条件と起こり得る例外に注意してください。  
  
-   プライマリ ID が用意されている場合、プライマリ ID が使用されます。 用意されていない場合は、<xref:Microsoft.Xrm.Sdk.KeyAttributeCollection> の確認が行われます。  <xref:Microsoft.Xrm.Sdk.KeyAttributeCollection> が用意されていない場合は、エラーをスローします。  
  
-   用意された <xref:Microsoft.Xrm.Sdk.KeyAttributeCollection> にエンティティの主キーである 1 つの属性が含まれていて、その値が有効である場合、その用意された値が <xref:Microsoft.Xrm.Sdk.Entity> または <xref:Microsoft.Xrm.Sdk.EntityReference> の ID プロパティに設定されます。  
  
-   キーの属性が提供されている場合、提供された属性のセットと <xref:Microsoft.Xrm.Sdk.Entity> に対して定義されているキーとの照合が試みられます。  一致が見つからない場合は、エラーがスローされます。  一致が検出された場合は、これらの属性に対して提供された値の有効性が確認されます。 有効な場合は、提供されたキー値に一致したレコードの ID が取得され、<xref:Microsoft.Xrm.Sdk.Entity> または <xref:Microsoft.Xrm.Sdk.EntityReference> の ID 値にこの値が設定されます。  
  
-   一意のキーとして定義されていない属性セットを指定する場合は、一意のキー属性の使用が必要であることを示すエラーがスローされます。  
  
### <a name="see-also"></a>関連項目  
 [エンティティの代替キーの定義](define-alternate-keys-entity.md)   
 [変更の追跡を使用してデータを外部システムに同期](use-change-tracking-synchronize-data-external-systems.md)   
 [Upsert を使用してレコードを挿入または更新](use-upsert-insert-update-record.md)
