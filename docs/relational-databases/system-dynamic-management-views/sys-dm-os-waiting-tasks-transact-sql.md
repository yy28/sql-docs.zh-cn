---
title: sys. dm_os_waiting_tasks （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f0efa4a5b5c8144807c27014a96b3fa90ed77971
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82811735"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回有关正在等待某些资源的任务的等待队列的信息。 有关任务的详细信息，请参阅[线程和任务体系结构指南](../../relational-databases/thread-and-task-architecture-guide.md)。
   
> [!NOTE]  
>  若要从或调用此 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ，请使用名称**dm_pdw_nodes_os_waiting_tasks**。  
  
|列名称|数据类型|说明|  
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
|**resource_description**|**nvarchar （3072）**|对正在占用的资源的说明。 有关详细信息，请参阅下面的列表。|  
|**pdw_node_id**|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="resource_description-column"></a>resource_description 列  
 resource_description 列具有以下可能值。  
  
 **线程池资源所有者：**  
  
-   threadpool id = 计划程序 \< 十六进制-地址>  
  
 **并行查询资源所有者：**  
  
-   exchangeEvent id = {Port |管道} \< hex-address> WaitType = \< exchange-wait> 节点 \<> id =  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **锁资源所有者：**  
  
-   \<特定于类型的说明> id = 锁 \< 锁-十六进制地址> mode = \< Mode> associatedObjectId = \< 关联的 obj-id>  
  
     **\<特定于类型的描述> 可以是：**  
  
    -   对于数据库： databaselock subresource = \< databaselock-subresource> dbid = \< db id>  
  
    -   对于 FILE： filelock fileid = \< file-id> subresource = \< filelock-subresource> dbid = \< db id>  
  
    -   对于 OBJECT： k lockPartition = \< objid => = \< obj-id> subresource = \< k-subresource> dbid = \< db id>  
  
    -   对于 PAGE： pagelock fileid = \< file id> pageid = \< PAGE id> dbid = \< db id> subresource = \< pagelock-subresource>  
  
    -   对于密钥：键锁 hobtid = \< hobt> dbid = \< db id>  
  
    -   对于区： extentlock fileid = \< file id> pageid = \< page id> dbid = \< db id>  
  
    -   对于 RID： ridlock fileid = \< file id> pageid = \< page id> dbid = \< db id>  
  
    -   对于应用程序： applicationlock hash = \< hash> databasePrincipalId = \< role-id> dbid = \< db id>  
  
    -   对于元数据： k subresource = \< metadata-subresource> classid = \< k-description> dbid = \< db id>  
  
    -   对于 HOBT： hobtlock hobtid = \< HOBT> subresource = \< HOBT-subresource> dbid = \< db id>  
  
    -   对于 ALLOCATION_UNIT： allocunitlock hobtid = \< hobt> subresource = \< 分配单元-subresource> dbid = \< 数据库 id>  
  
     **\<模式> 可以是：**  
  
     Sch-S、Sch-M、S、U、X、IS、IU、IX、SIU、SIX、UIX、BU、RangeS-S、RangeS-U、RangeI-N、RangeI-S、RangeI-U、RangeI-X、RangeX-、RangeX-U、RangeX-X  
  
 **外部资源所有者：**  
  
-   External ExternalResource = \< wait>  
  
 **常规资源所有者：**  
  
-   TransactionMutex TransactionInfo 工作区 = \< 工作区 id>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **闩锁资源所有者：**  
  
-   \<db id>： \< 文件 id>： \< 页面内文件>  
  
-   \<GUID>  
  
-   \<闩锁-类> （ \< 闩锁-地址>）  
  
## <a name="permissions"></a>权限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 权限。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 高级层上，需要具有 `VIEW DATABASE STATE` 数据库中的权限。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 标准层和基本层上，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   
 
## <a name="example"></a>示例
此示例将标识已阻止的会话。 [!INCLUDE[tsql](../../includes/tsql-md.md)]在中执行查询 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>另请参阅  
[&#40;Transact-sql 的与操作系统相关的动态管理视图 SQL Server&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[线程和任务体系结构指南](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
