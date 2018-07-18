---
title: sys.dm_pdw_resource_waits (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 704fcdc72f571485f10b76860a632c61233ed296
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38000849"
---
# <a name="sysdmpdwresourcewaits-transact-sql"></a>sys.dm_pdw_resource_waits (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  显示等待中的所有资源类型的信息[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|请求的等待列表中的位置。|基于 0 的序号。 这不是唯一所有等待条目。|  
|session_id|**nvarchar(32)**|在其中发生等待状态的会话 ID。|请参阅中的 session_id [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|type|**nvarchar(255)**|等待此条目表示的类型。|可能的值：<br /><br /> 连接<br /><br /> 本地查询并发性<br /><br /> 分布式的查询并发性<br /><br /> DMS 并发<br /><br /> 备份并发|  
|object_type|**nvarchar(255)**|等待受影响的对象的类型。|可能的值：<br /><br /> **OBJECT**<br /><br /> **DATABASE**<br /><br /> **SYSTEM**<br /><br /> **SCHEMA**<br /><br /> **应用程序**|  
|object_name|**nvarchar(386)**|名称或 GUID 指定等待受影响的对象。|表和视图都显示三个部分组成的名称。<br /><br /> 索引和统计信息显示具有由四部分组成的名称。<br /><br /> 名称、 主体和数据库是字符串名称。|  
|request_id|**nvarchar(32)**|在其发生的等待状态的请求 ID。|请求的 QID 标识符。<br /><br /> 加载请求的 GUID 标识符。|  
|request_time|**datetime**|请求的锁或资源的时间。||  
|acquire_time|**datetime**|获取的锁或资源的时间。||  
|state|**nvarchar(50)**|等待状态的状态。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等待项的优先级。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|保留此请求的并发槽数 (最大值 32) 数。|1 – 对于 SmallRC<br /><br /> 3 – 为 MediumRC<br /><br /> LargeRC 的 7<br /><br /> 22-为 XLargeRC|  
|resource_class|**nvarchar(20)**|用于此请求的资源类。|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
