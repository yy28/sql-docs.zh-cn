---
title: sys. dm_exec_external_operations （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_OPERATIONS_TSQL
- DM_EXEC_EXTERNAL_OPERATIONS
- SYS.DM_EXEC_EXTERNAL_OPERATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_external_operations management view
- dm_exec_external_operations management view
ms.assetid: d268217a-85b8-4b7f-9cd1-87865eba2be1
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b45bbaad37807e7ead860a9993648ee1e8c87315
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821220"
---
# <a name="sysdm_exec_external_operations-transact-sql"></a>sys.dm_exec_external_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  捕获有关外部 PolyBase 操作的信息。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|与 PolyBase 查询关联的唯一查询标识符|请参阅 sys.databases 中的 ID [dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|查询步骤的索引|请参阅 dm_exec_distributed_request_steps sys.databases 中的 step_index [&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|operation_ 类型|**nvarchar(128)**|描述 Hadoop 操作或其他外部操作|"外部 Hadoop 操作"|  
|operation_ 名称|**nvarchar(4000)**|指示作业状态的百分比（输入的使用量）|0-1-乘以系数100（已完成）|  
|map_ 进度|**float**|指示缩减作业状态的百分比（如果有）|0-1-乘以系数100（已完成）|  
  
## <a name="see-also"></a>另请参阅  
 [通过动态管理视图进行 PolyBase 故障排除](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
