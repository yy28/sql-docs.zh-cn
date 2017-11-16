---
title: "临时存储过程 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
caps.latest.revision: "15"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cdd2f68b97126999c61a79d78148440137d2cf8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="staging-stored-procedure-master-data-services"></a>临时存储过程 (Master Data Services)
  从 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]启动临时过程时，您使用三个存储过程之一。  
  
-   stg.udp_\<name>_Leaf  
  
-   stg.udp_\<name>_Consolidated  
  
-   stg.udp_\<name>_Relationship  
  
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
  
  
