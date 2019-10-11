---
title: sys.databases _os_waiting_tasks （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0a89a48fa960812ee955cd3b7ecb30069161f61
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2019
ms.locfileid: "72260381"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回有关正在等待某些资源的任务的等待队列的信息。 有关任务的详细信息，请参阅[线程和任务体系结构指南](../../relational-databases/thread-and-task-architecture-guide.md)。
   
> [!NOTE]  
>  若要从 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 或 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 调用此项，请使用名称 **_pdw_nodes_os_waiting_tasks**。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|等待任务的地址。|  
|**session_id**|**smallint**|与任务关联的会话的 ID。|  
|**exec_context_id**|**int**|与任务关联的执行上下文的 ID。|  
|**wait_duration_ms**|**bigint**|此等待类型的总等待时间（毫秒）。 此时间包含**signal_wait_time**。|  
|**wait_type**|**nvarchar(60)**|等待类型的名称。|  
|**resource_address**|**varbinary(8)**|任务等待的资源的地址。|  
|**blocking_task_address**|**varbinary(8)**|当前持有此资源的任务。|  
|**blocking_session_id**|**smallint**|正在阻塞请求的会话的 ID。 如果此列为 NULL，则表示请求未被阻塞，或锁定会话的会话信息不可用（或无法进行标识）。<br /><br /> -2 = 阻塞资源由孤立的分布式事务拥有。<br /><br /> -3 = 阻塞资源由延迟的恢复事务拥有。<br /><br /> -4 = 由于内部闩锁状态转换而无法确定阻塞闩锁所有者的会话 ID。|  
|**blocking_exec_context_id**|**int**|正在阻塞的任务的执行上下文 ID。|  
|**resource_description**|**nvarchar(3072)**|对正在占用的资源的说明。 有关详细信息，请参阅下面的列表。|  
|**pdw_node_id**|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="resource_description-column"></a>resource_description 列  
 Resource_description 列具有以下可能值。  
  
 **线程池资源所有者：**  
  
-   threadpool id = no__t-0hex-address >  
  
 **并行查询资源所有者：**  
  
-   exchangeEvent id={Port|Pipe}\<hex-address> WaitType=\<exchange-wait-type> nodeId=\<exchange-node-id>  
  
 **交换-等待类型：**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **锁定资源所有者：**  
  
-   \<type-specific-description> id=lock\<lock-hex-address> mode=\<mode> associatedObjectId=\<associated-obj-id>  
  
     **\<type-说明 > 可以：**  
  
    -   对于数据库： databaselock subresource = \<databaselock-subresource > dbid = \<db-id >  
  
    -   对于 FILE： filelock fileid = \<file > subresource = \<filelock-subresource > dbid = \<db-id >  
  
    -   对于 OBJECT： k lockPartition = \<lock > objid = \<obj-id > subresource = \<objectlock-subresource > dbid = \<db-id >  
  
    -   对于 PAGE： pagelock fileid = \<file > pageid = \<page > dbid = \<db-id > subresource = \<pagelock-subresource >  
  
    -   对于密钥：键锁 hobtid = \<hobt > dbid = \<db >  
  
    -   对于区： extentlock fileid = \<file > pageid = \<page > dbid = \<db-id >  
  
    -   对于 RID： ridlock fileid = \<file > pageid = \<page > dbid = \<db-id >  
  
    -   对于应用程序： applicationlock hash = \<hash > databasePrincipalId = \<role > dbid = \<db-id >  
  
    -   对于元数据： k subresource = \<metadata-subresource > classid = \<metadatalock > dbid = \<db-id >  
  
    -   对于 HOBT： hobtlock hobtid = \<hobt > subresource = \<hobt-subresource > dbid = \<db-id >  
  
    -   对于 ALLOCATION_UNIT： allocunitlock hobtid = \<hobt > subresource = \<alloc > dbid = subresource id @no__t  
  
     **\<mode > 可以：**  
  
     Sch-S、Sch-M、S、U、X、IS、IU、IX、SIU、SIX、UIX、BU、RangeS-S、RangeS-U、RangeI-N、RangeI-S、RangeI-U、RangeI-X、RangeX-、RangeX-U、RangeX-X  
  
 **外部资源所有者：**  
  
-   External ExternalResource = \<wait >  
  
 **一般资源所有者：**  
  
-   TransactionMutex TransactionInfo 工作区 = \<workspace >  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **闩锁资源所有者：**  
  
-   @no__t 0db >： @no__t-id >： \<page 文件中 >  
  
-   \<GUID >  
  
-   \<latch-class> (\<latch-address>)  
  
## <a name="permissions"></a>权限

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 上，需要 @no__t 权限。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 高级层上，需要数据库中的 @no__t 1 权限。 在 @no__t 标准层和基本层上，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   
 
## <a name="example"></a>示例
此示例将标识已阻止的会话。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中执行 @no__t 查询。

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>请参阅  
[与操作系统相关的动态管理视图&#40;SQL Server transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[线程和任务体系结构指南](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
