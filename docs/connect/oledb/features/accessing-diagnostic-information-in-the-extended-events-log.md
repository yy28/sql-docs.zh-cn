---
title: 访问扩展的事件日志中的诊断信息 |Microsoft 文档
description: 跟踪 SQL Server 的 OLE DB 驱动程序和访问扩展的事件日志中的诊断信息
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: c10eb2e76b881fa0f87f2fd7f430eb3e24df19c6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>访问扩展事件日志中的诊断信息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  从[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，OLE DB 驱动程序的 SQL Server 和数据访问跟踪 ([数据访问跟踪](http://go.microsoft.com/fwlink/?LinkId=125805)) 已更新，以更加轻松地从连接环形缓冲区中获取连接故障的诊断信息和扩展的事件日志中的应用程序性能信息。  
  
 有关读取扩展的事件日志的信息，请参阅[查看事件会话数据](../../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)。 

  
> [!NOTE]  
>  该功能只用于故障排除和诊断目的，可能不适合审核或安全目的。  
  
## <a name="remarks"></a>注释  
 对于连接操作，OLE DB 驱动程序的 SQL Server 将发送一个客户端连接 id。 如果连接失败，你可以访问连接环形缓冲区 ([连接中使用连接环形缓冲区的 SQL Server 2008 的故障排除](http://go.microsoft.com/fwlink/?LinkId=207752)) 并查找**ClientConnectionID**字段和获取有关连接故障的诊断信息。 仅当发生错误时，才在环形缓冲区中记录客户端连接 ID。 （如果在发送预登录数据包之前连接失败，将不会生成客户端连接 ID。）客户端连接 ID 是 16 字节的 GUID。 你还可以查找客户端连接 ID 在扩展事件输出目标，如果**client_connection_id**操作将添加到事件中扩展的事件会话。 你可以启用数据访问跟踪并重新运行连接命令并观察**ClientConnectionID**字段中失败的操作，数据访问跟踪，如果您需要进一步诊断帮助。  
   
  
 OLE DB 驱动程序的 SQL Server 还会发送一个特定于线程的活动 id。 如果开始会话时启用了 TRACK_CAUSAILITY 选项，则会在扩展的事件会话中捕获活动 ID。 有关活动连接的性能问题，你可以从客户端的数据访问跟踪获取活动 ID (**ActivityID**字段)，然后查找扩展的事件输出中的活动 ID。 扩展事件中的活动 ID 是 16 字节 GUID（与客户端连接 ID 的 GUID 不同），且后面追加四个字节的序列号。 该序列号表示某个请求在线程内的顺序，并指示线程的批处理和 RPC 语句的相对顺序。 **ActivityID**上启用数据访问跟踪和数据访问跟踪配置字中的第 18 位处于开启时根据需要发送的 SQL 批处理语句和 RPC 请求。  
  
 以下是一个使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 启动扩展事件会话的示例，该会话将存储在环形缓冲区中，并将记录从客户端针对 RPC 和批处理操作发送的活动 ID。  
  
```  
create event session MySession on server   
add event connectivity_ring_buffer_recorded,   
add event sql_statement_starting (action (client_connection_id)),   
add event sql_statement_completed (action (client_connection_id)),   
add event rpc_starting (action (client_connection_id)),   
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
  
```  
  
## <a name="control-file"></a>控制文件  
 SQL Server 控件文件 (ctrl.guid) OLE DB 驱动程序的内容是：  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x630ff  0   MSDADIAG.ETW
{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}  0x630ff  0   MSOLEDBSQL.1  
```  
  
## <a name="mof-file"></a>MOF 文件  
 SQL Server mof 文件 OLE DB 驱动程序的内容是：  
  
```  
#pragma classflags("forceupdate")  
#pragma namespace ("\\\\.\\Root\\WMI")  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  MSDADIAG.ETW  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F3-3CC6-0B9C-6651-9649CCE5C752}"),  
 DisplayName("msdadiag"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace : Bid2Etw_MSDADIAG_ETW  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextA : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextW : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  MSOLEDBSQL.1  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1 : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59D-D3E8-9684-AEAC-B214EFD91B31}"),  
 DisplayName("MSOLEDBSQL.1"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace : Bid2Etw_MSOLEDBSQL_1  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1 formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextA : Bid2Etw_MSOLEDBSQL_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1 formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextW : Bid2Etw_MSOLEDBSQL_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
```  
  
## <a name="see-also"></a>另请参阅  
 [处理错误](../../oledb/ole-db-errors/errors.md)  
  
  
