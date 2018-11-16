---
title: sys.dm_pdw_os_event_logs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f778d8904e80aa8874c5ec346cb378f7c9355c03
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656461"
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  包含有关不同的 Windows 事件的信息都记录在不同节点上。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|此日志所在的设备节点。<br /><br /> pdw_node_id 和 log_name 形成此视图的键。||  
|log_name|**nvarchar(255)**|Windows 事件日志名称。<br /><br /> pdw_node_id 和 log_name 形成此视图的键。||  
|log_source|**nvarchar(255)**|Windows 事件日志源名称。||  
|event_id|**int**|事件的 ID。 不是唯一的。||  
|event_type|**nvarchar(255)**|事件，确定严重性类型。|信息、 警告，Error|  
|event_message|**nvarchar(4000)**|该事件的详细信息。||  
|generate_time|**datetime**|创建事件的时间。||  
|write_time|**datetime**|实际写入事件日志的时间。||  
  
 此视图按保留的最大行有关的信息，请参阅中的系统视图的最大值部分[最小和最大值 (SQL Server PDW)](https://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9)主题。  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
