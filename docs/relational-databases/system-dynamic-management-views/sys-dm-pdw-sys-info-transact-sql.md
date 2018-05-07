---
title: sys.dm_pdw_sys_info (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5ea4d0200d5db2f8e9a9b92fce508f975bc3e4df
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmpdwsysinfo-transact-sql"></a>sys.dm_pdw_sys_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  提供一组设备反映总体活动的设备级别计数器。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|系统中当前的会话数。|0 到 max_active_sessions （见下文）。|  
|idle_sessions|**int**|当前空闲会话数。||  
|active_requests|**int**|当前运行的活动请求数。||  
|queued_requests|**int**|当前排队请求数。||  
|active_loads|**int**|在系统中当前运行的负载的数。||  
|queued_loads|**int**|排队等待执行的负载的数。||  
|active_backups|**int**|当前运行的备份数。||  
|active_restores|**int**|当前正在运行的备份还原的数。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
