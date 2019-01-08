---
title: sys.dm_io_pending_io_requests (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 71fb4daabcdb0eef03e615f595df20d555673a24
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2019
ms.locfileid: "53980203"
---
# <a name="sysdmiopendingiorequests-transact-sql"></a>sys.dm_io_pending_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中每个挂起的 I/O 请求返回一行。  
  
> [!NOTE]  
>  若要调用此项从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_io_pending_io_requests**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**io_completion_request_address**|**varbinary(8)**|IO 请求的内存地址。 不可为 null。|  
|**io_type**|**nvarchar(60)**|挂起的 IO 请求的类型。 不可为 null。|  
|**io_pending_ms_ticks**|**bigint**|仅限内部使用。 不可为 null。| 
|**io_pending**|**int**|指示 IO 请求被挂起还是已由 Windows 完成。 即使在 Windows 已完成 I/O 请求但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尚未执行上下文切换（在其中处理 I/O 请求并将其从此列表中删除）时，I/O 请求仍可处于挂起状态。 不可为 null。|  
|**io_completion_routine_address**|**varbinary(8)**|I/O 请求完成时调用的内部函数。 可以为 Null。|  
|**io_user_data_address**|**varbinary(8)**|仅限内部使用。 可以为 Null。|  
|**scheduler_address**|**varbinary(8)**|发出此 I/O 请求的计划程序。 I/O 请求将显示于计划程序的挂起 I/O 列表中。 有关详细信息，请参阅[sys.dm_os_schedulers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)。 不可为 null。|  
|**io_handle**|**varbinary(8)**|I/O 请求中所使用文件的文件句柄。 可以为 Null。|  
|**io_offset**|**bigint**|IO 请求的偏移量。 不可为 null。|  
|**io_handle_path**|**nvarchar(256)**| I/O 请求中使用的文件的路径。 可以为 Null。|
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [我 O 相关动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


