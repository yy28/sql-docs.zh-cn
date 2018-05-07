---
title: sys.dm_os_waiting_tasks (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_waiting_tasks
- sys.dm_os_waiting_tasks_TSQL
- dm_os_waiting_tasks_TSQL
- sys.dm_os_waiting_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_waiting_tasks dynamic management view
ms.assetid: ca5e6844-368c-42e2-b187-6e5f5afc8df3
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a44e9fe9e42f415ac7f859c25be95800ff0b1393
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmoswaitingtasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回有关正在等待某些资源的任务的等待队列的信息。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_waiting_tasks**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|等待任务的地址。|  
|**session_id**|**int**|与任务关联的会话的 ID。|  
|**exec_context_id**|**int**|与任务关联的执行上下文的 ID。|  
|**wait_duration_ms**|**bigint**|此等待类型的总等待时间（毫秒）。 此时间是包括**signal_wait_time**。|  
|**wait_type**|**nvarchar(60)**|等待类型的名称。|  
|**resource_address**|**varbinary(8)**|任务等待的资源的地址。|  
|**blocking_task_address**|**varbinary(8)**|当前持有此资源的任务。|  
|**blocking_session_id**|**int**|正在阻塞请求的会话的 ID。 如果此列为 NULL，则表示请求未被阻塞，或锁定会话的会话信息不可用（或无法进行标识）。<br /><br /> -2 = 阻塞资源由孤立的分布式事务拥有。<br /><br /> -3 = 阻塞资源由延迟的恢复事务拥有。<br /><br /> -4 = 由于内部闩锁状态转换而无法确定阻塞闩锁所有者的会话 ID。|  
|**blocking_exec_context_id**|**int**|正在阻塞的任务的执行上下文 ID。|  
|**resource_description**|**nvarchar(3072)**|对正在占用的资源的说明。 有关详细信息，请参阅下面的列表。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="resourcedescription-column"></a>resource_description 列  
 Resource_description 列具有以下可能的值。  
  
 **线程池资源所有者：**  
  
-   线程池 id = 计划程序\<十六进制地址 >  
  
 **并行查询资源所有者：**  
  
-   exchangeEvent id = {端口 |管道}\<十六进制地址 > WaitType =\<exchange 等待类型 > nodeId =\<exchange 节点 id >  
  
 **Exchange 等待类型：**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **锁资源所有者：**  
  
-   \<类型特定说明 > id = 锁\<锁十六进制地址 > 模式 =\<模式 > associatedObjectId =\<关联 obj id >  
  
     **\<类型特定说明 > 可以是：**  
  
    -   对于数据库： databaselock 子资源 =\<databaselock 子资源 > dbid =\<db id >  
  
    -   对于文件： filelock fileid =\<文件 id > 子资源 =\<filelock 子资源 > dbid =\<db id >  
  
    -   对象： objectlock lockPartition =\<锁分区 id > objid =\<obj id > 子资源 =\<objectlock 子资源 > dbid =\<db id >  
  
    -   页： pagelock fileid =\<文件 id > pageid =\<页 id > dbid =\<db id > 子资源 =\<pagelock 子资源 >  
  
    -   键： 键锁 hobtid =\<hobt id > dbid =\<db id >  
  
    -   以便范围： extentlock fileid =\<文件 id > pageid =\<页 id > dbid =\<db id >  
  
    -   有关 RID: ridlock fileid =\<文件 id > pageid =\<页 id > dbid =\<db id >  
  
    -   对于应用程序： applicationlock 哈希 =\<哈希 > databasePrincipalId =\<角色 id > dbid =\<db id >  
  
    -   元数据： metadatalock 子资源 =\<子资源的元数据 > classid =\<metadatalock 说明 > dbid =\<db id >  
  
    -   有关 HOBT: hobtlock hobtid =\<hobt id > 子资源 =\<hobt 子资源 > dbid =\<db id >  
  
    -   有关 ALLOCATION_UNIT: allocunitlock hobtid =\<hobt id > 子资源 =\<子资源单元分配 > dbid =\<db id >  
  
     **\<模式 > 可以是：**  
  
     Sch-S、Sch-M、S、U、X、IS、IU、IX、SIU、SIX、UIX、BU、RangeS-S、RangeS-U、RangeI-N、RangeI-S、RangeI-U、RangeI-X、RangeX-、RangeX-U、RangeX-X  
  
 **外部资源所有者：**  
  
-   外部 ExternalResource =\<等待类型 >  
  
 **通用资源所有者：**  
  
-   TransactionMutex TransactionInfo 工作区 =\<工作区 id >  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **闩锁资源所有者：**  
  
-   \<数据库 id >:\<文件 id >:\<页面中文件 >  
  
-   \<GUID &GT;  
  
-   \<闩锁类 > (\<闩锁地址 >)  
  
## <a name="permissions"></a>权限

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
 
## <a name="example"></a>示例
此示例将标识已阻塞的会话。  执行[!INCLUDE[tsql](../../includes/tsql-md.md)]查询中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>另请参阅  
  [SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


