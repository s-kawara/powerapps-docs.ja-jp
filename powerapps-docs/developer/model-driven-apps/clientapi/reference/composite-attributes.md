---
title: モデル駆動型アプリの複合属性 | Microsoft Docs
description: 属性値が変更されたときに呼び出される関数を設定するための、addOnchange メソッドについて説明します。
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9f3b2fed-fde5-46e4-8c59-43aa51aa82df
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="composite-attributes"></a>複合属性 



フォームに追加されるフィールドの一部は、データの複数のアイテムを表すことができます。 これらの*複合属性*は、Web アプリケーションで表示するときに、他の属性とは異なる動作をするため、それらを適切に使用するスクリプトを作成する必要があります。

次の表は、モデル駆動型アプリで利用可能な複合属性を示しています。

<table>
    <tbody>
        <tr>
            <th scope="col">
                <p>
エンティティ </p>
            </th>
            <th scope="col">
                <p>
[表示名] </p>
            </th>
            <th scope="col">
                <p>
論理名 </p>
            </th>
        </tr>
        <tr>
            <td rowspan="2">
                <p>
取引先企業 </p>
            </td>
            <td>
                <p>
                    <strong>住所 1</strong>
                </p>
            </td>
            <td>
                <p>
address1_composite </p>
            </td>
        </tr>
        <tr>
            <td>
                <p>
                    <strong>住所 2</strong>
                </p>
            </td>
            <td>
                <p>
address2_composite </p>
            </td>
        </tr>
        <tr>
            <td rowspan="3">
                <p>
取引先担当者  </p>
            </td>
            <td>
                <p>
                    <strong>氏名</strong>
                </p>
            </td>
            <td>
                <p>
fullname </p>
            </td>
        </tr>
        <tr>
            <td>
                <p>
                    <strong>住所 1</strong>
                </p>
            </td>
            <td>
                <p>
address1_composite </p>
            </td>
        </tr>
        <tr>
            <td>
                <p>
                    <strong>住所 2</strong>
                </p>
            </td>
            <td>
                <p>
address2_composite </p>
            </td>
        </tr>
        <tr>
            <td rowspan="3">
                <p>
潜在顧客 </p>
            </td>
            <td>
                <p>
                    <strong>氏名</strong>
                </p>
            </td>
            <td>
                <p>
fullname </p>
            </td>
        </tr>
        <tr>
            <td>
                <p>
                    <strong>住所 1</strong>
                </p>
            </td>
            <td>
                <p>
address1_composite </p>
            </td>
        </tr>
        <tr>
            <td>
                <p>
                    <strong>住所 2</strong>
                </p>
            </td>
            <td>
                <p>
address2_composite </p>
            </td>
        </tr>
        <tr>
            <td rowspan="3">
                <p>
ユーザー </p>
            </td>
            <td>
                <p>
                    <strong>氏名</strong>
                </p>
            </td>
            <td>
                <p>
fullname </p>
            </td>
        </tr>
        <tr>
            <td>
                <p>
                    <strong>住所</strong>
                </p>
            </td>
            <td>
                <p>
address1_composite </p>
            </td>
        </tr>
        <tr>
            <td>
                <p>
                    <strong>住所 (その他)</strong>
                </p>
            </td>
            <td>
                <p>
address2_composite </p>
            </td>
        </tr>        
        <tr>
            <td rowspan="2">
                <p>
見積もり  </p>
            </td>
            <td>
                <p>
                    <strong>請求先住所</strong>
                </p>
            </td>
            <td>
                <p>
billto_composite </p>
            </td>
        </tr>
        <tr>
            <td>
                <p>
                    <strong>送付先住所</strong>
                </p>
            </td>
            <td>
                <p>
shipto_composite </p>
            </td>
        </tr>
        <tr>
            <td rowspan="2">
                <p>
受注 </p>
            </td>
            <td>
                <p>
                    <strong>請求先住所</strong>
                </p>
            </td>
            <td>
                <p>
billto_composite </p>
            </td>
        </tr>
        <tr>
            <td>
                <p>
                    <strong>送付先住所</strong>
                </p>
            </td>
            <td>
                <p>
shipto_composite </p>
            </td>
        </tr>
        <tr>
            <td rowspan="2">
                <p>
請求書 </p>
            </td>
            <td>
                <p>
                    <strong>請求先住所</strong>
                </p>
            </td>
            <td>
                <p>
billto_composite </p>
            </td>
        </tr>
        <tr>
            <td>
                <p>
                    <strong>送付先住所</strong>
                </p>
            </td>
            <td>
                <p>
shipto_composite </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="composite-attributes-in-the-web-application"></a>Web アプリケーションの複合属性

複合属性のフィールドがメイン フォームに追加されると、Web アプリケーションは、複合属性のみを表示します。 ユーザーがフィールドを編集する場合は、複合属性を構成する個々の属性を示すポップアップが表示されます。 

たとえば、取引先担当者フォームの**アドレス**フィールドは複合属性です。 **アドレス**フィールドをクリックすると、複合属性を含む個々の属性を持つポップアップが表示されます。 

![複合属性の例](../../media/clientapi_compositeattribute.png)

属性を構成するそれぞれの属性は、フォーム エディターでは明示的にフォームに追加されませんが、フォームで使用できます。 [getValue](attributes/getValue.md)を使用して複合値の値を参照できますが、[setValue](attributes/setValue.md)  を使用して複合属性の値を直接変更できません。複合属性によって参照される属性を 1 つまたは複数設定する必要があります。

ポップアップに表示される個々の構成コントロールに名前でアクセスできます。 これらのコントロールは次の命名規則を使用します。\<**composite control name**>\_compositionLinkControl_\<**constituent attribute name**>。 

**address1_composite** コントロール内の **address_line1** コントロールのみにアクセスするには、以下を使用します。 

`formContext.getControl("address1_composite_compositionLinkControl_address1_line1")`

## <a name="composite-attributes-in-mobile-clients"></a>モバイル クライアント内の複合属性
モデル駆動型アプリのモバイル クライアントは、複合属性を持つエンティティで使用されている定義と同じフォーム定義を使用しますが、解釈方法が異なります。 複合属性がフォーム定義にある場合、複合属性を構成するすべての属性が、フォーム内のその部分に表示されます。 すべてのフィールドが表示されているため、ポップアップの必要はありません。 フォームに個々に属性を追加したときと同じように、個々の属性にアクセスするフォームのスクリプトを作成できます。
ただし、実際の複合コントロールは、モデル駆動型アプリのモバイル クライアント ページには存在しません。

## <a name="mitigate-the-differences"></a>違いの軽減

取引先担当者、潜在顧客、またはユーザー エンティティの氏名フィールドにアクセスする場合は、 **formContext.data.entity**.[getPrimaryAttributeValue](formContext-data-entity/getPrimaryAttributeValue.md) メソッドを使用することが、直接を参照せずにこの属性の値を取得する最も簡単な方法です。 このメソッドは、Web アプリケーションおよびモデル駆動型アプリ モバイル クライアントの両方で機能します。

アドレス複合属性の 1 つの値を読み取る必要のあるコードがある場合、両方のクライアントと連携するためには、**Xrm.Navigation**.[openAlertDialog](Xrm-Navigation/openAlertDialog.md) メソッドを使用してフォーマットされたアドレスをメインの Web アプリケーションまたは同じフォームのモバイル アプリ バージョンのいずれかに表示する次の関数のように、[getClient](Xrm-Utility/getGlobalContext/client.md#getclient) メソッドを使用してコードを分割する必要があります。

```JavaScript
function showAddressDialog(executionContext) {
    var address1_compositeValue;
    var formContext = executionContext.getFormContext();
    if (Xrm.Utility.getGlobalContext().client.getClient() != "Mobile") {
        address1_compositeValue = formContext.getAttribute("address1_composite").getValue();
    }
    else {
        var address1_line1 = formContext.getAttribute("address1_line1").getValue();
        var address1_line2 = formContext.getAttribute("address1_line2").getValue();
        var address1_line3 = formContext.getAttribute("address1_line3").getValue();
        var address1_city = formContext.getAttribute("address1_city").getValue();
        var address1_stateorprovince = formContext.getAttribute("address1_stateorprovince").getValue();
        var address1_postalcode = formContext.getAttribute("address1_postalcode").getValue();
        var address1_country = formContext.getAttribute("address1_country").getValue();

        // Achieve equivalent formatting
        //address1_line1
        //address1_line2
        //address1_line3
        //address1_city, address1_stateorprovince address1_postalcode
        //address1_country

        var addressText = "";
        if (address1_line1 != null) {
            addressText += address1_line1 + "\n";
        }
        if (address1_line2 != null) {
            addressText += address1_line2 + "\n";
        }
        if (address1_line3 != null) {
            addressText += address1_line3 + "\n";
        }
        if (address1_city != null) {
            addressText += address1_city + ", ";
        }
        if (address1_stateorprovince != null) {
            addressText += address1_stateorprovince + " ";
        }
        if (address1_postalcode != null) {
            addressText += address1_postalcode + "\n";
        }
        addressText += address1_country;

        address1_compositeValue = addressText;
    }
    Xrm.Navigation.openAlertDialog({ text: address1_compositeValue });
    console.log(address1_compositeValue);
}
```

### <a name="related-topics"></a>関連トピック
[属性](attributes.md)





