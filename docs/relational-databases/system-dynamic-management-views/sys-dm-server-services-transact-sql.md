---
title: "sys.dm_server_services (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/28/2017
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
- dm_server_services
- sys.dm_server_services
- sys.dm_server_services_TSQL
- dm_server_services_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_server_services dynamic management view
ms.assetid: 3f0defd0-478d-4e7f-96be-8795c9de4e3f
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8642cd9036fcaf7835c6dffc01f60817bdaa82bb
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmserverservices-transact-sql"></a>sys.dm_server_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的 SQL Server、全文和 SQL Server 代理服务的信息。 使用此动态管理视图可以报告有关这些服务的状态信息。  
  
 
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|SQL Server、全文和 SQL Server 代理服务的名称。 不可为 null。|  
|startup_type|**int**|指示服务的启动模式。 以下是可能的值以及及其相应的说明。<br /><br /> 0： 其他<br />1： 其他<br />2： 自动<br />3： 手动<br />4： 已禁用<br /><br /> 可以为 Null。|  
|startup_desc|**nvarchar(256)**|描述服务的启动模式。 以下是可能的值以及及其相应的说明。<br /><br /> 其他： 其他 （引导启动）<br />其他： 其他 （系统启动）<br />自动： 自动启动<br />启动手动： 要求<br />已禁用： 已禁用<br /><br /> 不可为 null。|  
|status|**int**|指示服务的当前状态。 以下是可能的值以及及其相应的说明。<br /><br /> 1： 已停止<br />2： 其他 （启动挂起）<br />3： 其他 （停止挂起）<br />4： 运行<br />5： 其他 （继续挂起）<br />6： 其他 （暂停挂起）<br />7： 暂停<br /><br /> 可以为 Null。|  
|status_desc|**nvarchar(256)**|描述服务的当前状态。 以下是可能的值以及及其相应的说明。<br /><br /> 服务已停止： 已停止。<br />其他 （启动操作挂起）： 服务正在启动。<br />其他 （停止操作挂起）： 服务正在停止。<br />运行： 服务正在运行。<br />其他 （继续挂起的操作）： 该服务处于挂起状态。<br />其他 （暂停挂起）： 服务正在暂停。<br />已暂停： 服务已暂停。<br /><br /> 不可为 null。|  
|process_id|**int**|服务的进程 ID。 不可为 null。|  
|last_startup_time|**datetimeoffset(7)**|上次启动服务的日期和时间。 可以为 Null。|  
|service_account|**nvarchar(256)**|授权来控制服务的帐户。 此帐户可以启动或停止服务，或修改服务属性。 不可为 null。|  
|filename|**nvarchar(256)**|服务可执行文件的路径和文件名。 不可为 null。|  
|is_clustered|**nvarchar(1)**|指示是否安装了服务，为群集服务器的资源。 不可为 null。|  
|cluster_nodename|**nvarchar(256)**|安装此服务的群集节点的名称。 可以为 Null。|
|instant_file_initialization_enabled|**nvarchar(1)**|**适用于： [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4，且开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1**。<br /><br />指定是否为 SQL Server 数据库引擎服务启用即时文件初始化。 此属性不适用于服务 (示例： SQL Server 代理) 除 SQL Server 数据库引擎服务以外。 可以为 null。<br /><br />Y = 为服务启用即时文件初始化。<br /><br />N = 即时文件初始化禁用服务。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 要求具有对服务器的 `VIEW SERVER STATE` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_server_registry &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  
  
