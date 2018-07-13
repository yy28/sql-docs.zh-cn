---
title: sys.dm_pdw_exec_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 966fbd2efde6934f8cfe1b59706dec27b92e301e
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926138"
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关的所有请求的信息当前或最近中处于活动状态[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 它列出了每个请求/查询对应一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此视图的键。 与请求关联的唯一数字 id。|在系统中的所有请求之间是唯一的。|  
|session_id|**nvarchar(32)**|与在其中运行此查询的会话相关联的唯一数字 id。 请参阅[sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|status|**nvarchar(32)**|请求的当前状态。|正在运行、 挂起、 已完成、 取消、 失败。|  
|submit_time|**datetime**|提交请求执行的时间。|有效**datetime**小于或等于当前时间和 start_time。|  
|start_time|**datetime**|请求执行开始时间。|对于排队的请求; 值为 NULL否则为有效**datetime**小于或等于当前时间。|  
|end_compile_time|**datetime**|引擎完成编译请求的时间。|对于尚未; 尚未编译的请求为 NULL否则为有效**datetime**小于 start_time 且小于或等于当前时间。|
|end_time|**datetime**|时间的请求执行将已完成、 失败或已取消。|对于排队或处于活动状态的请求; 值为 null否则为有效**datetime**小于或等于当前时间。|  
|total_elapsed_time|**int**|启动请求，以毫秒为单位后，在执行过程中已用时间。|介于 0 和 start_time 和 end_time 之间的差异。<br /><br /> 如果 total_elapsed_time 超出整数的最大值，将持续 total_elapsed_time 可最大值。 这种情况会生成警告"的最大值已超出。"<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|标签|**nvarchar(255)**|与 SELECT 查询的一些语句相关联的可选标签字符串。|任何字符串包含 a-z、 A-Z、"0-9、 _。|  
|error_id|**nvarchar(36)**|如果有与请求关联的错误的唯一 id。|请参阅[sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); 如果没有出现任何错误设置为 NULL。|  
|database_id|**int**|显式上下文 (例如，使用 DB_X) 使用的数据库的标识符。|请参阅中的 id [sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|command|**nvarchar(4000)**|包含用户提交的请求的完整文本。|任何有效的查询或请求文本。 长度超过 4000 字节的查询将被截断。|  
|resource_class|**nvarchar(20)**|用于此请求的资源类。 请参阅相关**concurrency_slots_used**中[sys.dm_pdw_resource_waits &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)。|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
 此视图按保留的最大行有关的信息，请参阅"最小值和最大值"中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="permissions"></a>权限  
 需要 VIEW SERVER STATE 权限。  
  
## <a name="security"></a>Security  
 sys.dm_pdw_exec_requests 不筛选查询结果根据特定于数据库的权限。 具有 VIEW SERVER STATE 权限的登录名可以获取结果的所有数据库的查询结果  
  
> [!WARNING]  
>  攻击者可以使用 sys.dm_pdw_exec_requests 来检索有关特定数据库对象的信息，通过只需具有 VIEW SERVER STATE 权限以及不具有特定于数据库的权限。  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
