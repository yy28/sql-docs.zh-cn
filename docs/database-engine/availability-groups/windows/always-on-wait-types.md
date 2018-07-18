---
title: Always On 可用性组等待类型 (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: afa8caff-f325-48d9-a8ef-a30beab60389
caps.latest.revision: 6
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1eee6003c8697be620fd69a0dc137d12c14620b8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32858352"
---
# <a name="always-on-availability-groups-wait-types"></a>Always On 可用性组等待类型
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
  
  