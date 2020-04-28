---
title: sys. pdw_loader_backup_runs （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c8e7826e4dcefdbed65fb0fa1f3368411a9ef12a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68127472"
---
# <a name="syspdw_loader_backup_runs-transact-sql"></a>sys. pdw_loader_backup_runs （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含有关中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]正在进行的和已完成的备份和还原操作的信息，以及有关中[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]的正在进行的和已完成的备份、还原和加载操作的信息。 信息在两次系统重启之间仍会保留。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|特定备份、还原或负载运行的唯一标识符。<br /><br /> 此视图的键。||  
|name|**nvarchar(255)**|对于 load，为 Null。 备份或还原的可选名称。||  
|submit_time|**datetime**|提交请求的时间。||  
|start_time|**datetime**|操作开始的时间。||  
|end_time|**datetime**|操作完成、失败或已取消的时间。||  
|total_elapsed_time|**int**|已完成、已取消或失败的运行的 start_time 与当前时间之间、start_time 和 end_time 之间经过的总时间。|如果 total_elapsed_time 超过了整数的最大值24.8 （以毫秒为单位），则会导致具体化失败，因为溢出。<br /><br /> 最大值（以毫秒为单位）等效于24.8 天。|  
|operation_type|**nvarchar （16）**|负载类型。|"备份"、"加载"、"还原"|  
|mode|**nvarchar （16）**|运行类型中的模式。|对于 operation_type =**备份**<br />**DIFFERENTIAL**<br />**FULL**<br /><br /> 对于 operation_type = **LOAD**<br />**附加**<br />**刷新**<br />**UPSERT**<br /><br /> 对于 operation_type = **RESTORE**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|作为此操作的上下文的数据库的名称||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|请求操作的用户的 ID。||  
|session_id|**nvarchar(32)**|执行操作的会话的 ID。|请参阅 dm_pdw_exec_sessions sys.databases 中的 session_id [&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|request_id|**nvarchar(32)**|执行操作的请求的 ID。 对于负载，这是与此负载关联的当前或最后一个请求。|请参阅 dm_pdw_exec_requests sys.databases 中的 request_id [&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|status|**nvarchar （16）**|运行状态。|"已取消"、"已完成"、"失败"、"排队"、"正在运行"|  
|进度|**int**|已完成百分比。|0 到 100|  
|command|**nvarchar(4000)**|用户提交的命令的完整文本。|如果长度超过4000个字符，则将被截断（统计空格）。|  
|rows_processed|**bigint**|作为此操作的一部分处理的行数。||  
|rows_rejected|**bigint**|作为此操作的一部分而被拒绝的行数。||  
|rows_inserted|**bigint**|作为此操作的一部分插入到数据库表中的行数。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
