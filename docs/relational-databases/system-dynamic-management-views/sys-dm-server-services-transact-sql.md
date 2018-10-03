---
title: sys.dm_server_services (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_services
- sys.dm_server_services
- sys.dm_server_services_TSQL
- dm_server_services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_services dynamic management view
ms.assetid: 3f0defd0-478d-4e7f-96be-8795c9de4e3f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ee801da96f6281e5bf1775df1233ee85712ff74a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47856965"
---
# <a name="sysdmserverservices-transact-sql"></a>sys.dm_server_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的 SQL Server、全文和 SQL Server 代理服务的信息。 使用此动态管理视图可以报告有关这些服务的状态信息。  
  
 
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|名称[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]，全文索引或 SQL Server 代理服务。 不可为 null。|  
|startup_type|**int**|指示服务的启动模式。 以下是可能的值和其相应的说明。<br /><br /> 0： 其他<br />1： 其他<br />2： 自动<br />3： 手动<br />4： 已禁用<br /><br /> 可以为 Null。|  
|startup_desc|**nvarchar(256)**|描述服务的启动模式。 以下是可能的值和其相应的说明。<br /><br /> 其他： 其他 （引导启动）<br />其他： 其他 （系统启动）<br />自动： 自动启动<br />Manual： 按需启动<br />已禁用： 已禁用<br /><br /> 不可为 null。|  
|status|**int**|指示服务的当前状态。 以下是可能的值和其相应的说明。<br /><br /> 1： 已停止<br />2： 其他 （启动挂起）<br />3： 其他 （停止挂起）<br />4： 运行<br />5： 其他 （继续挂起）<br />6： 其他 （暂停挂起）<br />7： 已暂停<br /><br /> 可以为 Null。|  
|status_desc|**nvarchar(256)**|描述服务的当前状态。 以下是可能的值和其相应的说明。<br /><br /> 已停止： 服务已停止。<br />其他 （启动操作挂起）： 该服务正在启动。<br />其他 （停止操作挂起）： 服务正在停止。<br />正在运行： 该服务正在运行。<br />其他 （继续挂起的操作）： 该服务处于挂起状态。<br />其他 （暂停挂起）： 服务正在暂停。<br />已暂停： 服务已暂停。<br /><br /> 不可为 null。|  
|process_id|**int**|服务的进程 ID。 不可为 null。|  
|last_startup_time|**datetimeoffset(7)**|上次启动服务的日期和时间。 可以为 Null。|  
|service_account|**nvarchar(256)**|授权来控制服务的帐户。 此帐户可以启动或停止服务，或修改服务属性。 不可为 null。|  
|filename|**nvarchar(256)**|服务可执行文件的路径和文件名。 不可为 null。|  
|is_clustered|**nvarchar(1)**|指示是否将服务安装为群集服务器的资源。 不可为 null。|  
|cluster_nodename|**nvarchar(256)**|安装此服务的群集节点的名称。 可以为 Null。|
|instant_file_initialization_enabled|**nvarchar(1)**|指定是否为启用即时文件初始化[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]服务。<br /><br />Y = 为服务启用即时文件初始化。<br /><br />N = 为服务禁用即时文件初始化。<br /><br /> 可以为 Null。<br /><br /> **注意：** 不适用于 SQL Server 代理之类的其他服务。<br /><br /> **适用于：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (开头[!INCLUDE[sssql11](../../includes/sssql11-md.md)]SP4，和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。|  

## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 要求具有对服务器的 `VIEW SERVER STATE` 权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_server_registry &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  
