---
title: sys.dm_pdw_hadoop_operations (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a9158bacb9959691118c356e4c742dc62e862346
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34466593"
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  个下推到 Hadoop 一部分运行的每个 map-reduce 作业中占一行[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]对外部 Hadoop 表的查询。 每个 map-reduce 作业均表示一个查询中的谓词。 谓词下推启用用于 Hadoop 外部表上的查询时才使用此选项。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|对于此外部 Hadoop 操作的 ID。|中的 ID 相同[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|指此 Hadoop 操作的查询步骤的索引。|与在 step_index 相同[sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|operation_type|**nvarchar(255)**|描述外部操作的类型。|外部 Hadoop Operation|  
|operation_name|**nvarchar(4000)**|Map-reduce 作业，作业 ID。 此值由 Hadoop 后返回[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]提交作业。||  
|map_progress|**float**|到目前为止消耗了映射作业的输入数据的百分比。|一个浮点数字之间，以及包括 0 和 100 之间。|  
|reduce_progress|**int**|化简作业已完成百分比...|一个浮点数字之间，以及包括 0 和 100 之间。|  
  
## <a name="see-also"></a>另请参阅  
 [系统视图&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
