---
title: "sys.dm_pdw_os_event_logs (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.reviewer: 
ms.service: 
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffd9bad344ed79048a65de4139ec7c2fd44cd9c4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  包含有关不同的 Windows 事件的信息都记录在不同节点上。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|此日志所在的设备节点。<br /><br /> pdw_node_id 和 log_name 组成的密钥，此视图。||  
|log_name|**nvarchar(255)**|Windows 事件日志名称。<br /><br /> pdw_node_id 和 log_name 组成的密钥，此视图。||  
|log_source|**nvarchar(255)**|Windows 事件日志源名称。||  
|event_id|**int**|事件 ID。 不是唯一的。||  
|event_type|**nvarchar(255)**|事件，标识严重性类型。|信息，警告、 错误|  
|event_message|**nvarchar(4000)**|事件详细信息。||  
|generate_time|**datetime**|创建事件的时间。||  
|write_time|**datetime**|事件实际写入日志的时间。||  
  
 有关通过此视图保留最大行数的信息，请参阅中的最大的系统视图值部分[最小值和最大值 (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)主题。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
