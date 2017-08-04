---
title: "临时存储的过程 (Master Data Services) |Microsoft 文档"
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
caps.latest.revision: 15
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c2c12151d25b7d563a8a37a7ccfd617bca5cb479
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="staging-stored-procedure-master-data-services"></a>临时存储过程 (Master Data Services)
  从 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]启动临时过程时，您使用三个存储过程之一。  
  
-   stg.udp_\<名称 > _Leaf  
  
-   stg.udp_\<名称 > _Consolidated  
  
-   stg.udp_\<名称 > _Relationship  
  
 其中 name 是创建实体时指定的临时表的名称。  
  
## <a name="staging-process-stored-procedure-parameters"></a>临时过程存储过程参数  
 下表列出了这些存储过程的参数。  
  
|参数|Description|  
|---------------|-----------------|  
|**VersionName**<br /><br /> 必需|版本的名称。 这可能区分大小写，也可能不区分，具体取决于您的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 排序规则设置。|  
|**LogFlag**<br /><br /> 必需|确定在临时过程中是否记录事务。 可能的值有：<br /><br /> **0**：不记录事务。<br /><br /> **1**：记录事务。<br /><br /> <br /><br /> 有关事务的详细信息，请参阅[事务 (Master Data Services)](../master-data-services/transactions-master-data-services.md)。|  
|**BatchTag**<br /><br /> 必需，但是 Web 服务除外|在临时表中指定 **BatchTag** 值。|  
|**Batch_ID**<br /><br /> 仅对 Web 服务为必需的|在临时表中指定的 **Batch_ID** 值。|  
|**用户名**|可选参数|  
|**用户 ID**|可选参数|  
  
### <a name="staging-process-stored-procedure-example"></a>临时过程存储过程示例  
 下面的示例说明了如何使用临时存储过程启动临时过程。  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
      @UserName=N’domain\user’  
  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [验证存储过程 (Master Data Services)](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [查看暂存过程中出现的错误 (Master Data Services)](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)  
  
  

