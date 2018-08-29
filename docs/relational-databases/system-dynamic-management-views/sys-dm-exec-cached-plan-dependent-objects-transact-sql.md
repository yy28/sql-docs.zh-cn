---
title: sys.dm_exec_cached_plan_dependent_objects (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plan_dependent_objects
- dm_exec_cached_plan_dependent_objects_TSQL
- sys.dm_exec_cached_plan_dependent_objects_TSQL
- dm_exec_cached_plan_dependent_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plan_dependent_objects dynamic management function
ms.assetid: 9b6cf5f7-b267-44fb-aac8-f49c9aa10cc1
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1d53372bd1ff1ae214e605d7fb5f8a27f211a9e9
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43102155"
---
# <a name="sysdmexeccachedplandependentobjects-transact-sql"></a>sys.dm_exec_cached_plan_dependent_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  针对每个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 执行计划、公共语言运行时 (CLR) 执行计划和与计划关联的游标返回一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
dm_exec_cached_plan_dependent_objects(plan_handle)  
```  
  
## <a name="arguments"></a>参数  
 *plan_handle*  
 为已执行且其计划位于计划缓存中的批次唯一标识查询执行计划。 *plan_handle*是**varbinary(64)**。 *Plan_handle*可以从以下动态管理对象中获得：  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**usecounts**|**int**|执行上下文或游标的已用次数。<br /><br /> 此列不可为空值。|  
|**memory_object_address**|**varbinary(8)**|执行上下文或游标的内存地址。<br /><br /> 此列不可为空值。|  
|**cacheobjtype**|**nvarchar(50)**|计划缓存对象类型。 此列不可为空值。 可能的值有<br /><br /> 可执行计划<br /><br /> CLR 编写函数<br /><br /> CLR 编写过程<br /><br /> 游标|  
  
## <a name="permissions"></a>Permissions  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="physical-joins"></a>物理联接  
 ![关系图](../../relational-databases/system-dynamic-management-views/media/dm-dependent-objects.gif "关系图")  
  
## <a name="relationship-cardinalities"></a>关系基数  
  
|从|若要|日期|关系|  
|----------|--------|--------|------------------|  
|**dm_exec_cached_plan_dependent_objects**|**dm_os_memory_objects**|**memory_object_address**|一对一|  
  
## <a name="see-also"></a>请参阅  
 [与执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.syscacheobjects &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)  
  
  
