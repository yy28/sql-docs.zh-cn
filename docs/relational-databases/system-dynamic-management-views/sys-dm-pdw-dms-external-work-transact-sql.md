---
description: 'sys. dm_pdw_dms_external_work (Transact-sql) '
title: sys. dm_pdw_dms_external_work (Transact-sql) |Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8633a363aa6ba486be4113bdf4826f2dc2e1a579
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474793"
---
# <a name="sysdm_pdw_dms_external_work-transact-sql"></a>sys. dm_pdw_dms_external_work (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 保存有关所有数据移动服务的信息的系统视图 (DM) 外部操作步骤。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|使用此 DMS 辅助角色的查询。<br /><br /> request_id、step_index 和 dms_step_index 构成此视图的键。|与 sys.databases 中的 request_id [dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|正在调用此 DMS 辅助角色的查询步骤。<br /><br /> request_id、step_index 和 dms_step_index 构成此视图的键。|与 sys.databases 中的 step_index [dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|dms_step_index|**int**|DMS 计划中的当前步骤。<br /><br /> request_id、step_index 和 dms_step_index 构成此视图的键。|与 sys.databases 中的 dms___step_index [dm_pdw_dms_workers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)。|  
|pdw_node_id|**int**|正在运行 DMS 辅助角色的节点。|与 sys.databases 中的 node_id [dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|type|**nvarchar(60)**|此节点正在运行的外部操作的类型。<br /><br /> 文件拆分是对已拆分成多个较小块的外部 Hadoop 文件执行的操作。|"文件拆分"|  
|work_id|**int**|文件拆分 ID。|大于或等于0。<br /><br /> 每个计算节点唯一。|  
|input_name|**nvarchar(60)**|要读取的输入的字符串名称。|对于 Hadoop 文件，这是 Hadoop 文件名。|  
|read_location|**bigint**|读取位置的偏移量。||  
|estimated_bytes_processed|**bigint**|此工作线程处理的字节数。|大于或等于0。|  
|length|**bigint**|文件拆分中的字节数。<br /><br /> 对于 Hadoop，这是 HDFS 块的大小。|用户定义的。 默认值为 64 MB。|  
|状态|**nvarchar(32)**|工作线程的状态。|挂起，处理，已完成，失败，已中止|  
|start_time|**datetime**|此工作线程的执行开始的时间。|大于或等于此辅助线程所属的查询步骤的开始时间。 请参阅 [sys.databases &#40;transact-sql&#41;dm_pdw_request_steps ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|end_time|**datetime**|执行结束、失败或已取消的时间。|对于正在进行的或已排队的工作线程，为 NULL。 否则，大于 start_time。|  
|total_elapsed_time|**int**|执行所用的总时间（以毫秒为单位）。|大于或等于0。<br /><br /> 如果 total_elapsed_time 超过整数的最大值，则 total_elapsed_time 将继续作为最大值。 此条件将生成警告 "已超过最大值。"<br /><br /> 最大值（以毫秒为单位）等效于24.8 天。|  
  
 有关此视图保留的最大行的信息，请参阅 [容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 主题中的元数据部分。
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的系统视图 &#40;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
