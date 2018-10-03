---
title: sys.dm_pdw_sys_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ad7311759e2ea38f5b9b375785b7f035d1dcdbfa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821515"
---
# <a name="sysdmpdwsysinfo-transact-sql"></a>sys.dm_pdw_sys_info (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  提供了一组设备级别反映在设备的总体活动的计数器。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|在系统中当前的会话数。|0 到 max_active_sessions （见下文）。|  
|idle_sessions|**int**|当前处于空闲状态的会话数。||  
|active_requests|**int**|当前正在运行的活动请求数。||  
|queued_requests|**int**|当前排队请求数。||  
|active_loads|**int**|在系统中当前正在运行的负载的数目。||  
|queued_loads|**int**|排队等待执行的加载的数。||  
|active_backups|**int**|当前正在运行的备份数。||  
|active_restores|**int**|当前正在运行的备份还原的数量。||  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
