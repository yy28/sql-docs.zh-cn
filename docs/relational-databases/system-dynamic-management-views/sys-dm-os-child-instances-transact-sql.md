---
title: sys. dm_os_child_instances （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_child_instances
- sys.dm_os_child_instances_TSQL
- dm_os_child_instances
- dm_os_child_instances_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server state information [SQL Server]
- sys.dm_os_child_instances dynamic management view
- monitoring server health
ms.assetid: 1bef3074-0ccc-48fa-8f3d-14f3d99df86b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 59a58348f5428f568f40d28b4e83bc6bc040647c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67900236"
---
# <a name="sysdm_os_child_instances-transact-sql"></a>sys.dm_os_child_instances (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为从父服务器实例创建的每个用户实例返回一行。  
  
> **重要说明！** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 从**dm_os_child_instances sys.databases**返回的信息可用于确定每个用户实例的状态（heart_beat），并获取可以用来创建与使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 SQLCmd 的用户实例的连接的管道名称（instance_pipe_name）。 只有在外部进程（例如客户端应用程序）启动了用户实例之后，您才能连接到该用户实例。 SQL 管理工具无法启动用户实例。  
  
> **注意：** 用户实例仅是的[!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)]一项功能。  
> 
> **注意**若要从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]调用此，请使用名称**dm_pdw_nodes_os_child_instances**。  
  
|列|数据类型|说明|  
|------------|---------------|-----------------|  
|**owning_principal_name**|**nvarchar(256)**|为其创建该用户实例的用户的名称。|  
|owning_principal_sid|nvarchar(256)|拥有该用户实例的主体的 SID（安全标识符）。 它与 Windows SID 相匹配。|  
|owning_principal_sid_binary|varbinary(85)|拥有用户实例的用户的二进制版 SID。|  
|**instance_name**|**nvarchar(128)**|该用户实例的名称。|  
|**instance_pipe_name**|**nvarchar(260)**|创建用户实例时，便会创建与应用程序连接的命名管道。 可以在连接字符串中使用该名称以连接到该用户实例。|  
|**os_process_id**|**Int**|该用户实例的 Windows 进程的进程号。|  
|**os_process_creation_date**|**型**|上次启动该用户实例进程的日期和时间。|  
|**heart_beat**|**nvarchar （5）**|该用户实例的当前状态，可以是 ALIVE 或 DEAD。|  
|**pdw_node_id**|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="remarks"></a>备注  
 有关动态管理视图的详细信息，请参阅联机丛书中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的[动态管理视图和函数 &#40;transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) 。  
  
## <a name="see-also"></a>另请参阅  
 [User Instances for Non-Administrators（非管理员的用户实例）](https://msdn.microsoft.com/85385aae-10fb-4f8b-9eeb-cce2ee7da019)  
  
  



