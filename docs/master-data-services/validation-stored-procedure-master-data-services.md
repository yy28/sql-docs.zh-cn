---
title: 验证存储过程 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 332d3c86-4440-4f12-a6cb-ffbfbccde52c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 239cd199e97fffdb3254a3fb5817f3922d28b661
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621085"
---
# <a name="validation-stored-procedure-master-data-services"></a>验证存储过程 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，对某一版本进行验证以便将业务规则应用于该模型版本中的所有成员。  
  
 本主题说明如何使用 **mdm.udpValidateModel** 存储过程来验证数据。 如果您是 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序的管理员，可以在 UI 中进行验证。 有关详细信息，请参阅 [针对业务规则验证版本 (Master Data Services)](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)。  
  
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
  
|参数|描述|  
|---------------|-----------------|  
|UserID|用户 ID。|  
|Model_ID|模型 ID。|  
|Version_ID|版本 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [概述：导入表中数据 (Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [针对业务规则验证版本 (Master Data Services)](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
  
