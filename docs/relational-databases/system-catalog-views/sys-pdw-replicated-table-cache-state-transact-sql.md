---
description: sys.pdw_replicated_table_cache_state (Transact-SQL)
title: sys.pdw_replicated_table_cache_state (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: ee5476020cfcece9bf9168bc048f3a0f3d34b635
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475349"
---
# <a name="syspdw_replicated_table_cache_state-transact-sql"></a>sys.pdw_replicated_table_cache_state (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  **Object_id**返回与复制的表关联的缓存状态。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|表的对象 ID。 请参阅 [sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。<br /><br /> **object_id** 是此视图的键。||  
|state|**nvarchar(40)**|此表的复制表缓存状态。|"NotReady"、"Ready"|  
  
## <a name="example"></a>示例
此示例将 sys. pdw_replicated_table_cache_state 与 sys.databases 联接以检索表名和复制的表缓存的状态。

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>后续步骤  
 有关 SQL 数据仓库和并行数据仓库的所有目录视图的列表，请参阅 [Sql 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。   
  
