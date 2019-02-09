---
title: 环形缓冲区目标 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events], ring buffer target
- ring buffer target [SQL Server extended events]
ms.assetid: 54494e11-b56b-43b7-aa5e-c8724e56b251
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d042ef49a82d16eb33cb27d80c8083a68ea69092
ms.sourcegitcommit: 4b5ea5fa3253fea028e1adbd46bd18b89f0a115b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "55905652"
---
# <a name="ring-buffer-target"></a>环形缓冲区目标
  环形缓冲区目标用于在内存中暂时容纳事件数据。 此目标可通过以下两种模式中的一种来管理事件。  
  
-   第一种模式是严格的先进先出模式 (FIFO)，在这种模式下，当分配给目标的所有内存都用尽时，将放弃最旧的事件。 在这种模式下（默认模式），occurrence_number 选项设为 0。  
  
-   第二种模式是按事件 FIFO，在这种模式下，每种类型将保留指定数量的事件。 在此模式下，每种类型的最早的事件时，放弃使用分配给目标的所有内存。 您可以配置 occurrence_number 选项来指定要保留的每种类型的事件数。  
  
 下表描述了配置环形缓冲区目标时可用的选项。  
  
|选项|允许的值|Description|  
|------------|--------------------|-----------------|  
|max_memory|任何 32 位的整数。 该值是可选的。|要使用的最大内存量 (KB)。 将基于首先到达的限制删除现有事件：max_event_limit 或 max_memory。 最大值为 4194303 KB。 环形缓冲区大小设置为 GB 范围中的限制，因为它可能会影响其他 SQL Server 中的内存使用者前应仔细考虑|  
|max_event_limit|任何 32 位的整数。 该值是可选的。|保留在 ring_buffer 中的事件的最大数量。 将基于首先到达的限制删除现有事件：max_event_limit 或 max_memory。 默认值 = 1000。|  
|occurrence_number|可以是以下值之一：<br /><br /> 0（默认值）= 当分配给目标的所有内存都用尽时，将放弃最旧的事件。<br /><br /> 任何 32 位整数 = 按事件 FIFO 的基础，在放弃之前保留每种类型的事件数。<br /><br /> <br /><br /> 该值是可选的。|FIFO 模式使用，如果设为大于 0 的值，则为要保留在缓冲区中的每种类型的首选事件数。|
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="adding-the-target-to-a-session"></a>将目标添加到会话  
 若要将环形缓冲区目标添加到扩展事件会话中，您必须在创建或更改事件会话时包括下面的语句：  
  
```sql
ADD TARGET package0.ring_buffer  
```  
  
## <a name="reviewing-the-target-output"></a>查看目标输出  
 若要查看环形缓冲区目标的输出，可以使用下面的查询，并将 *session_name* 替换为事件会话的名称。  
  
```sql
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 下面的示例演示了环形缓冲区目标的输出格式。  
  
```  
<RingBufferTarget eventsPerSec="" processingTime="" totalEventsProcessed="" eventCount="" droppedCount="" memoryUsed="">  
 <event name="" package="" id="" version="" timestamp="">  
    <data name="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </data>  
    <action name="" package="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </action>  
  </event>  
</RingBufferTarget>  
```


## <a name="see-also"></a>请参阅

- [SQL Server 扩展事件目标](../../2014/database-engine/sql-server-extended-events-targets.md)
- [sys.dm_xe_session_targets (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql?view=sql-server-2016)
- [CREATE EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/create-event-session-transact-sql?view=sql-server-2016)
- [ALTER EVENT SESSION (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-event-session-transact-sql?view=sql-server-2016)

