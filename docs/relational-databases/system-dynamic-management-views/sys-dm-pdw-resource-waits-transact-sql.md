---
title: sys.dm_pdw_resource_waits (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 40d96c4dadd7ddeac3c958b5d9ee2fed5287d74d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwresourcewaits-transact-sql"></a>sys.dm_pdw_resource_waits (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  显示等待中的所有资源类型的信息[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|请求的等待列表中的位置。|基于 0 的序号。 这不是唯一跨所有等待条目。|  
|session_id|**nvarchar(32)**|在其中发生等待状态的会话 ID。|请参阅中的 session_id [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|type|**nvarchar(255)**|等待此条目表示的类型。|可能的值：<br /><br /> 连接<br /><br /> 本地查询并发<br /><br /> 分布式的查询并发<br /><br /> DMS 并发<br /><br /> 备份的并发|  
|object_type|**nvarchar(255)**|通过在等待受影响的对象类型。|可能的值：<br /><br /> **OBJECT**<br /><br /> **DATABASE**<br /><br /> **SYSTEM**<br /><br /> **SCHEMA**<br /><br /> **应用程序**|  
|object_name|**nvarchar(386)**|名称或 GUID 指定等待受影响的对象。|表和视图将显示为三个部分组成的名称。<br /><br /> 索引和统计信息将显示具有由四部分构成的名称。<br /><br /> 名称、 主体和数据库是字符串名称。|  
|request_id|**nvarchar(32)**|在其发生等待状态的请求的 ID。|QID 的请求标识符。<br /><br /> 负载请求的 GUID 标识符。|  
|request_time|**datetime**|请求的锁或资源的时间。||  
|acquire_time|**datetime**|获取锁或资源的时间。||  
|state|**nvarchar(50)**|等待状态的状态。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等待项的优先级。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|为此请求保留并发槽 (32 max) 的数目。|1 – 用于 SmallRC<br /><br /> 3 – MediumRC<br /><br /> LargeRC 的 7<br /><br /> 22 – 对于 XLargeRC|  
|resource_class|**nvarchar(20)**|用于此请求的资源类。|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
