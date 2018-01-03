---
title: "optimize for ad hoc workloads 服务器配置选项 | Microsoft Docs"
ms.custom: 
ms.date: 11/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 96e21a0eb32b9aeecabdfeb574d3e793b3ab99d8
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>“针对即席工作负荷进行优化”服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  “针对即席工作负荷进行优化”  选项用于提高包含许多一次性临时批处理的工作负荷计划缓存的效率。 如果该选项设置为 1，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将在首次编译批处理时在计划缓存中存储一个编译的小计划存根，而不是存储完全编译的计划。 这种情况下不会让未重复使用的编译计划填充计划缓存，从而有助于缓解内存压力。  
  
 编译的计划存根使 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 能够识别此临时批处理以前已经过编译，但只存储了编译计划存根，因此当再次调用（编译或执行）此批处理时， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 会对此批处理进行编译，从计划缓存中删除编译计划存根并将完全编译的计划添加到计划缓存中。 
  
 编译计划存根是 sys.dm_exec_cached_plans 目录视图显示的 cacheobjtype 之一。 它具有唯一的 SQL 句柄和计划句柄。 编译计划存根没有与其关联的执行计划，并且查询计划句柄不会返回 XML 显示计划。  
  
 [跟踪标志 8032](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 将缓存限制参数还原为 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM 设置，此设置通常允许更大的缓存。 当频繁重复使用的缓存条目不适合缓存时，以及当“针对即席工作负荷进行优化”服务器配置选项未能解决与计划缓存相关的问题时，请使用此设置。  
  
> [!WARNING]  
>  如果大缓存使较少的内存可用于其他内存消耗者（如缓冲池），则跟踪标志 8032 可能导致性能较差。  

## <a name="recommendations"></a>建议
如果一次性计划的数量在 OLTP 服务器的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 内存中占了很大一部分（并且这些计划是临时计划），请使用这个服务器选项降低这些对象的内存使用量。
要获取一次性缓存计划的数量，请运行下列查询：

```sql
SELECT objtype, cacheobjtype, 
  AVG(usecounts) AS Avg_UseCount, 
  SUM(refcounts) AS AllRefObjects, 
  SUM(CAST(size_in_bytes AS bigint))/1024/1024 AS Size_MB
FROM sys.dm_exec_cached_plans
WHERE objtype = 'Adhoc' AND usecounts = 1
GROUP BY objtype, cacheobjtype;
```

> [!IMPORTANT]
> 将“针对即席工作负荷进行优化”  设置为 1 只会影响新计划；已在计划缓存中的计划不受影响。
> 若要立即影响已缓存的查询计划，需使用 [ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 清除计划缓存，或需重启 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

## <a name="see-also"></a>另请参阅  
 [sys.dm_exec_cached_plans (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
