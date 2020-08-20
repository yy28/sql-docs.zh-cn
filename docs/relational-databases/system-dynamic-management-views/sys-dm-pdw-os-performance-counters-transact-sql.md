---
description: 'sys. dm_pdw_os_performance_counters (Transact-sql) '
title: sys. dm_pdw_os_performance_counters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0673a8f8-8bed-41eb-8959-a9e3e9e03a65
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 08ef29f6fe47099bcbbdeb87fce0dfb5aa25a42a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474727"
---
# <a name="sysdm_pdw_os_performance_counters-transact-sql"></a>sys. dm_pdw_os_performance_counters (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  包含有关中节点的 Windows 性能计数器的信息 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|包含计数器的节点的 ID。<br /><br /> pdw_node_id 和 counter_name 构成此视图的键。|请参阅 dm_pdw_nodes sys.databases 中的 node_id [&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|counter_name|**nvarchar(255)**|Windows 性能计数器的名称。||  
|counter_category|**nvarchar(255)**|Windows 性能计数器类别的名称。||  
|instance_name|**nvarchar(255)**|计数器特定实例的名称。||  
|counter_value|**十进制 (38，10) **|计数器的当前值。||  
|last_update_time|**Datetime2 (3) **|上次更新值的时间戳。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
