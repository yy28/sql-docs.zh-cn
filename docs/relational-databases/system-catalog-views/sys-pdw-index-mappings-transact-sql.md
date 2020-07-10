---
title: sys. pdw_index_mappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 3e51acd0ef179d4bb9bf85bed34593f9676db063
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196779"
---
# <a name="syspdw_index_mappings-transact-sql"></a>sys. pdw_index_mappings (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  将逻辑索引映射到计算节点上使用的物理名称，该名称由保存该表中特定索引的索引和**index_id**的表的**object_id**的唯一组合反映。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|此索引所在的逻辑表的对象 ID。 请参阅[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。<br /><br /> **physical_name**和**object_id**构成此视图的键。||  
|index_id|**nvarchar(32)**|索引的 ID。 请参阅[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。||  
|physical_name|**nvarchar (36) **|计算节点上的数据库中的索引名称。<br /><br /> **physical_name**和**object_id**构成此视图的键。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys. pdw_table_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [sys. pdw_database_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  
