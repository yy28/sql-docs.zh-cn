---
title: sys. pdw_distributions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 12a3318f88a719ab70043e2685a475e14cf24fdc
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197394"
---
# <a name="syspdw_distributions-transact-sql"></a>sys. pdw_distributions (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存有关设备上的分发的信息。 它针对每个设备分布列出一行。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|与分发关联的唯一数字 id。<br /><br /> 此视图的键。|1到设备中计算节点的数目乘以每个计算节点的分布数。|  
|pdw_node_id|**int**|此分发所在的节点的 ID。|请参阅 dm_pdw_nodes sys.databases 中的 pdw_node_id [&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|name|**nvarchar(32)**|与分布关联的字符串标识符，用作分布式表的后缀。|由 "A-z"、"a-z"、"0-9"、"_"、"-" 组成的字符串。|  
|position|**int**|分布在节点中的位置，该节点对应于该节点上的其他分布。|1到每个节点的分配数。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
