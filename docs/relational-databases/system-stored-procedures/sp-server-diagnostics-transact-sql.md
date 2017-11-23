---
title: "sp_server_diagnostics (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_server_diagnostics
- sp_server_diagnostics_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_server_diagnostics
ms.assetid: 62658017-d089-459c-9492-c51e28f60efe
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 537267b15a65dca3035ba79e6bbecb9f7bc4a51c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spserverdiagnostics-transact-sql"></a>sp_server_diagnostics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

捕获有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的诊断数据和运行状况信息，以检测潜在故障。 该过程以重复模式运行，并定期发送结果。 可通过常规连接或 DAC 连接调用该过程。  
  
**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_server_diagnostics [@repeat_interval =] 'repeat_interval_in_seconds'   
```  
  
## <a name="arguments"></a>参数  
 [  **@repeat_interval**  =] *repeat_interval_in_seconds*  
 指示存储过程重复运行以发送运行状况信息的时间间隔。  
  
 *repeat_interval_in_seconds*是**int**与默认值 0。 有效参数值为 0，或等于或大于 5 的任意值。 存储过程至少要运行 5 秒钟才能返回完整数据。 存储过程以重复模式运行的最短时间为 5 秒。  
  
 如果不指定此参数或者指定值为 0，存储过程将一次性返回数据，然后退出。  
  
 如果指定的值小于最小值，它将引发错误而不返回任何内容。  
  
 如果指定的值等于或大于 5，存储过程将重复运行以返回运行状态，直到将其手动取消为止。  
  
## <a name="return-code-values"></a>返回代码值  
0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
**sp_server_diagnostics**返回以下信息  
  
|列|数据类型|Description|  
|------------|---------------|-----------------|  
|**creation_time**|**datetime**|指示行创建的时间戳。 单个行集中的每一行都具有相同的时间戳。|  
|**component_type**|**sysname**|指示行是否包含信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例组件或 Always On 可用性组级别：<br /><br /> instance<br /><br /> Alwayson: AvailabilityGroup|  
|**组件**|**sysname**|指示组件的名称或可用性组的名称：<br /><br /> system<br /><br /> resource<br /><br /> query_processing<br /><br /> io_subsystem<br /><br /> 事件<br /><br /> *\<可用性组的名称 >*|  
|**状态**|**int**|指示组件的运行状况状态：<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> 3|  
|**state_desc**|**sysname**|描述状态列。 与状态列中的值对应的说明：<br /><br /> 0： 未知<br /><br /> 1： 干净<br /><br /> 2： 警告<br /><br /> 3： 错误|  
|**数据**|**varchar (max)**|指定特定于组件的数据。|  
  
 下面是对五个组件的说明：  
  
-   **系统**： 收集数据从 system 透视自旋锁、 严重处理条件、 无法完成任务、 页面错误、 和 CPU 使用率。 此信息会产生总体运行状态建议。  
  
-   **资源**： 从资源透视中收集数据，在物理和虚拟内存，缓冲池页、 缓存和其他内存对象。 此信息会提供总体运行状态建议。  
  
-   **query_processing**： 从工作线程，任务，查询处理的角度收集数据等待类型、 CPU 密集型会话和阻塞的任务。 此信息会提供总体运行状态建议。  
  
-   **io_subsystem**： 在 IO 上收集数据。 除了诊断数据外，此组件还可生成仅适用于 IO 子系统的干净运行状况或警告运行状态。  
  
-   **事件**： 收集数据并通过存储过程的图面上的错误和事件记录的服务器，包括有关环形缓冲区异常的详细信息的感兴趣的环有关内存 broker，了内存，计划程序监视器的缓冲事件缓冲池、 自旋锁、 安全性和连接。 事件将始终显示 0 作为状态。  
  
-   **\<可用性组的名称 >**： 收集数据的指定的可用性组 (如果 component_type ="始终上： AvailabilityGroup")。  
  
## <a name="remarks"></a>注释  
从故障角度而言，系统、资源和 query_processing 组件可用于故障检测，而 io_subsystem 和事件组件只能用于诊断用途。  
  
下表将组件映射到其关联的运行状态。  
  
|Components|干净 (1)|警告 (2)|错误 (3)|未知 (0)|  
|----------------|-----------------|-------------------|-----------------|--------------------|  
|system|x|x|x||  
|resource|x|x|x||  
|query_processing|x|x|x||  
|io_subsystem|x|x|||  
|事件||||x|  
  
每行中的 (x) 表示组件处于有效运行状态。 例如，io_subsystem 将显示为干净或警告。 它将不显示错误状态。  
 
> [!NOTE]
> 在以高优先级 preemptive 线程上执行时 sp_server_diagnostics 内部过程的执行。
  
## <a name="permissions"></a>Permissions  
要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
最好使用扩展会话捕获运行状态信息并将其保存到位于 SQL Server 之外的文件中。 因此，在出现故障时仍然可以访问。 以下示例将事件会话的输出保存到文件：  
```tsql  
CREATE EVENT SESSION [diag]  
ON SERVER  
           ADD EVENT [sp_server_diagnostics_component_result] (set collect_data=1)  
           ADD TARGET [asynchronous_file_target] (set filename='c:\temp\diag.xel');  
GO  
ALTER EVENT SESSION [diag]  
      ON SERVER STATE = start;  
GO  
```  
  
下面的示例查询读取扩展会话日志文件：  
```tsql  
SELECT  
    xml_data.value('(/event/@name)[1]','varchar(max)') AS Name  
  , xml_data.value('(/event/@package)[1]', 'varchar(max)') AS Package  
  , xml_data.value('(/event/@timestamp)[1]', 'datetime') AS 'Time'  
  , xml_data.value('(/event/data[@name=''component_type'']/value)[1]','sysname') AS Sysname  
  , xml_data.value('(/event/data[@name=''component_name'']/value)[1]','sysname') AS Component  
  , xml_data.value('(/event/data[@name=''state'']/value)[1]','int') AS State  
  , xml_data.value('(/event/data[@name=''state_desc'']/value)[1]','sysname') AS State_desc  
  , xml_data.query('(/event/data[@name="data"]/value/*)') AS Data  
FROM   
(  
      SELECT  
                        object_name as event  
                        ,CONVERT(xml, event_data) as xml_data  
       FROM    
      sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\*.xel', NULL, NULL, NULL)  
)   
AS XEventData  
ORDER BY time;  
```  
  
以下示例以非重复模式将 sp_server_diagnostics 的输出捕获到一个表中：  
```tsql  
CREATE TABLE SpServerDiagnosticsResult  
(  
      create_time DateTime,  
      component_type sysname,  
      component_name sysname,  
      state int,  
      state_desc sysname,  
      data xml  
);  
INSERT INTO SpServerDiagnosticsResult  
EXEC sp_server_diagnostics; 
```  

下面的示例查询显示输出表中的摘要如下：  
```tsql  
SELECT create_time,
       component_name,
       state_desc 
FROM SpServerDiagnosticsResult;  
``` 

下面的示例查询从表中的每个组件中读取一些详细的输出：  
```tsql  
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult 
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult 
where component_name like 'resource'
go

-- Nonpreemptive waits
select waits.evt.value('(@waitType)','varchar(100)') as 'Wait_Type',
   waits.evt.value('(@waits)','bigint') as 'Waits',
   waits.evt.value('(@averageWaitTime)','bigint') as 'Avg_Wait_Time',
   waits.evt.value('(@maxWaitTime)','bigint') as 'Max_Wait_Time'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/topWaits/nonPreemptive/byDuration/wait') AS waits(evt)
where component_name like 'query_processing'
go

-- Preemptive waits
select waits.evt.value('(@waitType)','varchar(100)') as 'Wait_Type',
   waits.evt.value('(@waits)','bigint') as 'Waits',
   waits.evt.value('(@averageWaitTime)','bigint') as 'Avg_Wait_Time',
   waits.evt.value('(@maxWaitTime)','bigint') as 'Max_Wait_Time'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/topWaits/preemptive/byDuration/wait') AS waits(evt)
where component_name like 'query_processing'
go

-- CPU intensive requests
select cpureq.evt.value('(@sessionId)','bigint') as 'SessionID',
   cpureq.evt.value('(@command)','varchar(100)') as 'Command',
   cpureq.evt.value('(@cpuUtilization)','bigint') as 'CPU_Utilization',
   cpureq.evt.value('(@cpuTimeMs)','bigint') as 'CPU_Time_ms'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/cpuIntensiveRequests/request') AS cpureq(evt)
where component_name like 'query_processing'
go

-- Blocked Process Report
select blk.evt.query('.') as 'Blocked_Process_Report_XML'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/blockingTasks/blocked-process-report') AS blk(evt)
where component_name like 'query_processing'
go

-- IO
select data.value('(/ioSubsystem/@ioLatchTimeouts)[1]','bigint') as 'Latch_Timeouts',
   data.value('(/ioSubsystem/@totalLongIos)[1]','bigint') as 'Total_Long_IOs'
from SpServerDiagnosticsResult 
where component_name like 'io_subsystem'
go

-- Event information
select xevts.evt.value('(@name)','varchar(100)') as 'xEvent_Name',
   xevts.evt.value('(@package)','varchar(100)') as 'Package',
   xevts.evt.value('(@timestamp)','datetime') as 'xEvent_Time',
   xevts.evt.query('.') as 'Event Data'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/events/session/RingBufferTarget/event') AS xevts(evt)
where component_name like 'events'
go  
``` 
  
## <a name="see-also"></a>另请参阅  
 [故障转移群集实例的故障转移策略](../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
