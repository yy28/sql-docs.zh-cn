---
title: SQL Server - Columnstore 对象 | Microsoft Docs
description: 了解 SQLServer:Columnstore 对象，该对象提供计数器以监视 SQL Server 中执行的列存储索引。
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f00f4405144cec17b0b0266308ebc6df39336a70
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458404"
---
# <a name="sql-server-columnstore-object"></a>SQL Server，列存储对象
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQLServer:Columnstore 对象提供计数器以监视在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中执行的列存储索引。  
  
 下表介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Columnstore 计数器。  
  
|列存储计数器|说明|  
|--------------------------|-----------------|  
|**已关闭增量行组**|关闭的增量行组数。|  
|**已压缩增量行组**|压缩的增量行组数。|  
|**已创建增量行组**|创建的增量行组数。|  
|**段缓存命中率**|无需从磁盘读取即可在列存储池中找到的列段百分比。|  
|**Segment Cache Hit Ratio Base**|仅供内部使用。|
|**段读取次数/秒**|发出的物理段读取次数。|  
|**已迁移的删除缓冲区合计**|元组发动机清除删除缓冲区的次数。|  
|**合并策略评估数合计**|评估列存储合并策略的次数。|  
|**压缩的行组合计**|压缩的行组总数。|  
|**适合合并的行组合计**|自 SQL Server 启动以来适合 MERGE 的源行组数。|  
|**压缩的合并行组合计**|自 SQL Server 启动以来使用 MERGE 创建的已压缩目标源行组数。|  
|**合并的源行组合计**|自 SQL Server 启动以来合并的源行组数。|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
