---
title: 重播跟踪的注意事项 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2dd2fe9f5e4e2a5b41c9951b1a38dd819a15aa35
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316043"
---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>重播跟踪的注意事项 (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 无法重播下列类型的跟踪：  
  
-   包含事务复制和其他事务日志活动的跟踪。 将跳过这些事件。 其他类型的复制不标记事务日志，因此它们不会受到影响。  
  
-   包含涉及全局唯一标识符 (GUID) 的操作的跟踪。 这些事件将被跳过。  
  
-   包含对 **text**、 **ntext**和 **image** 列的操作、涉及 **bcp** 实用工具、BULK INSERT、READTEXT、WRITETEXT 和 UPDATETEXT 语句以及全文操作的跟踪。 将跳过这些事件。  
  
-   包含会话绑定（ **sp_getbindtoken** 和 **sp_bindsession** 系统存储过程）的跟踪。 将跳过这些事件。  
  
> [!NOTE]  
>  如果不使用预先配置的重播模版 (**TSQL_Replay**)，也不捕获所有必需的数据，则 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 将不重播跟踪。 有关详细信息，请参阅 [Replay Requirements](replay-requirements.md)。  
  
 有关重播跟踪需要哪些权限的信息，请参阅 [Permissions Required to Run SQL Server Profiler](sql-server-profiler.md)。  
  
## <a name="see-also"></a>请参阅  
 [bcp 实用工具](../bcp-utility.md)   
 [SQL Server 事件类参考](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql)   
 [sp_bindsession (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-bindsession-transact-sql)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [READTEXT (Transact-SQL)](/sql/t-sql/queries/readtext-transact-sql)   
 [WRITETEXT (Transact-SQL)](/sql/t-sql/queries/writetext-transact-sql)   
 [UPDATETEXT (Transact-SQL)](/sql/t-sql/queries/updatetext-transact-sql)  
  
  
