---
title: sys.pdw_loader_backup_runs (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
caps.latest.revision: 10
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c9de90ab3777e8f432f29cb16002e629862f12f3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181803"
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含有关正在进行的和已完成的备份和还原操作中的信息[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，以及有关正在进行的和已完成的备份、 还原和加载操作中的[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 信息在两次系统重启之间仍会保留。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|有关特定备份、 还原或运行的负载的唯一标识符。<br /><br /> 此视图的键。||  
|name|**nvarchar(255)**|负载的为 null。 为备份或还原的可选名称。||  
|submit_time|**datetime**|已提交的请求的时间。||  
|start_time|**datetime**|时间操作已开始。||  
|end_time|**datetime**|该操作已完成、 失败或已取消的时间。||  
|total_elapsed_time|**int**|总运行时间之间 start_time 和当前时间之间 start_time 和 end_time 或已完成的、 已取消，或未运行。|如果 total_elapsed_time 超过一个整数 （以毫秒为单位的 24.8 天） 的最大值，它将导致具体化失败由于溢出。<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|operation_type|**nvarchar(16)**|负载类型中。|备份，加载、 还原|  
|mode|**nvarchar(16)**|在运行的类型内模式。|对于 operation_type =**备份**<br />**差异**<br />**FULL**<br /><br /> 对于 operation_type =**负载**<br />**追加**<br />**重新加载**<br />**UPSERT**<br /><br /> 对于 operation_type =**还原**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|为此操作的上下文的数据库名称||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|请求操作的用户 ID。||  
|session_id|**nvarchar(32)**|执行该操作的会话 ID。|请参阅中的 session_id [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|request_id|**nvarchar(32)**|执行该操作的请求的 ID。 对于负载，这是与此负载关联的当前或最后一个请求...|请参阅中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|status|**nvarchar(16)**|运行状态。|取消，完成，已失败、 排队、 正在运行|  
|进度|**int**|已完成的百分比。|0 到 100|  
|command|**nvarchar(4000)**|由用户提交的命令的完整文本。|如果超过 4000 个字符 （包括空格），将被截断。|  
|rows_processed|**bigint**|作为此操作的一部分处理的行数。||  
|rows_rejected|**bigint**|此操作的一部分的拒绝的行数。||  
|rows_inserted|**bigint**|作为此操作的一部分插入到数据库表的行数。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
