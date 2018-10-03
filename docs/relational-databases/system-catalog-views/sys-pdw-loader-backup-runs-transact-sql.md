---
title: sys.pdw_loader_backup_runs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d8675de8ff7931753d20e99d5c0d61151192e5b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47751585"
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含有关正在进行和已完成的备份和还原操作中的信息[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，以及有关正在进行和已完成的备份、 还原和加载操作中的[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 信息在两次系统重启之间仍会保留。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|为特定的备份、 还原或负载运行的唯一标识符。<br /><br /> 此视图的键。||  
|NAME|**nvarchar(255)**|对于负载为 null。 为备份或还原的可选名称。||  
|submit_time|**datetime**|提交请求的时间。||  
|start_time|**datetime**|启动操作的时间。||  
|end_time|**datetime**|该操作已完成、 失败或已取消的时间。||  
|total_elapsed_time|**int**|总运行时间或 start_time 和 end_time start_time 和当前时间之间的已完成的已取消，或失败的运行。|如果 total_elapsed_time 超过一个整数 （以毫秒为单位的 24.8 天） 的最大值，它将导致具体化失败由于溢出。<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|operation_type|**nvarchar(16)**|负载类型。|备份，加载，还原|  
|mode|**nvarchar(16)**|在运行类型模式。|Operation_type =**备份**<br />**差异**<br />**FULL**<br /><br /> Operation_type =**负载**<br />**追加**<br />**重新加载**<br />**更新插入**<br /><br /> Operation_type =**还原**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|此操作的上下文的数据库的名称||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|请求操作的用户 ID。||  
|session_id|**nvarchar(32)**|执行该操作的会话 ID。|请参阅中的 session_id [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|request_id|**nvarchar(32)**|执行该操作的请求 ID。 对于负载，这是与此负载关联的当前或上一请求...|请参阅中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|status|**nvarchar(16)**|运行的状态。|取消，已完成，失败、 已排队、 正在运行|  
|进度|**int**|已完成的百分比。|0 到 100|  
|command|**nvarchar(4000)**|由用户提交的命令的完整文本。|如果长度超过 4000 个字符 （计算空格数），将被截断。|  
|rows_processed|**bigint**|此操作的一部分处理的行数。||  
|rows_rejected|**bigint**|此操作的一部分，已被拒绝的行数。||  
|rows_inserted|**bigint**|此操作的一部分插入到数据库表的行数。||  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
