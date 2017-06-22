---
title: "SQL Server - External Scripts 对象 | Microsoft Docs"
ms.custom: 
ms.date: 03/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- External Scripts object
- SQLServer:External Scripts
ms.assetid: 8a75ccce-b174-4937-bc92-8e413b55afe1
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2e5f146f5684567ec39e62d9c6d7786f3506d8d0
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-external-scripts-object"></a>SQL Server，外部脚本对象
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  **中的** SQLServer:External Scripts [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象可以提供计数器，以监视与执行外部脚本关联的操作。 有关执行外部脚本的信息，请参阅 [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。  
  
 下表介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **外部脚本** 计数器。  
  
|SQL Server 外部脚本计数器|说明|  
|------------------------------------------|-----------------|  
|**执行错误**|执行外部脚本时的错误数量。|  
|**隐含身份验证登录**|通过使用默示身份验证从附属进程验证的登录次数。|  
|**并行执行**|使用 @parallel = 1 执行的外部脚本的数量。|  
|**SQL CC 执行**|使用 SQL 计算上下文执行的外部脚本的数量。|  
|**流式执行**|使用 @r_rowsPerRead 参数执行的外部脚本的数量。|  
|**总执行时间 (ms)**|执行外部脚本花费的总时间。|  
|**执行总次数**|已执行的外部脚本的数量。|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.resource_governor_external_resource_pools (Transact SQL)](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity (Transact SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  

