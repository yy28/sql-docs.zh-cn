---
title: sys.pdw_distributions (TRANSACT-SQL) |Microsoft Docs
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
ms.openlocfilehash: 7deddb57cdc02410fe161728f45190492ac18a16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127553"
---
# <a name="syspdwdistributions-transact-sql"></a>sys.pdw_distributions (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存在设备上的分发有关的信息。 它列出了每个设备分发对应一行。  
  
|列名|数据类型|描述|范围|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|与分布相关的唯一数字 id。<br /><br /> 此视图的键。|1 到乘以每个计算节点的分布区数目的设备中的计算节点数。|  
|pdw_node_id|**int**|此分布是的节点 ID。|请参阅中的 pdw_node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|name|**nvarchar(32)**|字符串标识符关联的分发、 用作分布式表上的后缀。|字符串组成的 A-Z、 a-z、"0-9、 _、-。|  
|position|**int**|该节点上的其他分发到相应的节点内的分布的位置。|1 到每个节点的分布区数。|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
