---
title: sys. dm_pdw_os_event_logs （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ed27e25a1aa977c8fc78186ae2bc9f96ee0e231e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82819259"
---
# <a name="sysdm_pdw_os_event_logs-transact-sql"></a>sys. dm_pdw_os_event_logs （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存有关不同节点上的不同 Windows 事件日志的信息。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|此日志来自的设备节点。<br /><br /> pdw_node_id 和 log_name 构成此视图的键。||  
|log_name|**nvarchar(255)**|Windows 事件日志名称。<br /><br /> pdw_node_id 和 log_name 构成此视图的键。||  
|log_source|**nvarchar(255)**|Windows 事件日志源名称。||  
|event_id|**int**|事件的 ID。 不唯一。||  
|event_type|**nvarchar(255)**|事件的类型，标识严重性。|"信息"、"警告"、"错误"|  
|event_message|**nvarchar(4000)**|事件的详细信息。||  
|generate_time|**datetime**|事件的创建时间。||  
|write_time|**datetime**|事件实际写入日志的时间。||  
  
 有关此视图保留的最大行的信息，请参阅[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主题中的元数据部分。 
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
