---
title: "SQL Server R Services 的扩展事件 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 11/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4e90e057-aacb-4adc-8da6-64861f4e87df
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0b4d65cd2812fea830bbdd7127b8f47569979e94
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="extended-events-for-sql-server-r-services"></a>SQL Server R 服务的扩展事件
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 提供了一组扩展事件，用于对与 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 相关的操作或发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 R 作业进行故障排除。  
  
 若要查看与 SQL Server 相关的事件的列表，请从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]运行以下查询。  
  
```  
select o.name as event_name, o.description  
  from sys.dm_xe_objects o  
  join sys.dm_xe_packages p  
    on o.package_guid = p.guid  
 where o.object_type = 'event'  
   and p.name = 'SQLSatellite';  
```  
  
 但是， [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的一些额外的扩展事件只能从外部进程触发，例如 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]、BXLServer 和启动 R 运行时的附属进程。 有关如何捕获这些事件的详细信息，请参阅 [Collecting Events from External Processes](#bkmk_externalevents)。  
  
 有关使用扩展事件的一般信息，请参阅 [SQL Server Extended Events Sessions](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)。  

  
##  <a name="bkmk_xeventtable"></a> 扩展事件表  
  
|事件|说明|改用|  
|-----------|-----------------|---------|  
|connection_accept|接受一个新连接时发生。 此事件用于记录所有连接尝试。||  
|failed_launching|启动失败。|指示一个错误。|  
|satellite_abort_connection|中止连接记录||  
|satellite_abort_received|通过卫星连接接收中止消息时触发。||  
|satellite_abort_sent|通过卫星连接发送中止消息时触发。||  
|satellite_authentication_completion|对基于 TCP 或 Namedpipe 的连接的身份验证完成时触发。||  
|satellite_authorization_completion|对基于 TCP 或 Namedpipe 的连接的授权完成时触发。||  
|satellite_cleanup|卫星调用清理时触发。|仅从外部进程触发。 请参阅有关从外部进程收集事件的说明。|  
|satellite_data_chunk_sent|卫星连接完成发送单个数据区块时触发。|发送区块时，此事件报告发送的行数、列数、SNI 数据包 usedm 的数目以及所用时间（以毫秒为单位）。 这些信息可帮助你了解传递不同类型的数据时花费了多长时间，以及使用了多少个数据包。|  
|satellite_data_receive_completion|通过卫星连接接收查询所需的所有数据时触发。|仅从外部进程触发。 请参阅有关从外部进程收集事件的说明。|  
|satellite_data_send_completion|通过卫星连接发送会话所需的所有数据时触发。||  
|satellite_data_send_start|数据传输开始时（就在第一个数据区块发送之前）触发。||  
|satellite_error|用于跟踪 sql 卫星错误||  
|satellite_invalid_sized_message|消息大小无效||  
|satellite_message_coalesced|用于跟踪在网络层合并的消息||  
|satellite_message_ring_buffer_record|消息环形缓冲区记录||  
|satellite_message_summary|有关消息传送的摘要信息||  
|satellite_message_version_mismatch|消息的版本字段不匹配||  
|satellite_messaging|用于跟踪消息传送事件（绑定、取消绑定等）||  
|satellite_partial_message|用于跟踪网络层的部分消息||  
|satellite_schema_received|通过 SQL 接收和读取架构消息时触发。||  
|satellite_schema_sent|通过卫星发送架构消息时触发。|仅从外部进程触发。 请参阅有关从外部进程收集事件的说明。|  
|satellite_service_start_posted|当服务启动消息发布到 launchpad 时触发。|这可以通知 launchpad 启动外部进程，并且该事件包含此新会话的 ID。|  
|satellite_unexpected_message_received|接收到意外消息时触发。|指示一个错误。|  
|stack_trace|请求进行进程的内存转储时发生。|指示一个错误。|  
|trace_event|用于跟踪目的|这些事件可以包含 SQL Server、Launchpad 和外部进程跟踪消息。 这包括从 R 到 stdout 和 stderr 的输出。|  
|launchpad_launch_start|launchpad 开始启动卫星时触发。|仅从 Launchpad 触发。 请参阅有关从 launchpad.exe 收集事件的说明。|  
|launchpad_resume_sent|Launchpad 已启动卫星并将恢复消息发送到 SQL Server 时触发。|仅从 Launchpad 触发。 请参阅有关从 launchpad.exe 收集事件的说明。|  
|satellite_data_chunk_sent|卫星连接完成发送单个数据区块时触发。|包含列数、行数、数据包数量，以及发送数据区块所用的时间等信息。|  
|satellite_sessionId_mismatch|消息的会话 ID 不匹配||  
  
###  <a name="bkmk_externalevents"></a> Collecting Events from External Processes  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 启动在 SQL Server 进程外部运行的一些服务。 若要捕获与这些外部进程相关的事件，必须创建一个事件跟踪配置文件，并将文件放在与进程的可执行文件的相同的目录中。  
  
-   **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
     若要捕获与 Launchpad 相关的事件，请将 *.config* 文件放在 SQL Server 实例的 Binn 目录中。  在默认安装中，此目录为：`C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`。  
  
-   **BXLServer** 是使用 R 及其他外部脚本语言支持 SQL 可扩展性的附属进程。  
  
     若要捕获与 BXLServer 相关的事件，请将 *.config* 文件放在 R 安装目录中。  在默认安装中，此目录为：`C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`。  
  
> [!IMPORTANT]
>   此配置文件的名称必须与可执行文件相同，并使用“[名称].xevents.xml”的格式。 换而言之，这些文件的名称如下所示：  
>   
> - Launchpad.xevents.xml  
> - bxlserver.xevents.xml  
  
 配置文件自身具有以下格式：  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="[session name]" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="you">Xevent for launchpad or bxl server.</description>  
    <event package="SQLSatellite" name="[XEvent Name 1]" />  
    <event package="SQLSatellite" name="[XEvent Name 2]" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="[SessionName].xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
  
```  
  
 **注意：**  
  
-   若要配置跟踪，请编辑 *session name* 占位符、文件名的占位符 (`[SessionName].xel`) 和要捕获的事件的名称（如 `[XEvent Name 1]`、`[XEvent Name 1]`）。  
  
-   可能出现任意数量的 `event package` 标记，并且只要名称属性正确就会收集此标记。  
  
### <a name="example-capturing-launchpad-events"></a>示例：捕获 Launchpad 事件  
 下面的示例显示了 Launchpad 服务的事件跟踪定义。  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="launchpad_launch_start" />  
    <event package="SQLSatellite" name="launchpad_resume_sent" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="launchpad_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
  
```  
  
 **注意：**  
  
-   将 *.config* 文件放在 SQL Server 实例的 Binn 目录中。  
  
-   此文件必须命名为 *Launchpad.xevents.xml*。  
  
### <a name="example-capturing-bxlserver-events"></a>示例：捕获 BXLServer 事件  
 下面的示例显示了 BXLServer 可执行文件的事件跟踪定义。  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
 <event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="satellite_abort_received" />  
    <event package="SQLSatellite" name="satellite_authentication_completion" />  
    <event package="SQLSatellite" name="satellite_cleanup" />  
    <event package="SQLSatellite" name="satellite_data_receive_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_start" />  
    <event package="SQLSatellite" name="satellite_schema_sent" />   
    <event package="SQLSatellite" name="satellite_unexpected_message_received" />    
    <event package="SQLSatellite" name="satellite_data_chunk_sent" />   
    <target package="package0" name="event_file">  
      <parameter name="filename" value="satellite_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
  
```  
  
 **注意：**  
  
-   将 *.config* 文件放在与 BXLServer 可执行文件相同的目录中。  
  
-   此文件必须命名为 *bxlserver.xevents.xml*。  
  
## <a name="see-also"></a>另请参阅
[R Services 的自定义 Management Studio 报告](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [管理和监视 R 解决方案](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
  
  
