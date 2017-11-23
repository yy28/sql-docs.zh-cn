---
title: "sys.dm_os_hosts (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_hosts_TSQL
- dm_os_hosts
- dm_os_hosts_TSQL
- sys.dm_os_hosts
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_hosts dynamic management view
ms.assetid: a313ff3b-1fe9-421e-b94b-cea19c43b0e5
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8aebdc1e911e9b42974f96a83a5ce1b08348099d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmoshosts-transact-sql"></a>sys.dm_os_hosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回当前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中注册的所有主机。 该视图还返回这些主机使用的资源。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_hosts**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary （8)**|主机对象的内部内存地址。|  
|**type**|**nvarchar(60)**|宿主组件的类型。 例如：<br /><br /> SOSHOST_CLIENTID_SERVERSNI = SQL Server 本机接口<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = SQL Server Native Client OLE DB 访问接口<br /><br /> SOSHOST_CLIENTID_MSDART = Microsoft 数据访问运行时|  
|**名称**|**nvarchar(32)**|主机名称。|  
|**enqueued_tasks_count**|**int**|该主机放置到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的队列上的任务总数。|  
|**active_tasks_count**|**int**|该主机放在队列中的、正在运行的任务数。|  
|**completed_ios_count**|**int**|通过该主机发出和完成的 I/O 总数。|  
|**completed_ios_in_bytes**|**bigint**|通过该主机完成的 I/O 字节总数。|  
|**active_ios_count**|**int**|与该主机相关的、当前正在等待完成的 I/O 请求总数。|  
|**default_memory_clerk_address**|**varbinary （8)**|与该主机相关的内存分配器对象的内存地址。 有关详细信息，请参阅[sys.dm_os_memory_clerks &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>Permissions  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层，需要`VIEW DATABASE STATE`数据库中的权限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准版和基本层，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可执行文件一部分的组件（如 OLE DB 访问接口）分配内存并加入非抢先计划。 这些组件由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 承载，而且由这些组件分配的所有资源都被跟踪。 通过承载这些组件，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以更好地顾及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可执行文件外部的组件所用的资源。  
  
## <a name="relationship-cardinalities"></a>关系基数  
  
|从|若要|关系|  
|----------|--------|------------------|  
|sys.dm_os_hosts. default_memory_clerk_address|sys.dm_os_memory_clerks. memory_clerk_address|一对一|  
|sys.dm_os_hosts. host_address|sys.dm_os_memory_clerks. host_address|一对一|  
  
## <a name="examples"></a>示例  
 以下示例可确定由宿主组件调配的内存总量。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>另请参阅  

 [sys.dm_os_memory_clerks &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [SQL Server 操作系统相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


