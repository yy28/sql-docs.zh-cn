---
title: 'sys. pdw_permanent_table_mappings (Transact-sql) '
ms.custom: ''
ms.date: 07/24/2020
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: mstehrani
ms.author: emtehran
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: c48cb981549d47b24152772cef9278de6557612f
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89062256"
---
# <a name="syspdw_permanent_table_mappings-transact-sql"></a>sys. pdw_permanent_table_mappings (Transact-sql) 
[!INCLUDE [applies-to-version/asa](../../includes/applies-to-version/asa.md)]

  通过 **object_id**将永久用户表与内部对象名称进行绑定。  
  
> [!NOTE]
> **sys. pdw_permanent_table_mappings** 保存到永久性表的映射，并且不包含临时或外部表映射。

|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|physical_name|**nvarchar (36) **|表的物理名称。<br /><br /> **physical_name** 和 **object_id** 构成此视图的键。||  
|object_id|**int**|表的对象 ID。 请参阅 [sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。<br /><br /> **physical_name** 和 **object_id** 构成此视图的键。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys. pdw_index_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
  
