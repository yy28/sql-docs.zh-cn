---
title: SQL Server - Columnstore 对象 | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 415caa19f4d659ad6bf9540672c4feede7542119
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-columnstore-object"></a>SQL Server，列存储对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **SQLServer:Columnstore** 对象提供计数器以监视在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中执行的列存储索引。  
  
 下表介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **列存储** 计数器。  
  
|列存储计数器|Description|  
|--------------------------|-----------------|  
|**已关闭增量行组**|关闭的增量行组数。|  
|**已压缩增量行组**|压缩的增量行组数。|  
|**已创建增量行组**|创建的增量行组数。|  
|**段缓存命中率**|无需从磁盘读取即可在列存储池中找到的列段百分比。|  
|**Segment Cache Hit Ratio Base**|仅限内部使用。|
|**段读取次数/秒**|发出的物理段读取次数。|  
|**已迁移的删除缓冲区合计**|元组发动机清除删除缓冲区的次数。|  
|**合并策略评估数合计**|评估列存储合并策略的次数。|  
|**压缩的行组合计**|压缩的行组总数。|  
|**适合合并的行组合计**|自 SQL Server 启动以来适合 MERGE 的源行组数。|  
|**压缩的合并行组合计**|自 SQL Server 启动以来使用 MERGE 创建的已压缩目标源行组数。|  
|**合并的源行组合计**|自 SQL Server 启动以来合并的源行组数。|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
