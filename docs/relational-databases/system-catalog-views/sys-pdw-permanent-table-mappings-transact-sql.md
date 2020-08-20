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
ms.openlocfilehash: 12261e8e38e75edf7dd596ca2b3499100cfff5ad
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646837"
---
# <a name="syspdw_permanent_table_mappings-transact-sql"></a>sys. pdw_permanent_table_mappings (Transact-sql) 
[!INCLUDE [applies-to-version/asa](../../includes/applies-to-version/asa.md)]

  通过 **object_id**将永久用户表与内部对象名称进行绑定。 建议使用比 sys.databases 更好的性能 **pdw_table_mappings**。  
  
> [!NOTE]
> **sys. pdw_permanent_table_mappings** 保存到永久性表的映射，并且不包含临时表映射。

|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|physical_name|**nvarchar (36) **|表的物理名称。<br /><br /> **physical_name** 和 **object_id** 构成此视图的键。||  
|object_id|**int**|表的对象 ID。 请参阅 [sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。<br /><br /> **physical_name** 和 **object_id** 构成此视图的键。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys. pdw_index_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
  
