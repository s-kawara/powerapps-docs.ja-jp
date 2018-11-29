---
title: モデル駆動型アプリの getEntityMetadata (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 89123cde-7c66-4c7d-94e4-e287285019f8
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getentitymetadata"></a>getEntityMetadata



[!INCLUDE[./includes/getEntityMetadata-description.md](./includes/getEntityMetadata-description.md)] 

## <a name="syntax"></a>構文

`Xrm.Utility.getEntityMetadata(entityName,attributes).then(successCallback, errorCallback)`

## <a name="parameters"></a>パラメーター

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|entityName|String|あり|エンティティの論理名。|
|属性|文字列の配列|いいえ|メタデータを取得する属性。|
|successCallback|関数|いいえ|エンティティ メタデータが返される場合に呼び出す関数。|
|errorCallback|関数|いいえ|処理が失敗したときに呼び出す関数。|

## <a name="returns"></a>戻り値

**種類**: オブジェクト

**説明**: 次の属性を含むエンティティ メタデータ情報を含むオブジェクト。

<table>
<tr>
<th>属性名</th>
<th>種類</th>
<th>説明</th>
</tr>
<tr>
<td>ActivityTypeMask</td>
<td>数値</td>
<td>カスタム活動をWeb アプリケーションの活動メニューに表示するかどうか。 0はユーザー定義の活動が表示されないことを示し、1は表示されることを示します。</td>
</tr>
<tr>
<td>AutoRouteToOwnerQueue</td>
<td>Boolean</td>
<td>この種類のレコードの作成または割り当て時に所有者の既定のキューにレコードを自動的に移動するかどうかを指定します。 </td>
</tr>

<tr>
<td>CanEnableSyncToExternalSearchIndex</td>
<td>Boolean</td>
<td>内部のみで使用。</td>
</tr>
<tr>
<td>CanTriggerWorkflow</td>
<td>Boolean</td>
<td>エンティティがワークフロー プロセスをトリガーできるかどうかを指定します。</td>
</tr>
<tr>
<td>説明</td>
<td>String</td>
<td>エンティティの説明。</td>
</tr>
<tr>
<td>DisplayCollectionName</td>
<td>String</td>
<td>エンティティの複数形での表示名。</td>
</tr>
<tr>
<td>DisplayName</td>
<td>String</td>
<td>エンティティの表示名。</td>
</tr>
<tr>
<td>EnforceStateTransitions</td>
<td>Boolean</td>
<td>エンティティがユーザー定義の状態の遷移を強制するかどうかを指定します。</td>
</tr>
<tr>
<td>EntityColor</td>
<td>String</td>
<td>アプリケーションでこのエンティティに使用する色を表す16進数コード。</td>
</tr>
<tr>
<td>EntitySetName</td>
<td>String</td>
<td>このエンティティのWeb APIエンティティ セットの名前。</td>
</tr>
<tr>
<td>HasActivities</td>
<td>Boolean</td>
<td>活動がこのエンティティと関連付けられるかどうかを指定します。</td>
</tr>
<tr>
<td>IsActivity</td>
<td>Boolean</td>
<td>エンティティが活動かどうかを示します。</td>
</tr>
<tr>
<td>IsActivityParty</td>
<td>Boolean</td>
<td>電子メール メッセージがこの種類のレコードに保存されている電子メール アドレスに送信できるかどうかを指定します。</td>
</tr>
<tr>
<td>IsBusinessProcessEnabled</td>
<td>Boolean</td>
<td>エンティティが業務プロセス フローに対して有効になっているかどうかを示します。</td>
</tr>
<tr>
<td>IsBPFEntity</td>
<td>Boolean</td>
<td>エンティティが業務プロセス フロー エンティティかどうかを示します。</td>
</tr>
<tr>
<td>IsChildEntity</td>
<td>Boolean</td>
<td>エンティティが子エンティティかどうかを示します。</td>
</tr>
<tr>
<td>IsConnectionsEnabled</td>
<td>Boolean</td>
<td>接続がこのエンティティに対して有効になっているかどうかを示します。</td>
</tr>
<tr>
<td>IsCustomEntity</td>
<td>Boolean</td>
<td>エンティティがユーザー定義エンティティかどうかを示します。</td>
</tr>
<tr>
<td>IsCustomizable</td>
<td>Boolean</td>
<td>エンティティがカスタマイズ可能かどうかを示します。</td>
</tr>
<tr>
<td>IsDocumentManagementEnabled</td>
<td>Boolean</td>
<td>ドキュメント管理が有効かどうかを示します。</td>
</tr>
<tr>
<td>IsDocumentRecommendationsEnabled</td>
<td>Boolean</td>
<td>ドキュメント レコメンデーションが有効かどうかを示します。</td>
</tr>
<tr>
<td>IsDuplicateDetectionEnabled</td>
<td>Boolean</td>
<td>重複データ検出が有効かどうかを示します。</td>
</tr>
<tr>
<td>IsEnabledForCharts</td>
<td>Boolean</td>
<td>グラフが有効かどうかを示します。</td>
</tr>
<tr>
<td>IsImportable</td>
<td>Boolean</td>
<td>エンティティがインポート ウィザードを使用してインポートできるかどうかを示します。</td>
</tr>
<tr>
<td>IsInteractionCentricEnabled</td>
<td>Boolean</td>
<td>エンティティが対話型エクスペリエンスに対して有効化されていることを示します。</td>
</tr>
<tr>
<td>IsKnowledgeManagementEnabled</td>
<td>Boolean</td>
<td>ナレッジ マネージメントがエンティティに対して有効になっているかどうかを示します。</td>
</tr>
<tr>
<td>IsMailMergeEnabled</td>
<td>Boolean</td>
<td>差し込み印刷がこのエンティティに対して有効になっているかどうかを示します。</td>
</tr>
<tr>
<td>IsManaged</td>
<td>Boolean</td>
<td>エンティティが管理ソリューションの一部であるかどうかを示します。</td>
</tr>
<tr>
<td>IsOneNoteIntegrationEnabled</td>
<td>Boolean</td>
<td>OneNote 統合がエンティティに対して有効になっているかどうかを示します。</td>
</tr>
<tr>
<td>IsOptimisticConcurrencyEnabled</td>
<td>Boolean</td>
<td>オプティミスティック同時実行がエンティティに対して有効になっているかどうかを示します。</td>
</tr>
<tr>
<td>IsQuickCreateEnabled</td>
<td>Boolean</td>
<td>エンティティが簡易作成フォームに対して有効になっているかどうかを示します。</td>
</tr>
<tr>
<td>IsStateModelAware</td>
<td>Boolean</td>
<td>エンティティがユーザー定義の状態の遷移の設定をサポートするかどうかを指定します。</td>
</tr>
<tr>
<td>IsValidForAdvancedFind</td>
<td>Boolean</td>
<td>エンティティが高度な検索で表示されるかどうかを指定します。</td>
</tr>
<tr>
<td>IsVisibleInMobileClient</td>
<td>Boolean</td>
<td>タブレット ユーザーのMicrosoft Dynamics 365がこのエンティティのデータを表示できるかどうかを指定します。</td>
</tr>
<tr>
<td>IsEnabledInUnifiedInterface</td>
<td>Boolean</td>
<td>エンティティが統一インターフェイス対して有効になっているかどうかを示します。</td>
</tr>
<tr>
<td>LogicalCollectionName</td>
<td>String</td>
<td>論理的なコレクション名。</td>
</tr>
<tr>
<td>LogicalName</td>
<td>String</td>
<td>エンティティの論理名。</td>
</tr>
<tr>
<td>ObjectTypeCode</td>
<td>数値</td>
<td>エンティティの種類コード。</td>
</tr>
<tr>
<td>OwnershipType</td>
<td>String</td>
<td>エンティティの所有権の種類:「UserOwned」または「OrganizationOwned」。</td>
</tr>
<tr>
<td>PrimaryIdAttribute</td>
<td>String</td>
<td>エンティティの主IDの属性の名前。</td>
</tr>
<tr>
<td>PrimaryImageAttribute</td>
<td>String</td>
<td>エンティティの主イメージ属性の名前。</td>
</tr>
<tr>
<td>PrimaryNameAttribute</td>
<td>String</td>
<td>エンティティの主属性の名前。</td>
</tr>
<tr>
<td>特権</td>
<td>オブジェクトの配列</td>
<td>*それぞれの*オブジェクトがエンティティへのアクセスのセキュリティ特権を定義する以下の属性を含むエンティティの特権メタデータ:
<ul>
<li><b>CanBeBasic</b>: ブール値。 特権はベーシックなアクセス レベルであり得るかどうか。</li>
<li><b>CanBeDeep</b>: ブール値。 特権はディープなアクセス レベルであり得るかどうか。</li>
<li><b>CanBeEntityReference</b>: ブール値。 外部パーティの特権がベーシックなアクセス レベルによって生成され得るかどうか。</li>
<li><b>CanBeGlobal</b>: ブール値。 特権がグローバルなアクセス レベルであり得るかどうか。</li>
<li><b>CanBeLocal</b>: ブール値。 特権がローカルなアクセス レベルであり得るかどうか。</li>
<li><b>CanBeParentEntityReference</b>: ブール値。 外部パーティの特権が上位アクセス レベルによって生成され得るかどうか。</li>
<li><b>Name</b>: 文字列。 特権の名前。</li>
<li><b>PrivilegeId</b>: 文字列。 特権のID。</li>
<li><b>PrivilegeType</b>: 番号。 特権の種類で、次のいずれかである:</li>
<ul>
<li>0: なし</li>
<li>1: 作成</li>
<li>2: 読み取り</li>
<li>3: 書き込み</li>
<li>4: 削除</li>
<li>5: 割り当て</li>
<li>6: 共有</li>
<li>7: 追加</li>
<li>8: 追加先</li>
</ul>
</ul></td>
</tr>
<tr>
<td>属性</td>
<td>集荷</td>
<td>属性のメタデータ オブジェクトの収集。 返されるオブジェクトは属性メタデータの種類によって異なります。
<p><b><i>ベース</i>の種類</b>の属性のメタデータ<br/>
次のプロパティを持つオブジェクト返されます:</p>
<ul>
<li><b>AttributeType</b>: 番号。 属性の種類。 属性の種類の値の一覧については、<a href="https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.metadata.attributetypecode">AttributeTypeCode</a>を参照してください。</li>
<li><b>DisplayName</b>: 文字列。 属性の表示名。</li>
<li><b>EntityLogicalName</b>: 文字列。 属性を含むエンティティの論理名。</li>
<li><b>LogicalName</b>: 文字列。 属性の論理名。</li></ul>

<p><b><i>ブール値</i>の種類</b>の属性のメタデータ<br/>
<i>ベース</i>属性メタデータの種類のプロパティに加えて、次のプロパティとともに返されるオブジェクト:</p>
<ul>
<li><b>DefaultFormValue</b>: ブール値。 ブール値オプション セットの既定値。</li>
<li><b>OptionSet</b>: オブジェクト。 各オプションがキーであるブール値属性のオプション: 値のペア。</li></ul>

<p><b><i>列挙</i>の種類</b>の属性のメタデータ<br/>
<i>ベース</i>属性メタデータの種類のプロパティに加えて、次のプロパティとともに返されるオブジェクト:</p>
<ul>
<li><b>OptionSet</b>: オブジェクト。 各オプションがキーである属性のオプション: 値のペア。</li></ul>

<p><b><i>候補リスト</i>の種類</b>の属性のメタデータ<br/>
<i>ベース</i>属性メタデータの種類のプロパティに加えて、次のプロパティとともに返されるオブジェクト:</p>
<ul>
<li><b>DefaultFormValue</b>: 番号。 属性の既定のフォーム値。</li>
<li><b>OptionSet</b>: オブジェクト。 各オプションがキーである属性のオプション: 値のペア。</li></ul>

<p><b><i>状態</i>の種類</b>の属性のメタデータ<br/>
<i>ベース</i>属性メタデータの種類のプロパティに加えて、次のプロパティとともに返されるオブジェクト:</p>
<ul>
<li><b>OptionSet</b>: オブジェクト。 各オプションがキーである属性のオプション: 値のペア。</li></ul>
<p>オブジェクトには、次のメソッドも含まれています:</p>
<ul>
<li><b>getDefaultStatus(arg) </b>: エンティティの状態値で渡されるもの基づいて既定のステータス(数値)を返します。 エンティティの既定の状態およびステータス値については、<a href="https://docs.microsoft.com/powerapps/developer/common-data-service/reference/about-entity-reference">エンティティ参照</a>のエンティティのエンティティ メタデータ情報を参照してください。</li>
<li><b>getStatusValuesForState(arg)</b>: 指定された状態値の可能な状態値 (数値の配列) を返します。 エンティティの状態およびステータス値については、<a href="https://docs.microsoft.com/powerapps/developer/common-data-service/reference/about-entity-reference">エンティティ参照</a>のエンティティのエンティティ メタデータ情報を参照してください。</li></ul>

<p><b><i>状態</i>の種類</b>の属性のメタデータ<br/>
<i>ベース</i>属性メタデータの種類のプロパティに加えて、次のプロパティとともに返されるオブジェクト:</p>
<ul>
<li><b>OptionSet</b>: オブジェクト。 各オプションがキーである属性のオプション: 値のペア。</li></ul>
<p>オブジェクトには、次のメソッドも含まれています:</p>
<ul>
<li><b>getState(arg)</b>: 指定された状態値 (数値) の状態値 (数値) を返します。 エンティティの既定の状態およびステータス値については、<a href="https://docs.microsoft.com/powerapps/developer/common-data-service/reference/about-entity-reference">エンティティ参照</a>のエンティティのエンティティ メタデータ情報を参照してください。</li>
</ul>
</td>
</tr>
</table>

### <a name="related-topics"></a>関連トピック

[Xrm.Utility](../xrm-utility.md)

