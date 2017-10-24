---
title: "重播跟踪 （SQL Server 事件探查器） 的注意事项 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 77934826a2ba364c4ec8b4e6a5295699d8469257
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>重播跟踪的注意事项 (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]无法重播下列类型的跟踪：  
  
-   包含事务复制和其他事务日志活动的跟踪。 将跳过这些事件。 其他类型的复制不标记事务日志，因此它们不会受到影响。  
  
-   包含涉及全局唯一标识符 (GUID) 的操作的跟踪。 这些事件将被跳过。  
  
-   包含对 **text**、 **ntext**和 **image** 列的操作、涉及 **bcp** 实用工具、BULK INSERT、READTEXT、WRITETEXT 和 UPDATETEXT 语句以及全文操作的跟踪。 将跳过这些事件。  
  
-   包含会话绑定（ **sp_getbindtoken** 和 **sp_bindsession** 系统存储过程）的跟踪。 将跳过这些事件。  
  
> [!NOTE]  
>  如果不使用预先配置的重播模版 (**TSQL_Replay**)，也不捕获所有必需的数据，则 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 将不重播跟踪。 有关详细信息，请参阅 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
 有关重播跟踪需要哪些权限的信息，请参阅 [Permissions Required to Run SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)。  
  
## <a name="see-also"></a>另请参阅  
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [SQL Server 事件类参考](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [sp_bindsession &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [READTEXT &#40;Transact SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [WRITETEXT &#40;Transact SQL &#41;](../../t-sql/queries/writetext-transact-sql.md)   
 [UPDATETEXT &#40;Transact SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  

