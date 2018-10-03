---
title: 事件计数器目标 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- synchronous event counter target [SQL Server extended events]
- targets [SQL Server extended events], synchronous event counter target
ms.assetid: 342e08d1-dcca-4a71-ae64-cb61b55b85bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8f701ff8a1648a3f90f7e04c71f159081ac7a3da
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101177"
---
# <a name="event-counter-target"></a>事件计数器目标
  事件计数器目标将计算在扩展事件会话过程中发生的所有事件数目。 通过使用事件计数器目标，您可以获得有关工作负荷特征的信息，而不必因进行完整的事件收集而增加系统开销。 此目标不包含任何可自定义的参数。  
  
## <a name="adding-the-target-to-a-session"></a>将目标添加到会话  
 若要将事件计数器目标添加到扩展事件会话，您必须在创建或更改事件会话时包括下面的语句：  
  
```  
ADD TARGET package0.event_counter  
```  
  
## <a name="reviewing-the-target-output"></a>查看目标输出  
 若要查看事件计数器目标的输出，你可以使用下面的查询，将 *session_name* 替换为事件会话的名称：  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 下面的示例演示了事件计数器目标输出的格式。  
  
```  
<CounterTarget truncated = "0">  
  <Packages>  
    <Package name = "[package name]">  
      <Event name = "[event name]" count = "[number]" />  
    </Package>  
  </Packages>  
</CounterTarget>  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 扩展事件目标](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
