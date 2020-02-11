---
title: sys. dm_pdw_os_threads （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ddc12f05-edeb-4848-b6d7-e851684cf044
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a4b9028d30db3c36157ef3db628dcb7c1cbeda00
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899230"
---
# <a name="sysdm_pdw_os_threads-transact-sql"></a>sys. dm_pdw_os_threads （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|受影响的节点的 ID。<br /><br /> pdw_node_id 和 thread_id 构成此视图的键。|请参阅 dm_pdw_nodes sys.databases 中的 node_id [&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|thread_id|**int**|pdw_node_id 和 thread_id 构成此视图的键。||  
|process_id|**int**|||  
|name|**nvarchar(255)**|||  
|priority|**int**|||  
|start_time|**datetime**|||  
|state|**nvarchar （32）**|||  
|wait_reason|**nvarchar （32）**|||  
|total_processor_elapsed_time|**bigint**|线程使用的内核时间总量。||  
|total_user_elapsed_time|**bigint**|线程使用的总用户时间||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
