---
title: 計算およびロールアップ属性 (Common Data Service) | Microsoft Docs
description: 一般的な要素および特性、計算属性、ロールアップ属性、計算されたロールアップ フィールド値、計算されたロールアップ フィールド値をすばやく取得する方法、SourceTypeMasks列挙体について説明します。
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
# <a name="calculated-and-rollup-attributes"></a>計算およびロールアップ属性

*計算*および*ロールアップ*属性を使用すると、手動で計算を実行する必要がなくなるので、作業に集中できます。 システム管理者は、開発者と協力しないで、多くの共通計算の値を含むフィールドを定義できるようになりました。 開発者も、自分のコード内ではなく、プラットフォーム機能を活用してこれらの計算を実行できます。  
  
 [ビデオ: Microsoft Dynamics CRM 2015 のロールアップ フィールドと計算フィールド](http://youtu.be/RoahCH1p3T8)  
  
<a name="BKMK_CommonElements"></a>   
## <a name="common-elements-and-characteristics"></a>共通の要素と特性  
 計算属性とロールアップ属性には、次のような共通の要素と特性があります。  
  
- 読み取り専用です。  
  
- ユーザー固有ではありません。 計算はシステム ユーザー アカウントを使用して実行されるため、その値は、フィールド レベルのセキュリティが有効な属性など、ユーザーが表示する特権を持たないレコードに基づく場合があります。  
  
  <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata> から継承するすべての属性には、次の表に示されている値を含む <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.SourceType> プロパティがあります。  
  
|                 Value                 |                                    説明                                     |
|---------------------------------------|------------------------------------------------------------------------------------|
| Null |       計算またはロールアップ属性となるには、無効な属性の種類です。        |
|                   0                   | 単純な属性です。 この属性は、計算またはロールアップ属性として定義されていません。 |
|                   1                   |                                計算属性                                |
|                   2                   |                                  ロールアップ属性                                  |
  
 計算属性とロールアップ属性は、<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata> から継承される既存の属性の種類に基づいています。 次の種類の属性には、新しいプロパティがあります。  
  
- <xref:Microsoft.Xrm.Sdk.Metadata.BooleanAttributeMetadata>  
  
- <xref:Microsoft.Xrm.Sdk.Metadata.DateTimeAttributeMetadata>  
  
- <xref:Microsoft.Xrm.Sdk.Metadata.DecimalAttributeMetadata>  
  
- <xref:Microsoft.Xrm.Sdk.Metadata.IntegerAttributeMetadata>  
  
- <xref:Microsoft.Xrm.Sdk.Metadata.MoneyAttributeMetadata>  
  
- <xref:Microsoft.Xrm.Sdk.Metadata.PicklistAttributeMetadata>  
  
- <xref:Microsoft.Xrm.Sdk.Metadata.StringAttributeMetadata>  
  
  これらの種類の属性には、それぞれ計算とロールアップをサポートする以下のプロパティがあります。  
  
|      プロパティ       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        定義                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `FormulaDefinition` |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   計算やロールアップの実行時に使用される数式の XAML 定義が含まれます。 この値を変更できる唯一の方法は、アプリケーション数式エディターを使用する方法です。<br /><br /> これらの属性の数式を構成する方法については、『カスタマイズ ガイド』のトピック「[ロールアップ フィールドの定義](https://technet.microsoft.com/library/dn832162.aspx)」と「[計算フィールドの定義](https://technet.microsoft.com/library/dn832103.aspx)」を参照してください。                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|  `SourceTypeMask`   | この読み取り専用プロパティのビットマスク値は、計算属性の数式で使用されるソースの種類を記述するか、計算属性またはロールアップ属性の数式が無効かどうかを示します。<br /><br /> -   0: **未定義**。 単純な属性およびロールアップ属性の既定値です。<br />-   1: **単純**。 計算属性は、同じレコードの属性を参照します。<br />-   2: **関連**。 計算属性は、関連レコードの属性を参照します。<br />-   4: `Logical`。 計算属性は、同じレコードにあるものの、実際には異なるデータベース テーブルに格納されている属性を参照します。 詳細: [論理的属性](/dynamics365/customer-engagement/developer/introduction-to-entity-attributes#BKMK_LogicalAttributes)<br />-   8: `Calculated`。 計算属性は、別の計算属性を参照します。<br />-   16: `Rollup`。 計算属性は、ロールアップ属性を参照します。<br />-   32: `Invalid`。 計算またはロールアップ フィールドが無効です。<br />     通常は、フィールドの参照する属性が存在しない場合です。 **注意:** これらの条件の 1 つ以上が計算またはロールアップ フィールドにあてはまる場合があります。 これはビットマスク値であるため、ビットごとの操作を実行する際には [SourceTypeMasks 列挙体](calculated-rollup-attributes.md#BKMK_SourceTypeMasks) を使用すると便利な場合があります。 |
  
<a name="BKMK_Calculated"></a>   
## <a name="calculated-attributes"></a>計算属性  
 計算属性は、取得時にリアルタイムに計算されます。 計算属性は、異なるデータの種類を使用して構成できます。 たとえば、整数の計算属性は、小数または通貨属性から値を参照できます。 詳細: [計算フィールドの定義](https://technet.microsoft.com/library/dn832103.aspx)。  
  
 計算属性の値は、取得プラグイン パイプラインで使用できます。 エンティティ レコードの更新または作成のポスト イメージには、ステージ 40 の計算属性値が含まれます。 詳細: [イベント実行パイプライン](event-framework.md#event-execution-pipeline) と [エンティティ イメージ](understand-the-data-context.md#entity-images)
  
### <a name="limitations"></a>制限  
 関連エンティティ、別の計算属性、または同じエンティティの*論理値*を参照する計算属性の値を使用して、クエリによって返されるデータを並べ替えることはできません。 計算属性を使用して結果を並べ替えるようクエリで指定することはできますが、並べ替えの向きは無視され、エラーはスローされません。 計算属性が同じレコードの単純な値のみを参照する場合、並べ替えは正常に機能します。 計算フィールドで使用されているソースを確認するには、属性のメタデータに対して `SourceTypeMask` プロパティを使用します。 詳細: [論理的属性](/dynamics365/customer-engagement/developer/introduction-to-entity-attributes.md#BKMK_LogicalAttributes)  
  
 計算属性では、直接の親エンティティの属性のみを使用できます。  
  
 保存されたクエリ、グラフ、およびビジュアル化には、固有の計算属性を最大 10 まで含めることができます。  
  
 計算属性は、数式に含まれる他の計算属性を参照することはできますが、自分自身を参照することはできません。  
  
 Dynamics 365 for Outlook のユーザーがオフラインのとき、計算属性には値がありません。  
  
 `MaxValue` と `MinValue` メタデータ プロパティは、計算属性に対して設定できません。  
  
<a name="BKMK_Rollup"></a>   
## <a name="rollup-attributes"></a>ロールアップ属性  
 ロールアップ属性はデータベースで保持されるため、通常の属性と同じように、フィルタリングや並べ替えに使用できます。 どの種類のプロセスやプラグインも、最後に計算した属性の値を使用します。 ロールアップ属性値はスケジュールしたシステム ジョブで非同期に計算されます。 管理者がジョブを実行またはジョブを一時停止する時を設定します。 既定では、各属性は毎時間更新されます。 詳細: [ロールアップ フィールドの定義](https://technet.microsoft.com/library/dn832103.aspx)。  
  
 ロールアップ属性の作成または更新時に、**ロールアップ フィールドの一括計算**ジョブは 12 時間以内に実行するようにスケジュールされます。 12 時間の遅れは、リソースを大量に必要とするこの操作をユーザーに影響しない時に実行するのが目的です。 ジョブが完了すると、このジョブは、次回は約 10 年後に実行されるように自動的にスケジュールされます。 計算に問題がある場合は、システム ジョブとして報告されます。 **設定** > **システム ジョブ**にあるシステム ジョブで、ロールアップ フィールドでのエラーを探します。  
  
> [!TIP]
>  展開環境のソリューションをテストする開発者の中には、12 時間も待ちたくない開発者もいます。 もっと早く実行すことも可能です。 **システム ジョブ**一覧で**定期システム ジョブ**ビューを使用して、一覧をフィルター処理し、**ロールアップ フィールドの一括計算**ジョブを見つけます。 ジョブを選択して、**その他の操作** > **延期**を使用して、もっと早い時間に設定します。  
>   
>  新しい**ロールアップ フィールドの一括計算**ジョブのプログラムでの作成を起動するには、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveAttributeRequest>を使用してロールアップ属性の <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata> を取得し、<xref:Microsoft.Xrm.Sdk.Messages.UpdateAttributeRequest> を使用して、実際には何も変更せずに属性を更新します。  
  
 **ロールアップ フィールドの一括計算**ジョブは、ロールアップ属性を含むソリューションがインポートされるとすぐに実行されます。 これは、ユーザーに悪影響を与えない時間にソリューションをインストールすることが前提です。  
  
 エンティティの各ロールアップ属性には、ロールアップ属性に 2 つのサポートされている属性が含まれます。  
  
- *\<SchemaName 属性>* `_Date`: DateTime – ロールアップが最後に計算された時間。  
  
- *\<attribute SchemaName>* `_State`: Integer – ロールアップ計算の状態。 詳細: [ロールアップ状態値](calculated-rollup-attributes.md#BKMK_RollupStateValues)。  
  
<a name="BKMK_RollupStateValues"></a>   
### <a name="rollup-state-values"></a>ロールアップ状態値  
 ロールアップフィールド計算の状態は、対応する *\<attribute SchemaName>*`_State` 属性と <xref:Microsoft.Crm.Sdk.Messages.CalculateRollupFieldResponse>。`FieldState` プロパティで使用できます。 プロパティ。 状態を示す値を次の表に示します。  
  
|状態値|説明|  
|-----------------|-----------------|  
|0|`NotCalculated`: 属性値はまだ計算されていません。|  
|1|`Calculated`: 属性値は*\<attribute SchemaName>*`_Date`での最後の更新時ごとに計算されました。|  
|2|`OverflowError`: 属性数計算がオーバフロー エラーの原因になりました。|  
|3|`OtherError`: 属性値計算は、内部エラーが原因で発生しました。次回の計算ジョブ実行時にはたいてい修正されます。|  
|4|`RetryLimitExceeded`並行処理の多さと競合のロックが原因で、値の計算の再試行の最大数を超過し、属性値の計算に失敗しました。|  
|5|`HierarchicalRecursionLimitReached`: 最大限度の階層の深さに計算が到達したことが原因で、属性値の計算に失敗しました。|  
|6|`LoopDetected`レコードの階層で再帰的ループが検出されたことが原因で、属性値の計算に失敗しました。|  
  
### <a name="retrieve-a-calculated-rollup-field-value-immediately"></a>計算ロールアップ フィールドの値をすぐに取得する  
 ロールアップ属性は、オンデマンドでロールアップ属性値を計算するのに開発者が使用する`CalculateRollupField` メッセージをサポートします。 要求と応答をメンバーと共に、次の表に示します。  
  
|要求/応答|メンバー|  
|-----------------------|-------------|  
|<xref:Microsoft.Crm.Sdk.Messages.CalculateRollupFieldRequest>|`Target`: レコードの<xref:Microsoft.Xrm.Sdk.EntityReference>。<br /><br /> `FieldName`: 属性の論理名を表す文字列。|  
|<xref:Microsoft.Crm.Sdk.Messages.CalculateRollupFieldResponse>|`Entity`: ロールアップ属性とサポートしている *\<attribute SchemaName>*`_Date` と *\<attribute SchemaName>*`_State` 属性を含む<xref:Microsoft.Xrm.Sdk.Entity>。|  
  
 このメッセージは、要求で指定した属性のみの同期操作です。 このレコードの値が他ロールアップ フィールドの一部として含まれている場合、これらの計算を実行する定期的にスケジュールされた非同期ジョブが発生するまでこのメソッドを考慮するので、それらのフィールド値は可能な値変更を行いません。  
  
### <a name="limitations"></a>制限  
 ロールアップ属性はワークフロー イベントまたは待機状態として使用することはできません。 これらの属性はワークフローをトリガーするイベントを発生させません。  
  
 エンティティの ModifiedBy と ModifiedOn  属性は、ロールアップが更新されたときには、更新されません。  
  
 ロールアップ属性は最大 100 まで組織内で定義できます。 各エンティティには 10 未満のロールアップ属性を設定できます。  
  
 ロールアップ属性の式は、他のロールアップ属性を参照できません。  
  
 ロールアップ属性の式は、複雑に計算された属性を参照できません。 同じレコードの簡単な属性を参照する計算属性だけがロールアップで使用できます。  
  
 ロールアップ属性式には、多対多(N: N)の関連付けのレコードを含めることはできません。 一対多(1: N)の関連付けのレコードのみを含めることができます。  
  
 ロールアップ属性式は一対多(1:N)関連付けを`ActivityPointer` または `ActivityParty` エンティティで使用できません。  
  
<a name="BKMK_SourceTypeMasks"></a>   
## <a name="sourcetypemasks-enumeration"></a>SourceTypeMasks 列挙体  
 計算属性およびロールアップ フィールドをサポートするこれらの属性の`SourceTypeMask` プロパティは、ビットマスク値を含みます。 値から関連情報を取得するには、ビットごとの操作を実行する際に、列挙体があると便利です。 `SourceTypeMask` プロパティ値を比較する際は、次の`SourceTypeMasks`列挙体を使用します。  
  
```csharp  
 public enum SourceTypeMasks  
{  
    /// <summary>  
    /// Undefined: 0 - The default value for simple and rollup attributes.  
    /// </summary>  
    Undefined = 0,  
    /// <summary>  
    /// Simple: 1 - The calculated attribute refers to an attribute in the same record.  
    /// </summary>  
    Simple = 1,  
    /// <summary>  
    /// Related: 2 - The calculated attribute refers to an attribute in a related record.  
    /// </summary>  
    Related = 2,  
    /// <summary>  
    /// Logical: 4 - The calculated attribute refers to a logical attribute.  
    /// </summary>  
    Logical = 4,  
    /// <summary>  
    /// Calculated: 8 - The calculated attribute refers to another calculated attribute.  
    /// </summary>  
    Calculated = 8,  
    /// <summary>  
    /// Rollup: 16 - The calculated attribute refers a rollup attribute.   
    /// </summary>  
    Rollup = 16,  
    /// <summary>  
    /// Invalid: 32 - The calculated or rollup attribute is invalid.  
    /// Typically this would be where a field refers to an attribute that no longer exists.   
    /// </summary>  
    Invalid = 32  
}  
```  
  
### <a name="see-also"></a>関連項目  
 [ビデオ: Microsoft Dynamics CRM 2015 のロールアップ フィールドと計算フィールド](http://youtu.be/RoahCH1p3T8)   
 [エンティティ属性の概要](/dynamics365/customer-engagement/developer/introduction-to-entity-attributes)   
 [計算フィールドの定義](https://technet.microsoft.com/library/dn832103.aspx)   
 [ロールアップ フィールドを定義する](https://technet.microsoft.com/library/dn832103.aspx)
