---
title: 'サンプル: ユーザー定義ワークフロー活動を使用した次回の誕生日の更新 (Common Data Service) | Microsoft Docs'
description: 'サンプル ワークフロー活動は次回の誕生日を返します。 顧客に誕生日の挨拶を送信するワークフローでこれを使用します。 '
ms.custom: ''
ms.date: 12/03/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: samples
applies_to:
  - Dynamics 365 (online)
ms.assetid: 1cff83b0-1f7b-4ddb-a2af-b85f9f785529
caps.latest.revision: 21
author: JimDaly
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-update-next-birthday-using-a-custom-workflow-activity"></a>サンプル: ユーザー定義ワークフロー活動を使用した次回の誕生日の更新

ここからサンプル全体をダウンロードします [カスタム ワークフロー活動のサンプル](https://code.msdn.microsoft.com/Custom-Workflow-Activities-eee57285)。 

## <a name="prerequisites"></a>前提条件

[!INCLUDE [sdk-prerequisite](../../../includes/sdk-prerequisite.md)]
  
## <a name="requirements"></a>要件 
 
このユーザー定義のワークフロー活動が機能するためには、次のカスタム フィールドが存在している必要があります。  
  
-   `Contact`.`new_nextbirthday`  
  
## <a name="demonstrates"></a>説明  
 次のサンプル ワークフロー活動は次回の誕生日を返します。 顧客に誕生日の挨拶を送信するワークフローでこれを使用します。  
  
## <a name="example"></a>例  

```csharp
using System;
using System.Activities;
using System.Collections;
using System.Reflection;

using Microsoft.Xrm.Sdk;
using Microsoft.Xrm.Sdk.Messages;
using Microsoft.Xrm.Sdk.Query;
using Microsoft.Xrm.Sdk.Workflow;

namespace Microsoft.Crm.Sdk.Samples
{
    /// <summary>
    /// Activity will return the next upcoming birthday that has just passed
    /// 
    /// If this year's birthday has not yet occurred, it will return this year's birthday
    /// Otherwise, it will return the birthday for next year
    /// 
    /// A workflow can timeout when on this date
    /// </summary>
    [Persist]
    public sealed partial class ReleaseScenario_UpdateNextBirthday : CodeActivity
    {
        protected override void Execute(CodeActivityContext executionContext)
        {
            IWorkflowContext context = executionContext.GetExtension<IWorkflowContext>();

            //Create an Organization Service
            IOrganizationServiceFactory serviceFactory = executionContext.GetExtension<IOrganizationServiceFactory>();
            IOrganizationService service = serviceFactory.CreateOrganizationService(context.InitiatingUserId);

            //Retrieve the contact id
            Guid contactId = this.Contact.Get(executionContext).Id;

            //Create the request
            RetrieveRequest request = new RetrieveRequest();
            request.ColumnSet = new ColumnSet(new string[] { "birthdate" });
            request.Target = new EntityReference(EntityName.Contact, contactId);

            //Retrieve the entity to determine what the birthdate is set at
            Entity entity = (Entity)((RetrieveResponse)service.Execute(request)).Entity;

            //Extract the date out of the entity
            DateTime? birthdate;
            if (entity.Contains(ContactAttributes.Birthdate))
            {
                birthdate = (DateTime?)entity[ContactAttributes.Birthdate];
            }
            else
            {
                birthdate = null;
            }

            //Check to see if the current birthday is set. We don't want the activity to fail if the birthdate is not set
            if (birthdate == null)
            {
                return;
            }

            //Calculate the next birthdate. Encapsulated in a methdo so that the method can be used in the test case for verification purposes
            DateTime nextBirthdate = CalculateNextBirthday(birthdate.Value);

            //Update the next birthday field on the entity
            Entity updateEntity = new Entity(EntityName.Contact);
            updateEntity.Id = contactId;
            updateEntity["new_nextbirthday"] = nextBirthdate;

            service.Update(updateEntity);
        }

        //Define the properties
        [RequiredArgument]
        [Input("Update Next Birthdate for")]
        [ReferenceTarget("contact")]
        public InArgument<EntityReference> Contact { get; set; }

        private DateTime CalculateNextBirthday(DateTime birthdate)
        {
            DateTime nextBirthday = new DateTime(birthdate.Year, birthdate.Month, birthdate.Day);

            //Check to see if this birthday occurred on a leap year
            bool leapYearAdjust = false;
            if (nextBirthday.Month == 2 && nextBirthday.Day == 29)
            {
                //Sanity check, was that year a leap year
                if (DateTime.IsLeapYear(nextBirthday.Year))
                {
                    //Check to see if the current year is a leap year
                    if (!DateTime.IsLeapYear(DateTime.Now.Year))
                    {
                        //Push the date to March 1st so that the date arithmetic will function correctly
                        nextBirthday = nextBirthday.AddDays(1);
                        leapYearAdjust = true;
                    }
                }
                else
                {
                    throw new Exception("Invalid Birthdate specified", new ArgumentException("Birthdate"));
                }
            }

            //Calculate the year difference
            nextBirthday = nextBirthday.AddYears(DateTime.Now.Year - nextBirthday.Year);

            //Check to see if the date was adjusted
            if (leapYearAdjust && DateTime.IsLeapYear(nextBirthday.Year))
            {
                nextBirthday = nextBirthday.AddDays(-1);
            }

            return nextBirthday;
        }
    }
}
```
  
### <a name="see-also"></a>関連項目

[ワークフローの拡張機能](workflow-extensions.md)<br />
[チュートリアル: ワークフロー拡張の作成](tutorial-create-workflow-extension.md)<br />
[サンプル: カスタム ワークフロー活動の作成](sample-create-custom-workflow-activity.md)<br />
[サンプル: ユーザー定義ワークフロー活動でクレジット スコアを計算する](sample-calculate-credit-score-custom-workflow-activity.md)
