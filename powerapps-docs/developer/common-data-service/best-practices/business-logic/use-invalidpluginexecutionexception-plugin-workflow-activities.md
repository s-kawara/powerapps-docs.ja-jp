---
title: プラグインおよびワークフロー活動で InvalidPluginExecutionException を使用する | MicrosoftDocs
description: エラーをプラグインまたはワークフロー活動で上げる場合は InvalidPluginExecutionException を使用します。
services: ''
suite: powerapps
documentationcenter: na
author: jowells
manager: austinj
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 1/15/2019
ms.author: jowells
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-invalidpluginexecutionexception-in-plug-ins-and-workflow-activities"></a>プラグインおよびワークフロー活動で InvalidPluginExecutionException を使用する

**カテゴリ**: 保守性、ユーザビリティ

**影響の可能性**: 中程度

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

同期プラグインがプラットフォームに <xref:Microsoft.Xrm.Sdk.InvalidPluginExecutionException> 以外の例外を返す場合、エラー ダイアログ ボックスが、スタック トレース付きの例外メッセージ <xref:System.Exception.Message> とともに表示されます。 これは、すでに発生している可能性のある不満を感じる状況で、好ましくないユーザー エクスペリエンスを提供します。

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

以下の理由から、プラグインは <xref:Microsoft.Xrm.Sdk.InvalidPluginExecutionException> のみをプラットフォームに返すことをお勧めします。

- ユーザーへわかりやすいメッセージを表示する
- イベント ログ / トレース ファイルの肥大化を回避する

他の型の未処理の例外は、実行時に予期しないエラーが発生した場合にのみ発生します。 以下は、有効な方法の例です。

- 保護されていない InvalidPluginExecutionException をスローする

    ```csharp
    public void Execute(IServiceProvider serviceProvider)
    {
        // Invocation of a valid scenario that throws an appropriate exception type
        ThrowPluginException();
    }
    
    private void ThrowPluginException()
    {
        throw new InvalidPluginExecutionException("Throwing a plug-in exception in a member method body");
    }
    ```

- 保護された例外が、新しい InvalidPluginExecutionException として処理またはスローします

    ```csharp
    public void Execute(IServiceProvider serviceProvider)
    {
        try
        {
            ThrowGuardedMemberException();
        }
        catch (CustomException ex)
        {
            throw new InvalidPluginExecutionException("Unable to save the contact. This is likely caused by..."), ex);
        }
    
        // Invocation of a valid scenario in a member method
        HandleMemberException();
    }
    
    private void HandleMemberException()
    {
        try
        {
            // Invocation of a scenario where CustomException is thrown
            ThrowGuardedMemberException();
        }
        catch (CustomException ex)
        {
            // Handle the exception.
            // Note - Debug.WriteLine is likely not the appropriate way to handle the exception. This is for demonstration purposes only
            Debug.WriteLine(ex.Message);
        }
    }
    
    private void ThrowGuardedMemberException()
    {
        throw new CustomException("Throwing a custom exception in a guarded member");
    }
    ```

<a name='problem'></a>

## <a name="problematic-patterns"></a>問題となるパターン

> [!WARNING]
> これらのパターンは、回避する必要があります。

- 保護されていない例外がスローされています

    ```csharp
    public void Execute(IServiceProvider serviceProvider)
    {
        // Invocation of a scenario where violation occurs during an unguarded throw
        UnguardedMemberThrowException();
    }
    
    private void UnguardedMemberThrowException()
    {
        throw new CustomException("Throwing an unguarded custom exception in a member method body");
    }
    ```

- 保護されていない再スローを伴う、保護された例外がスローされています

    ```csharp
    public void Execute(IServiceProvider serviceProvider)
    {
        // Invocation of a scenario where violation occurs during an unguarded rethrow
        UnguardedMemberRethrowException();
    }
    
    private void UnguardedMemberRethrowException()
    {
        try
        {
            // Guarded invoking of a method member that throws a custom exception
            GuardedMemberThrowException();
        }
        catch (CustomException ex)
        {
            // Handle and rethrow
            Debug.WriteLine(ex.Message);
    
            // This is where the issue occurs
            throw;
        }
    }
    
    private void GuardedMemberThrowException()
    {
        throw new CustomException("Throwing a guarded custom exception in a member method body");
    }
    ```

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

[操作のキャンセル](../../handle-exceptions.md#cancelling-an-operation)<br/>
[ワークフロー活動のデバッグ](../../workflow/workflow-extensions.md#debug-workflow-activities)<br/>