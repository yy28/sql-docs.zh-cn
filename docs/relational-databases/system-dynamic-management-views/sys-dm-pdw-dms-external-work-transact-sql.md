---
title: "sys.dm_pdw_dms_external_work (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2aa4ee7ab7bc3ce19771a47ae990fe8904161f18
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>sys.dm_pdw_dms_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 保存有关外部操作的所有数据移动服务 (DMS) 步骤的信息的系统视图。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|使用此 DMS 辅助进程的查询。<br /><br /> request_id、 step_index 和 dms_step_index 窗体的密钥，此视图。|与在 request_id 相同[sys.dm_pdw_exec_requests &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|调用此 DMS 辅助进程的查询步骤。<br /><br /> request_id、 step_index 和 dms_step_index 窗体的密钥，此视图。|与在 step_index 相同[sys.dm_pdw_request_steps &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|DMS 计划中的当前步骤。<br /><br /> request_id、 step_index 和 dms_step_index 窗体的密钥，此视图。|与在 dms___step_index 相同[sys.dm_pdw_dms_workers &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md).|  
|pdw_node_id|**int**|正在运行的 DMS 辅助进程的节点。|与通过 node_id 中相同[sys.dm_pdw_nodes &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|type|**nvarchar(60)**|该节点正在运行的外部操作的类型。<br /><br /> 文件拆分是在已拆分为多个较小回退的外部 Hadoop 文件上一个操作。|文件拆分|  
|work_id|**int**|该文件拆分 id。|大于或等于 0。<br /><br /> 每个计算节点唯一。|  
|input_name|**nvarchar(60)**|正在读取的输入的名称的字符串。|对于 Hadoop 文件，这是 Hadoop 文件名称。|  
|read_location|**bigint**|读取位置的偏移量。||  
|estimated_bytes_processed|**bigint**|此工作线程处理的字节数。|大于或等于 0。|  
|长度|**bigint**|文件拆分中的字节数。<br /><br /> 对于 Hadoop，这是 HDFS 块的大小。|用户定义。 默认值为 64 MB。|  
|status|**nvarchar(32)**|辅助进程的状态。|挂起，处理、 完成、 失败、 已中止|  
|start_time|**datetime**|此辅助进程的执行开始时间。|大于或等于此辅助进程所属的查询步骤的开始时间。 请参阅[sys.dm_pdw_request_steps &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|从该处执行将结束、 失败或已取消的时间。|正在进行或已排队的工作人员的为 NULL。 否则为大于 start_time。|  
|total_elapsed_time|**int**|在执行，以毫秒为单位中花费的总时间。|大于或等于 0。<br /><br /> 如果 total_elapsed_time 超过一个整数的最大值，total_elapsed_time 将继续是最大值。 这种情况将生成警告"的最大值已超出。"<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
  
 有关通过此视图保留最大行数的信息，请参阅[最大的系统视图值](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)。  
  
## <a name="see-also"></a>另请参阅  
 [系统视图 &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
