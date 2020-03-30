---
title: SQL Server - Plan Cache 对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Plan Cache object
- SQLServer:Plan Cache
ms.assetid: 225e2b02-8d2f-4f29-9eba-f5847c36ea99
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a181919a40ce2e53c9fef9887f5c7ec6ff93fc5b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68130847"
---
# <a name="sql-server-plan-cache-object"></a>SQL Server Plan Cache 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Plan Cache** 对象提供用于监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何使用内存来存储对象（例如存储过程、即席和准备的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句以及触发器）的计数器。 可同时监视 **Plan Cache** 对象的多个实例，每个实例代表一个要监视的不同类型的计划。  
  
 下表介绍了 **SQLServer:Plan Cache**计数器。  
  
|SQL Server Plan Cache 计数器|说明|  
|------------------------------------|-----------------|  
|**Cache Hit Ratio**|高速缓存命中次数和查找次数的比率。|  
|**Cache Hit Ratio Base**|仅供内部使用。| 
|**Cache Object Counts**|高速缓存中高速缓存的对象数。|  
|**Cache Pages**|高速缓存对象所使用的 8 (KB) 页的数目。|  
|**Cache Objects in use**|正在使用的缓存对象数。|  
  
 对象中的每个计数器均包含以下实例：  
  
|Plan Cache 实例|说明|  
|-------------------------|-----------------|  
|**_Total**|所有类型的缓存实例的信息。|  
|**Sql 计划**|由一个临时的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询（包括自动参数化查询）生成的查询计划，或使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] sp_prepare **或** sp_cursorprepare **预备的**语句生成的查询计划。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将临时的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的计划存入缓存，以便将来需要执行相同的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句时再次使用。 用户参数化的查询（即使未显式准备）也作为准备好的 SQL 计划监视。|  
|**对象计划**|通过创建存储过程、函数或触发器而生成的查询计划。|  
|**绑定树**|视图、规则、计算列和检查约束的规范化树。|  
|**扩展存储过程**|扩展存储过程的目录信息。|  
|**临时表和表变量**|与临时表和表变量相关的缓存信息。|  
  
## <a name="see-also"></a>另请参阅  
 [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server Buffer Manager 对象](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
