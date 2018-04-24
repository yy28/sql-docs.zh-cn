---
title: 使用 system_health 会话 | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 57bdc59b3b5db69fdf01737b0a850725e9b17f88
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="use-the-systemhealth-session"></a>使用 system_health 会话
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  system_health 会话是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]默认包含的扩展事件会话。 该会话在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 启动时自动启动，并且运行时不会对性能造成任何明显影响。 该会话收集的系统数据可用于帮助对 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的性能问题进行故障排除。 因此，我们建议您不要停止或删除该会话。  
  
 该会话收集的信息包括：  
  
-   发生严重性 >=20 的错误的任何会话的 sql_text 和 session_id 。  
  
-   发生内存相关错误的任何会话的 sql_text 和 session_id 。 这些错误包括 17803、701、802、8645、8651、8657 和 8902。  
  
-   任何无法完成的计划程序问题的记录。 （这些问题在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中显示为错误 17883。）  
  
-   检测到的任何死锁。  
  
-   等待闩锁（或其他相关资源）时间 > 15 秒的任何会话的 callstack、sql_text 和 session_id。  
  
-   等待锁（或其他相关资源）时间 > 30 秒的任何会话的 callstack、sql_text 和 session_id。  
  
-   为获得“抢先等待”（或其他相关资源）而等待时间很长的任何会话的 callstack、sql_text 和 session_id。 持续时间因等待类型而异。 在抢先等待中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 等待的是外部 API 调用。  
  
-   CLR 分配失败和虚拟分配失败的调用堆栈和 session_id。  
  
-   有关内存 Broker、计划程序监视、内存节点 OOM、安全性和连接的 ring_buffer 事件。  
  
-   sp_server_diagnostics 中的系统组件结果。  
  
-   scheduler_monitor_system_health_ring_buffer_recorded 收集的实例运行状况。  
  
-   CLR 分配失败。  
  
-   使用 connectivity_ring_buffer_recorded 时的连接错误。  
  
-   使用 security_error_ring_buffer_recorded 时的安全错误。  
  
## <a name="viewing-the-session-data"></a>查看会话数据  
 会话使用环形缓冲区目标存储数据。 若要查看会话数据，请使用下面的查询：  
  
```  
SELECT CAST(xet.target_data as xml) FROM sys.dm_xe_session_targets xet  
JOIN sys.dm_xe_sessions xe  
ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'system_health'  
```  
  
若要查看事件文件中的会话数据，请使用 Management Studio 中提供的扩展事件用户界面。 有关详细信息，请参阅 [SQL Server 中扩展事件的目标数据的高级查看功能](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)。
  
## <a name="restoring-the-systemhealth-session"></a>还原 system_health 会话  
 如果删除 system_health 会话，则可以通过在查询编辑器中执行 **u_tables.sql** 文件来还原该会话。 该文件位于下面的文件夹中，其中 C: 表示您安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程序文件的驱动器：  
  
 C:\Program Files\Microsoft SQL Server\MSSQL13.\<*instanceid*>\MSSQL\Install  
  
 请注意，在还原该会话后，必须使用 ALTER EVENT SESSION 语句或使用对象资源管理器中的 **“扩展事件”** 节点启动会话。 否则，该会话会在您下次重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务时自动启动。  
  
## <a name="see-also"></a>另请参阅  
 [扩展事件工具](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
