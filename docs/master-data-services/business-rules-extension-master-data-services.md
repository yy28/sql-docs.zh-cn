---
title: "业务规则扩展 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4c18be5f-a3fa-45a8-9be6-0f45f58bbc9e
caps.latest.revision: "16"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a4eea06466e59b0ddb8344dbba5b7d81bf1e97b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="business-rules-extension-master-data-services"></a>业务规则扩展 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，可以将用户定义的 SQL 脚本作为预定义条件和操作的扩展进行应用。  
  
> [!NOTE]  
>  所有脚本都必须在 [usr] 架构下定义。  
  
 满足以下条件的 SQL 函数可以用作业务规则条件。  
  
-   返回值类型必须为 BIT。  
  
-   参数类型仅支持以下类型。  
  
    -   NVARCHAR  
  
    -   DATETIME2  
  
    -   DECIMAL（精度、小数位数）  
  
         精度必须为 38  
  
         小数位数的取值范围必须为 0 到 7  
  
 使用以下语法的 SQL 存储过程可用作业务规则操作  
  
```  
CREATE PROCEDURE [usr].[YourAction]  
       (         
            @MemberIdList mdm.[MemberId] READONLY,  
            @ModelName NVARCHAR(MAX),  
            @VersionName NVARCHAR(MAX),  
            @EntityName NVARCHAR(MAX),  
            @BusinessRuleName NVARCHAR(MAX)  
        )    
      AS BEGIN    
       ...     
       END  
  
```  
  
 用户定义脚本不会添加到部署包中。 请确保在部署包之前，目标 Master Data Services 数据库包含业务规则中所用的所有脚本。  
  
 脚本操作将以具有以下权限的 mds_br_user 身份执行  
  
|||  
|-|-|  
|**架构**|**Permissions**|  
|mdm|SELECT|  
|stg|SELECT、UPDATE、DELETE、EXECUTE、INSERT|  
|usr|FULL|  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   你必须有权访问“系统管理”功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
-   用户定义脚本已添加到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。  
  
## <a name="create-a-business-rule-to-take-a-user-defined-script-as-a-condition-or-as-an-action"></a>创建业务规则，以将用户定义脚本用作条件或操作  
  
1.  在主数据管理器中，单击“系统管理” 。  
  
2.  在菜单栏中，指向“管理”  ，然后单击“业务规则” 。  
  
3.  在“业务规则”页上，从“模型”下拉列表中选择某一模型。  
  
4.  从“实体”下拉列表中选择一个实体。  
  
5.  从“成员类型”  下拉列表中，选择要应用业务规则的成员类型。  
  
6.  单击 **“添加”**。  
  
7.  执行以下操作以将用户定义脚本创建为条件。  
  
    1.  在“If”  块下，单击“添加”按钮  。 此时，系统会显示一个面板。  
  
    2.  从“运算符”下拉列表中，选择“用户定义脚本”下的用户定义函数。  
  
    3.  将显示用户定义函数的所有参数。  
  
    4.  向每个参数赋值  
  
    5.  单击 **“保存”**。  
  
8.  执行以下操作以将用户定义脚本用作操作。  
  
    1.  在“Then”  块下，单击“添加”按钮  。 此时，系统会显示一个面板。  
  
    2.  从“运算符”下拉列表中，选择“用户定义脚本”下的用户定义函数。  
  
    3.  单击 **“保存”**。  
  
## <a name="see-also"></a>另请参阅  
 [业务规则 (Master Data Services)](../master-data-services/business-rules-master-data-services.md)   
 [业务规则条件 (Master Data Services)](../master-data-services/business-rule-conditions-master-data-services.md)   
 [业务规则操作 (Master Data Services)](../master-data-services/business-rule-actions-master-data-services.md)  
  
  
