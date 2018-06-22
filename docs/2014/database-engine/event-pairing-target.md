---
title: 事件配对目标 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- pairing target [SQL Server extended events]
- event pairing target
- targets [SQL Server extended events], pairing target
ms.assetid: 3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2b2bff842462e0ab77ecd30373df00746260cea5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015304"
---
# <a name="event-pairing-target"></a>事件配对目标
  事件配对目标使用两个事件中存在的一列或多列数据来对这两个事件进行匹配。 许多事件是成对的，例如，锁获取和锁释放。 对某个事件序列配对完毕，便会放弃这两个事件。 放弃匹配完毕的事件便于检测哪些获取的锁尚未释放。  
  
 通过使用事件级别筛选器，可以使用配对目标仅捕获那些与预设条件不匹配的事件。  
  
 使用事件配对目标时，可以选择两个要匹配的事件和一个序列，此序列由要对其进行匹配的列构成。 此序列中的所有列必须属于同一类型。  
  
 下表描述了配置事件配对时可用的选项。  
  
|选项|允许的值|Description|  
|------------|--------------------|-----------------|  
|begin_event|当前会话中存在的任何一个事件的名称。|用于指定成对序列中开始事件的事件名称。|  
|end_event|当前会话中存在的任何一个事件的名称。|用于指定成对序列中结束事件的事件名称。|  
|begin_matching_columns|一个以逗号分隔的列名称排序列表。|要对其执行匹配的列。|  
|end_matching_columns|一个以逗号分隔的列名称排序列表。|要对其执行匹配的列。|  
|begin_matching_actions|一个以逗号分隔的操作排序列表。|要对其执行匹配的操作。|  
|end_matching_actions|一个以逗号分隔的操作排序列表。|要对其执行匹配的操作。|  
|respond_to_memory_pressure|可以是以下值之一：<br /><br /> 0 = 不响应。<br /><br /> 1 = 内存不足时停止向列表添加新的孤立项。|目标对内存事件予以响应。 如果设为 1，则服务器内存不足时，将删除保留的不成对信息。|  
|max_orphans||指定将在目标中收集的不成对事件的总数。 一旦达到此限制，将在先入先出 (FIFO) 的基础上删除不成对事件。 默认值 = 10,000。|  
  
 系统将捕获并存储与某个事件相关联的所有数据，以供将来配对之用。 此外，还将收集由操作添加的数据。 收集的事件数据存储在内存中，因此会有一定的限制。 此限制基于系统容量和活动。 所用内存量将根据可用系统资源来决定，而不是以最大内存量作为限定因素。 内存不足时，将删除已经保留的不成对事件。 如果某事件尚未成对便被删除，则与之匹配的事件将作为不成对事件出现。  
  
 配对目标会将不成对事件序列化为 XML 格式。 此格式不遵从任何架构， 只包含两种元素类型。 **\<不成对 >** 元素是根后, 跟一个元素。 **\<事件 >** 当前是否正在跟踪的每个不成对事件的元素。 **\<事件 >** 元素包含一个属性，其中包含不成对事件的名称。  
  
## <a name="adding-the-target-to-a-session"></a>将目标添加到会话  
 若要将配对目标添加到扩展事件会话，您必须在创建或更改事件会话时包括下面的语句：  
  
```  
ADD TARGET package0.pair_matching   
```  
  
 紧接着可以使用一个 SET 语句，以定义开始和结束事件，以及要匹配的操作或列。 下面的示例演示对匹配的 sqlserver.lock_acquired 和 sqlserver.lock_released 事件的示例语法。  
  
```  
   ( SET begin_event = 'sqlserver.lock_acquired',  
      begin_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
      end_event = 'sqlserver.lock_released',  
      end_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
   respond_to_memory_pressure = 1)  
```  
  
 有关详细信息，请参阅 [确定持有锁的查询](../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)。  
  
## <a name="reviewing-the-target-output"></a>查看目标输出  
 若要查看成对匹配目标的输出，你可以使用下面的查询，将 *session_name* 替换为事件会话的名称。  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 下面的示例演示了配对目标输出格式。  
  
```  
<unpaired truncated = "0" matchedCount = "[matched count]" memoryPressureDroppedCount = " [lost count]">  
    <event name  = "[event name]" package = "[package]" id= "[event ID value]" version = "[event version]">  
    <data name = "[column name]">   
    <type name = "[column type]" package = "[type package]" />   
    <value>[column value]</value>  
    <text value>[text value]</text>>  
        </data>  
    </event>  
</unpaired>  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 扩展事件目标](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
