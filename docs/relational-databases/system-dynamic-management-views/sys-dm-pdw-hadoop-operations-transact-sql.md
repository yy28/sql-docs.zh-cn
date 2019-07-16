---
title: sys.dm_pdw_hadoop_operations (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b4429585d735ee4eb51d2b0b421b53fdf06bf8ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899383"
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  向下推送到 Hadoop 一部分运行的每个 map-reduce 作业存在对应的一行[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]对外部 Hadoop 表的查询。 每个 map-reduce 作业，表示在查询中的谓词之一。 仅当谓词下推启用对 Hadoop 外部表的查询时，才使用此选项。  
  
|列名|数据类型|描述|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|对于此外部 Hadoop 操作 ID。|中的 ID 相同[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|此 Hadoop 操作是指的查询步骤的索引。|相同中 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|operation_type|**nvarchar(255)**|描述外部操作的类型。|外部 Hadoop Operation|  
|operation_name|**nvarchar(4000)**|Map-reduce 作业，作业 ID。 此值由 Hadoop 后返回[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]提交作业。||  
|map_progress|**float**|到目前为止消耗了 map 作业的输入数据的百分比。|一个浮点数之间，以及包括 0 和 100 之间。|  
|reduce_progress|**int**|已完成的 reduce 作业的百分比...|一个浮点数之间，以及包括 0 和 100 之间。|  
  
## <a name="see-also"></a>请参阅  
 [系统视图&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
