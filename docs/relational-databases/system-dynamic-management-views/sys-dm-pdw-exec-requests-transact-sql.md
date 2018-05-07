---
title: sys.dm_pdw_exec_requests (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/09/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 2728c1801d0c1e61fecdbe0661f4b417d422c209
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关的所有请求的信息当前或最近中处于活动状态[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 它列出每个请求/查询的一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此视图的键。 与请求关联的唯一数字 id。|唯一跨系统中的所有请求。|  
|session_id|**nvarchar(32)**|与在其中运行此查询会话相关联的唯一数字 id。 请参阅[sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|status|**nvarchar(32)**|请求的当前状态。|正在运行，挂起、 完成、 取消、 已失败。|  
|submit_time|**datetime**|已提交的请求执行的时间。|有效**datetime**小于或等于当前时间和 start_time。|  
|start_time|**datetime**|请求执行开始时间。|对于排队请求; 为 NULL否则为有效**datetime**小于或等于当前时间。|  
|end_compile_time|**datetime**|引擎完成编译请求的时间。|对于尚未; 尚未编译的请求为 NULL否则为有效**datetime**小于 start_time 且小于或等于当前时间。|
|end_time|**datetime**|从该处请求执行将已完成、 失败或已取消的时间。|对于排队或活动的请求; 为 null否则为是有效**datetime**小于或等于当前时间。|  
|total_elapsed_time|**int**|自启动请求，以毫秒为单位，在执行过程中已用时间。|之间 0 和 start_time 和 end_time 之间的差异。<br /><br /> 如果 total_elapsed_time 超过一个整数的最大值，total_elapsed_time 将继续是最大值。 这种情况将生成警告"的最大值已超出。"<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|标签|**nvarchar(255)**|与 SELECT 查询的一些语句关联的可选标签字符串。|任何字符串包含 a-z、 A-Z、"0-9、 _。|  
|error_id|**nvarchar(36)**|如果有与此请求相关联的错误的唯一 id。|请参阅[sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); 设置为 NULL，如果未发生错误。|  
|database_id|**int**|显式上下文 (例如，使用 DB_X) 使用的数据库的标识符。|在中看到 id [sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|command|**nvarchar(4000)**|包含由用户提交的请求的完整文本。|任何有效的查询或请求文本。 查询的长度大于 4000 个字节将被截断。|  
|resource_class|**nvarchar(20)**|用于此请求的资源类。 请参阅相关**concurrency_slots_used**中[sys.dm_pdw_resource_waits &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)。|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
 有关通过此视图保留最大行数的信息，请参阅"最小值和最大值"中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="permissions"></a>权限  
 需要 VIEW SERVER STATE 权限。  
  
## <a name="security"></a>Security  
 sys.dm_pdw_exec_requests 不筛选查询结果根据特定于数据库的权限。 与 VIEW SERVER STATE 权限的登录名可以获取结果的所有数据库的查询结果  
  
> [!WARNING]  
>  攻击者可以使用 sys.dm_pdw_exec_requests 可通过只需具有 VIEW SERVER STATE 权限以及不具有特定于数据库的权限检索有关特定数据库对象的信息。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
