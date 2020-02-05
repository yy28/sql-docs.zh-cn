---
title: 标识与可用性组关联的等待
description: 使用 Transact-SQL (T-SQL) 和扩展事件标识与 Always On 可用性组关联的等待。
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: afa8caff-f325-48d9-a8ef-a30beab60389
author: rothja
ms.author: jroth
ms.openlocfilehash: a62145645a965d46c8da076eca14cd8a3dd85857
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "67934960"
---
# <a name="identify-waits-associated-with-availability-groups"></a>标识与可用性组关联的等待
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  排除 Always On 可用性组延迟问题时，可在动态管理视图 (DMV) 中使用特定于可用性组的等待类型 [sys.dm_os_wait_stats (Transact-SQL)](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) 监视累积统计信息。  
  
 有关使用等待统计信息的常规信息，请参阅 [SQL Server 2005 等待和队列](https://technet.microsoft.com/library/cc966413.aspx)。 该文档针对 SQL Server 2005 编写，但其信息适用于更高版本的 SQL Server。  
  
## <a name="query-for-availability-groups-wait-types"></a>针对可用性组等待类型的查询  
 使用下面的 T-SQL 查询检索可用性组等待类型的所有等待统计信息：  
  
```sql  
SELECT * FROM sys.dm_os_wait_stats   
WHERE wait_type LIKE '%hadr%'  
ORDER BY wait_time_ms DESC  
```  
  
 要通过捕获扩展事件监视等待统计信息，请使用下面的 T-SQL 命令。  
  
```sql
CREATE EVENT SESSION [alwayson] ON SERVER   
ADD EVENT sqlos.wait_info(  
    WHERE ([wait_type]=(758) OR [wait_type]=(776) OR [wait_type]=(853) OR [wait_type]=(833)))  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,  
MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)  
GO  
```  
  
 可通过运行下面的查询，查看等待类型的键值映射：  
  
```sql
SELECT * FROM sys.dm_xe_map_values   
WHERE name='wait_types' AND map_value LIKE '%hadr%'   
ORDER BY map_key ASC  
```  
  
## <a name="next-steps"></a>后续步骤  
 [等待的类型](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md#WaitTypes)  
  
  
