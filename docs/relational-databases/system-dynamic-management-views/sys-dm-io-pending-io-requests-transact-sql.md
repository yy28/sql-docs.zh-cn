---
description: sys.dm_io_pending_io_requests (Transact-SQL)
title: sys. dm_io_pending_io_requests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_pending_io_requests
- dm_io_pending_io_requests
- dm_io_pending_io_requests_TSQL
- sys.dm_io_pending_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_pending_io_requests dynamic management view
ms.assetid: d1fb46dd-5c74-4c04-9ecf-8934b1bedb5b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 69f544c80718611ab56d8535a714c360a58870ee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419671"
---
# <a name="sysdm_io_pending_io_requests-transact-sql"></a>sys.dm_io_pending_io_requests (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中每个挂起的 I/O 请求返回一行。  
  
> [!NOTE]  
>  若要从或调用此 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ，请使用名称 **dm_pdw_nodes_io_pending_io_requests**。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**io_completion_request_address**|**varbinary(8)**|IO 请求的内存地址。 不可为 null。|  
|**io_type**|**nvarchar(60)**|挂起的 IO 请求的类型。 不可为 null。|  
|**io_pending_ms_ticks**|**bigint**|仅限内部使用。 不可为 null。| 
|**io_pending**|**int**|指示 IO 请求被挂起还是已由 Windows 完成。 即使在 Windows 已完成 I/O 请求但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尚未执行上下文切换（在其中处理 I/O 请求并将其从此列表中删除）时，I/O 请求仍可处于挂起状态。 不可为 null。|  
|**io_completion_routine_address**|**varbinary(8)**|I/O 请求完成时调用的内部函数。 可以为 Null。|  
|**io_user_data_address**|**varbinary(8)**|仅限内部使用。 可以为 Null。|  
|**scheduler_address**|**varbinary(8)**|发出此 I/O 请求的计划程序。 I/O 请求将显示于计划程序的挂起 I/O 列表中。 有关详细信息，请参阅 [sys.databases&#41;dm_os_schedulers &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)。 不可为 null。|  
|**io_handle**|**varbinary(8)**|I/O 请求中所使用文件的文件句柄。 可以为 Null。|  
|**io_offset**|**bigint**|IO 请求的偏移量。 不可为 null。|  
|**io_handle_path**|**nvarchar(256)**| I/o 请求中使用的文件的路径。 可以为 Null。|
|pdw_node_id|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="permissions"></a>权限  

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 权限。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 高级层上，需要具有 `VIEW DATABASE STATE` 数据库中的权限。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 标准层和基本层上，需要  **服务器管理员** 或 **Azure Active Directory 管理员** 帐户。   
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与 SQL&#41;相关的动态管理视图和函数 &#40;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


