---
title: SQL Server - Query Store 对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store object
- SQL Server:Query Store
ms.assetid: b4a04acd-0b66-44a5-b72d-1a45b49e13e6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9da34a3bcf208e433b62a29a34b8cd87e5269cbe
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158630"
---
# <a name="sql-server-query-store-object"></a>SQL Server，Query Store 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Query Store 对象提供计数器来监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的资源利用率，从而存储对象（如存储过程、临时和预定义 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和触发器）的查询文本、执行计划和运行时统计信息。  
  
 下表介绍了 **SQLServer:Query Store**计数器。  
  
|SQL Server Query Store 计数器|描述|  
|-------------------------------------|-----------------|  
|**Query Store CPU 使用率**|指明 Query Store 的 CPU 使用率。|  
|**Query Store 逻辑读取次数**|指明由 Query Store 执行的逻辑读取次数。|  
|**Query Store 逻辑写入次数**|指明正在排队等待从 Query Store 刷新的数据量。 将项（表示运行时统计信息）添加到队列的频率和延迟是由“数据刷新间隔”设置进行控制。|  
|**Query Store 物理读取次数**|指明由 Query Store 执行的物理读取次数。|  
  
 对象中的每个计数器均包含以下实例：  
  
|Query Store 实例|描述|  
|--------------------------|-----------------|  
|**_Total**|此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的 Query Store 信息。|  
|\<数据库名称>|此数据库的 Query Store 信息。|  
  
## <a name="see-also"></a>另请参阅  
 [使用查询存储来监视性能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [查询存储存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [查询存储目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
