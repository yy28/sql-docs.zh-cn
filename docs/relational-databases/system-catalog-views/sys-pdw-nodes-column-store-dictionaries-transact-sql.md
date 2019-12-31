---
title: sys. pdw_nodes_column_store_dictionaries （Transact-sql）
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.custom: seo-dt-2019
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 7ae1c2e4-45c0-4880-a692-1f299fbcfd19
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4e4ecf91491a88e002c92a82d321e5712d48ef76
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399823"
---
# <a name="syspdw_nodes_column_store_dictionaries-transact-sql"></a>sys. pdw_nodes_column_store_dictionaries （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  列存储索引中使用的每个字典都包含一行。 字典用于对某些而非全部数据类型进行编码，因此并非列存储索引中的所有列都有字典。 字典可以作为主字典存在（对于所有段），也可能作为用于部分列段的其他辅助字典存在。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|指示分区 ID。 在数据库中是唯一的。|  
|**hobt_id**|**bigint**|具有此列存储索引的表的堆或B 树索引（HoBT）的 ID。|  
|**column_id**|**整形**|列存储列的 ID。|  
|**dictionary_id**|**整形**|字典的 ID。|  
|**版本**|**整形**|字典格式的版本。|  
|**类别**|**整形**|字典类型：<br /><br /> 1-包含**int**值的哈希字典<br /><br /> 2-未使用<br /><br /> 3-包含字符串值的哈希字典<br /><br /> 包含**浮点**值的4哈希字典|  
|**last_id**|**整形**|字典中的最后一个数据 ID。|  
|**entry_count**|**bigint**|字典中的条目数。|  
|**on_disc_size**|**bigint**|字典大小（以字节为单位）。|  
|**pdw_node_id**|**整形**|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]节点的唯一标识符。|  
  
## <a name="permissions"></a>权限  
 需要 `VIEW SERVER STATE` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [&#40;Transact-sql&#41;创建列存储索引](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys. pdw_nodes_column_store_segments &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [sys. pdw_nodes_column_store_row_groups &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
  
