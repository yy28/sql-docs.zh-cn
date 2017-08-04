---
title: "验证存储过程 (Master Data Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 332d3c86-4440-4f12-a6cb-ffbfbccde52c
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4c0606a05973dfbcd8e43f24898c8a9ce01d9fc8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="validation-stored-procedure-master-data-services"></a>验证存储过程 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，对某一版本进行验证以便将业务规则应用于该模型版本中的所有成员。  
  
 本主题说明如何使用 **mdm.udpValidateModel** 存储过程来验证数据。 如果您是 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序的管理员，可以在 UI 中进行验证。 有关详细信息，请参阅[针对业务规则验证版本 (Master Data Services)](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)。  
  
> [!NOTE]  
>  如果在临时过程完成前调用验证，将不验证未完成暂存的成员。  
  
## <a name="example"></a>示例  
  
```  
DECLARE @ModelName nVarchar(50) = 'Customer'   
DECLARE @Model_id int   
DECLARE @UserName nvarchar(50)= 'DOMAIN\user_name'   
DECLARE @User_ID int   
DECLARE @Version_ID int   
  
SET @User_ID = (SELECT ID    
                 FROM mdm.tblUser u   
                 WHERE u.UserName = @UserName)   
SET @Model_ID = (SELECT Top 1 Model_ID   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_Name = @ModelName)   
SET @Version_ID = (SELECT MAX(ID)   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_ID = @Model_ID)  
  
EXECUTE mdm.udpValidateModel @User_ID, @Model_ID, @Version_ID, 1  
  
```  
  
## <a name="parameters"></a>Parameters  
 此过程的参数如下所示：  
  
|参数|Description|  
|---------------|-----------------|  
|UserID|用户 ID。|  
|Model_ID|模型 ID。|  
|Version_ID|版本 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [概述：导入表中数据 (Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [针对业务规则 &#40; 验证版本Master Data Services &#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
  
