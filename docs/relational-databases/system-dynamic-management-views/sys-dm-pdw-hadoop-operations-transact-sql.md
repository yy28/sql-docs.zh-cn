---
description: 'sys. dm_pdw_hadoop_operations (Transact-sql) '
title: sys. dm_pdw_hadoop_operations (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 6665a23aa3b3a30aee3c80cfbd8ed139d6784d3e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481853"
---
# <a name="sysdm_pdw_hadoop_operations-transact-sql"></a>sys. dm_pdw_hadoop_operations (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  在对外部 Hadoop 表运行查询的过程中，每个映射到 Hadoop 的每个地图缩减作业都包含一行 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 每个映射-缩减作业表示查询中的一个谓词。 仅当为 Hadoop 外部表上的查询启用了谓词下推时，才使用此功能。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此外部 Hadoop 操作的 ID。|与 [sys. dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)相同。|  
|step_index|**int**|引用此 Hadoop 操作的查询步骤的索引。|与 sys.databases 中的 step_index [dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|operation_type|**nvarchar(255)**|描述外部操作的类型。|"外部 Hadoop 操作"|  
|operation_name|**nvarchar(4000)**|映射-缩减作业的作业 ID。 此情况由 Hadoop 在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 提交作业后返回。||  
|map_progress|**float**|映射作业迄今为止已使用的输入数据的百分比。|介于和之间的浮点数字，其中包括0和100。|  
|reduce_progress|**int**|已完成的缩减作业的百分比。|介于和之间的浮点数字，其中包括0和100。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的系统视图 &#40;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
