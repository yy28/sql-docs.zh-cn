---
title: sys.dm_os_child_instances (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a57719becab0c7dda9d684e4de3218e29418b6a3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62504962"
---
# <a name="sysdmoschildinstances-transact-sql"></a>sys.dm_os_child_instances (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为从父服务器实例创建的每个用户实例返回一行。  
  
> **重要说明！** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 从返回的信息**sys.dm_os_child_instances**可用来确定每个用户实例 (heart_beat) 的状态并获取可用于创建与用户的连接的管道名称 (instance_pipe_name)使用实例的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 SQLCmd。 只有在外部进程（例如客户端应用程序）启动了用户实例之后，您才能连接到该用户实例。 SQL 管理工具无法启动用户实例。  
  
> **注意**：用户实例是一项功能[!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)]仅。  
> 
> **请注意**来调用此项从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用的名称**sys.dm_pdw_nodes_os_child_instances**。  
  
|“列”|数据类型|Description|  
|------------|---------------|-----------------|  
|**owning_principal_name**|**nvarchar(256)**|为其创建该用户实例的用户的名称。|  
|owning_principal_sid|nvarchar(256)|拥有该用户实例的主体的 SID（安全标识符）。 它与 Windows SID 相匹配。|  
|owning_principal_sid_binary|varbinary(85)|拥有用户实例的用户的二进制版 SID。|  
|**instance_name**|**nvarchar(128)**|该用户实例的名称。|  
|**instance_pipe_name**|nvarchar(260)|创建用户实例时，便会创建与应用程序连接的命名管道。 可以在连接字符串中使用该名称以连接到该用户实例。|  
|**os_process_id**|**Int**|该用户实例的 Windows 进程的进程号。|  
|**os_process_creation_date**|**日期时间**|上次启动该用户实例进程的日期和时间。|  
|**heart_beat**|**nvarchar(5)**|该用户实例的当前状态，可以是 ALIVE 或 DEAD。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="remarks"></a>备注  
 有关动态管理视图的详细信息，请参阅[动态管理视图和函数&#40;TRANSACT-SQL&#41; ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [非管理员的用户实例](https://msdn.microsoft.com/85385aae-10fb-4f8b-9eeb-cce2ee7da019)  
  
  



