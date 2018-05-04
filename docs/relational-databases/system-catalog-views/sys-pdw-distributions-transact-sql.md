---
title: sys.pdw_distributions (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4e7d8e8ea3fa08c79bd7b0e26078ad229ce17c1b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="syspdwdistributions-transact-sql"></a>sys.pdw_distributions (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关分布区在设备上的信息。 它列出每个设备分布的一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|与分布相关联的唯一数字 id。<br /><br /> 此视图的键。|1 到计算节点的每个计算节点数的乘积的设备的数目。|  
|pdw_node_id|**int**|此分布是的节点 ID。|请参阅中的 pdw_node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|name|**nvarchar(32)**|字符串与分布，使用作为后缀分布式表相关联的标识符。|字符串组成的 A-Z、 a-z、"0-9、 _、-。|  
|position|**int**|在该节点上的其他分发到相应的节点内分发的位置。|1 到每个节点的分布区数目。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
