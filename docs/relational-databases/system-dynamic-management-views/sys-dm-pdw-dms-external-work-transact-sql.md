---
title: sys.dm_pdw_dms_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d02a1d50e9c7a5f906e78fa6753d594edced341f
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658113"
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>sys.dm_pdw_dms_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 保存有关外部操作的所有数据移动服务 (DMS) 步骤的信息的系统视图。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|使用此 DMS 辅助进程的查询。<br /><br /> request_id、 step_index 和 dms_step_index 构成此视图的键。|与中的 request_id 相同[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|调用此 DMS 辅助进程的查询步骤。<br /><br /> request_id、 step_index 和 dms_step_index 构成此视图的键。|相同中 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|dms_step_index|**int**|DMS 计划中的当前步骤。<br /><br /> request_id、 step_index 和 dms_step_index 构成此视图的键。|相同中 dms___step_index [sys.dm_pdw_dms_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)。|  
|pdw_node_id|**int**|正在运行的 DMS 辅助角色节点。|相同中找到 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|type|**nvarchar(60)**|此节点正在运行的外部操作的类型。<br /><br /> 文件拆分是已拆分为多个较小降到外部 Hadoop 文件上的操作。|文件拆分|  
|work_id|**int**|该文件拆分 id。|大于或等于 0。<br /><br /> 每个计算节点是唯一的。|  
|input_name|**nvarchar(60)**|正在读取的输入的名称的字符串。|对于 Hadoop 文件，这是 Hadoop 文件名称。|  
|read_location|**bigint**|读取位置的偏移量。||  
|estimated_bytes_processed|**bigint**|通过此工作线程处理的字节数。|大于或等于 0。|  
|长度|**bigint**|文件拆分中的字节数。<br /><br /> 对于 Hadoop，这是 HDFS 块的大小。|用户定义。 默认值为 64 MB。|  
|status|**nvarchar(32)**|工作线程的状态。|挂起，处理、 完成、 失败、 已中止|  
|start_time|**datetime**|此工作线程的执行开始时间。|大于或等于此辅助角色所属的查询步骤的开始时间。 请参阅[sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|end_time|**datetime**|时间的执行将结束、 失败或已取消。|对于正在进行或排入队列的辅助角色为 NULL。 否则为大于 start_time。|  
|total_elapsed_time|**int**|所用的执行，以毫秒为单位的总时间。|大于或等于 0。<br /><br /> 如果 total_elapsed_time 超出整数的最大值，将持续 total_elapsed_time 可最大值。 这种情况会生成警告"的最大值已超出。"<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
  
 此视图按保留的最大行有关的信息，请参阅中的元数据部分[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主题。
  
## <a name="see-also"></a>请参阅  
 [系统视图&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
