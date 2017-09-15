---
title: "访问扩展的事件日志中的诊断信息 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e6dfbd857905f0c0f444c44a9c9eb9813cc32ab2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>访问扩展事件日志中的诊断信息
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  在[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]、 跟踪 ([跟踪驱动程序操作](../../connect/jdbc/tracing-driver-operation.md)) 已更新，便于更轻松地将客户端事件与诊断信息，如连接失败，从服务器的连接环关联缓冲区和应用程序中扩展的事件日志的性能信息。 有关读取扩展的事件日志的信息，请参阅[查看事件会话数据](http://msdn.microsoft.com/library/hh710068(SQL.110).aspx)。  
  
## <a name="details"></a>详细信息  
 对于连接操作，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]将发送一个客户端连接 id。 如果连接失败，你可以访问连接环形缓冲区 ([连接中使用连接环形缓冲区的 SQL Server 2008 的故障排除](http://go.microsoft.com/fwlink/?LinkId=207752)) 并查找**ClientConnectionID**字段和获取有关连接故障的诊断信息。 仅当发生错误时，才在环形缓冲区中记录客户端连接 ID。 （如果在发送预登录数据包之前连接失败，将不会生成客户端连接 ID。）客户端连接 ID 是 16 字节的 GUID。 你还可以查找客户端连接 ID 在扩展的事件目标输出中，如果**client_connection_id**操作将添加到事件中扩展的事件会话。 你可以启用跟踪并重新运行连接命令并观察**ClientConnectionID**字段在跟踪中，如果需要进一步的客户端驱动程序诊断帮助。  
  
 你可以获取客户端连接 ID 以编程方式通过使用[ISQLServerConnection 接口](../../connect/jdbc/reference/isqlserverconnection-interface.md)。 该连接 ID 还存在于任何与连接相关的异常中。  
  
 存在连接错误时，服务器的 BID 跟踪信息和连接环形缓冲区中的客户端连接 ID 可以帮助将客户端连接与服务器上的连接关联。 在服务器上跟踪 BID 有关的详细信息，请参阅[Data Access Tracing](http://go.microsoft.com/fwlink/?LinkId=125805)。 请注意，数据访问跟踪文章还包含有关执行不适用于为数据访问跟踪信息[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]; 请参阅[跟踪驱动程序操作](../../connect/jdbc/tracing-driver-operation.md)有关的操作使用数据访问跟踪信息[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 JDBC Driver 还会发送特定于线程的活动 ID。 如果开始会话时启用了 TRACK_CAUSAILITY 选项，则会在扩展的事件会话中捕获活动 ID。 对于与活动连接有关的性能问题，你可以从客户端的跟踪中获取活动 ID（ActivityID 字段），然后在扩展事件输出中找到该活动 ID。 扩展事件中的活动 ID 是一个 16 字节 GUID（与客户端连接 ID 的 GUID 不同），附有一个四字节的序列号。 序列号代表线程内某个请求的顺序。 ActivityId 会为 SQL 批处理语句和 RPC 请求发送。 为了能将 ActivityId 发送到服务器，您首先需要在 Logging.Properties 文件中指定以下键值对：  
  
```  
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 以外的任何值`on`（区分大小写） 将禁用发送 ActivityId。  
  
 有关详细信息，请参阅[跟踪驱动程序操作](../../connect/jdbc/tracing-driver-operation.md)。 跟踪标志与对应的 JDBC 对象记录程序一起使用，以决定是否在 JDBC 驱动程序中跟踪和发送 ActivityId。 除了更新 Logging.Properties 文件以外，还需要在 FINER 或更高级别启用 com.microsoft.sqlserver.jdbc 记录程序。 如果你想为特定类发出的请求将 ActivityId 发送到服务器，则需要在 FINER 或 FINEST 级别启用对应的类记录程序。 例如，如果类是 SQLServerStatement，则启用 com.microsoft.sqlserver.jdbc.SQLServerStatement 记录程序。  
  
 以下是一个示例，使用[!INCLUDE[tsql](../../includes/tsql_md.md)]若要启动扩展的事件会话将存储在环形缓冲区，并且将记录的活动 ID 发送的 RPC 和批处理操作上的客户端：  
  
```  
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>另请参阅  
 [诊断 JDBC 驱动程序的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
