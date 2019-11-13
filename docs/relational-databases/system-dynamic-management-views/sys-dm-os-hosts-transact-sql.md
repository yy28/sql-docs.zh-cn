---
title: sys. dm_os_hosts （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_hosts_TSQL
- dm_os_hosts
- dm_os_hosts_TSQL
- sys.dm_os_hosts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_hosts dynamic management view
ms.assetid: a313ff3b-1fe9-421e-b94b-cea19c43b0e5
author: stevestein
ms.author: sstein
ms.openlocfilehash: e4ff3e25accf5c499afb5e306a0eec206f6b3f82
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982546"
---
# <a name="sysdm_os_hosts-transact-sql"></a>sys.dm_os_hosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回当前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中注册的所有主机。 该视图还返回这些主机使用的资源。  
  
> [!NOTE]  
>  若要从 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 或 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中调用此名称，请使用名称**sys.databases. dm_pdw_nodes_os_hosts**。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary(8)**|主机对象的内部内存地址。|  
|**type**|**nvarchar(60)**|宿主组件的类型。 例如，应用于对象的<br /><br /> SOSHOST_CLIENTID_SERVERSNI = SQL Server 本机接口<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = SQL Server Native Client OLE DB 访问接口<br /><br /> SOSHOST_CLIENTID_MSDART = Microsoft 数据访问运行时|  
|**名称**|**nvarchar(32)**|主机名称。|  
|**enqueued_tasks_count**|**int**|该主机放置到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的队列上的任务总数。|  
|**active_tasks_count**|**int**|该主机放在队列中的、正在运行的任务数。|  
|**completed_ios_count**|**int**|通过该主机发出和完成的 I/O 总数。|  
|**completed_ios_in_bytes**|**bigint**|通过该主机完成的 I/O 字节总数。|  
|**active_ios_count**|**int**|与该主机相关的、当前正在等待完成的 I/O 请求总数。|  
|**default_memory_clerk_address**|**varbinary(8)**|与该主机相关的内存分配器对象的内存地址。 有关详细信息，请参阅[sys. &#40;dm_os_memory_clerks transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)。|  
|pdw_node_id|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="permissions"></a>Permissions

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上，需要 `VIEW SERVER STATE` 权限。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 高级层上，需要数据库中的 `VIEW DATABASE STATE` 权限。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 标准层和基本层上，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   

## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可执行文件一部分的组件（如 OLE DB 访问接口）分配内存并加入非抢先计划。 这些组件由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 承载，而且由这些组件分配的所有资源都被跟踪。 通过承载这些组件，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以更好地顾及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可执行文件外部的组件所用的资源。  
  
## <a name="relationship-cardinalities"></a>关系基数  
  
|从|若要|“关系”|  
|----------|--------|------------------|  
|sys.dm_os_hosts. default_memory_clerk_address|sys.dm_os_memory_clerks. memory_clerk_address|一对一|  
|sys.dm_os_hosts. host_address|sys.dm_os_memory_clerks. host_address|一对一|  
  
## <a name="examples"></a>示例  
 以下示例可确定由宿主组件调配的内存总量。  
  
||  
|-|  
|**适用于**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更高版本。|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>另请参阅  

 [sys. dm_os_memory_clerks &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [与操作系统相关的动态管理视图&#40;SQL Server transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


