---
title: 临时存储过程
description: 使用三个存储过程之一，从 Master Data Services 中的 SQL Server Management Studio 启动过渡过程。
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 82b068612f0699cdba3788e4931fb6bdfe8c7e69
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796498"
---
# <a name="staging-stored-procedure-master-data-services"></a>临时存储过程 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  从 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]启动临时过程时，您使用三个存储过程之一。  
  
-   stg.<name _Leaf udp_ \<name>  
  
-   stg.<name _Consolidated udp_ \<name>  
  
-   stg.<name _Relationship udp_ \<name>  
  
 其中 name 是创建实体时指定的临时表的名称。  
  
## <a name="staging-process-stored-procedure-parameters"></a>临时过程存储过程参数  
 下表列出了这些存储过程的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|**VersionName**<br /><br /> 必选|版本的名称。 这可能区分大小写，也可能不区分，具体取决于您的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 排序规则设置。|  
|**LogFlag**<br /><br /> 必选|确定在临时过程中是否记录事务。 可能的值包括：<br /><br /> **0**：不记录事务。<br /><br /> **1**：记录事务。<br /><br /> <br /><br /> 有关事务的详细信息，请参阅[事务 (Master Data Services)](../master-data-services/transactions-master-data-services.md)。|  
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
      @UserName=N'domain\user'  
  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [验证存储过程 &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [查看暂存过程中出现的错误 (Master Data Services)](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)  
  
  
