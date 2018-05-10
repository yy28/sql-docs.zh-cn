---
title: sys.dm_pdw_os_performance_counters (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0673a8f8-8bed-41eb-8959-a9e3e9e03a65
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 96f788386a53e4493d0fb52ab33bfe1848527f4f
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwosperformancecounters-transact-sql"></a>sys.dm_pdw_os_performance_counters (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  包含有关 Windows 性能计数器中的节点信息[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|包含的计数器的节点 ID。<br /><br /> pdw_node_id 和 counter_name 组成的密钥，此视图。|请参阅中的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|counter_name|**nvarchar(255)**|Windows 性能计数器的名称。||  
|counter_category|**nvarchar(255)**|Windows 性能计数器类别的名称。||  
|instance_name|**nvarchar(255)**|计数器特定实例的名称。||  
|counter_value|**Decimal(38,10)**|计数器的当前值。||  
|last_update_time|**Datetime2(3)**|值上次更新的时间的时间戳。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
