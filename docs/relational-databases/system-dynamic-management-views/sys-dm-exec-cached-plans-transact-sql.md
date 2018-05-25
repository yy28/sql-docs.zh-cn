---
title: sys.dm_exec_cached_plans (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plans
- dm_exec_cached_plans
- dm_exec_cached_plans_TSQL
- sys.dm_exec_cached_plans_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plans dynamic management view
ms.assetid: 95b707d3-3a93-407f-8e88-4515d4f2039d
caps.latest.revision: 44
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f181f3d3aaea01de64dd053c82eee4006d371139
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmexeccachedplans-transact-sql"></a>sys.dm_exec_cached_plans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为了加快查询执行而缓存的每个查询计划返回一行。 可以用此动态管理视图来查找缓存的查询计划、缓存的查询文本、缓存计划占用的内存量，以及重新使用缓存计划的计数。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 要避免公开此类信息，需要将包含不属于已连接租户的数据的每一行都筛选掉。此外，列中的值**memory_object_address**和**pool_id**进行筛选; 该列的值设置为 NULL。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_exec_cached_plans**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|bucketid|**int**|其中条目已缓存的哈希存储桶的 ID。 此值指示从 0 到特定缓存类型的哈希表大小之间的范围。<br /><br /> 对于 SQL 计划和对象计划缓存而言，在 32 位系统上哈希表的大小可达 10007，在 64 位系统上哈希表的大小可达 40009。 对于绑定树缓存而言，在 32 位系统上哈希表大小可达 1009，在 64 位系统上哈希表大小可达 4001。 对于扩展存储过程缓存的哈希表大小可达 127 32 位和 64 位系统上。|  
|refcounts|**int**|引用该缓存对象的缓存对象数。 **Refcounts**必须至少为 1 可在缓存中的条目。|  
|usecounts|**int**|已查找缓存对象的次数。 当参数化查询在缓存中找到计划时不递增。 在使用显示计划时可多次递增。|  
|size_in_bytes|**int**|缓存对象占用的字节数。|  
|memory_object_address|**varbinary(8)**|缓存条目的内存地址。 此值可与[sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)若要获取的内存明细，缓存的计划和[sys.dm_os_memory_cache_entries](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)_entries 一起使用，以获取的缓存条目的成本。|  
|cacheobjtype|**nvarchar(34)**|缓存中的对象类型。 该值可以是下列值之一：<br /><br /> Compiled Plan<br /><br /> Compiled Plan Stub<br /><br /> Parse Tree<br /><br /> Extended Proc<br /><br /> CLR Compiled Func<br /><br /> CLR Compiled Proc|  
|objtype|**nvarchar(16)**|对象的类型。 以下是可能的值以及及其相应的说明。<br /><br /> Proc： 存储的过程<br />准备好： 已准备的语句<br />Adhoc： 即席查询。 是指[!INCLUDE[tsql](../../includes/tsql-md.md)]作为语言事件提交使用**osql**或**sqlcmd**而不是作为远程过程调用。<br />ReplProc： 复制筛选过程<br />触发器： 触发器<br />视图： 视图<br />默认： 默认<br />UsrTab： 用户表<br />SysTab： 系统表<br />检查： CHECK 约束<br />规则： 规则|  
|plan_handle|**varbinary(64)**|内存中计划的标识符。 该标识符是瞬态的，仅当计划保留在缓存中时，它才保持不变。 此值可以和以下动态管理函数一起使用：<br /><br /> [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)<br /><br /> [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)<br /><br /> [sys.dm_exec_plan_attributes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)|  
|pool_id|**int**|特定资源池的 ID，此计划内存使用量就是针对该资源池而言的。|  
|pdw_node_id|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
 <sup>1</sup>  
  
## <a name="permissions"></a>权限

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="examples"></a>示例  
  
### <a name="a-returning-the-batch-text-of-cached-entries-that-are-reused"></a>A. 返回重新使用的缓存条目的批处理文本  
 以下示例返回经过多次使用的所有缓存条目的 SQL 文本。  
  
```  
SELECT usecounts, cacheobjtype, objtype, text   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle)   
WHERE usecounts > 1   
ORDER BY usecounts DESC;  
GO  
```  
  
### <a name="b-returning-query-plans-for-all-cached-triggers"></a>B. 为所有缓存触发器返回查询计划  
 以下示例返回所有缓存触发器的查询计划。  
  
```  
SELECT plan_handle, query_plan, objtype   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_query_plan(plan_handle)   
WHERE objtype ='Trigger';  
GO  
```  
  
### <a name="c-returning-the-set-options-with-which-the-plan-was-compiled"></a>C. 返回编译计划所用的 SET 选项  
 以下示例返回编译计划所用的 SET 选项。 `sql_handle`的计划，也会返回。 使用 PIVOT 运算符到输出`set_options`和`sql_handle`属性列，而不是行。 有关中返回的值的详细信息`set_options`，请参阅[sys.dm_exec_plan_attributes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)。  
  
```  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
      SELECT plan_handle, epa.attribute, epa.value   
      FROM sys.dm_exec_cached_plans   
      OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
      WHERE cacheobjtype = 'Compiled Plan'  
      ) AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
### <a name="d-returning-the-memory-breakdown-of-all-cached-compiled-plans"></a>D. 返回所有缓存的编译计划的内存明细  
 以下示例返回缓存中所有编译计划所使用的内存明细。  
  
```  
SELECT plan_handle, ecp.memory_object_address AS CompiledPlan_MemoryObject,   
    omo.memory_object_address, type, page_size_in_bytes   
FROM sys.dm_exec_cached_plans AS ecp   
JOIN sys.dm_os_memory_objects AS omo   
    ON ecp.memory_object_address = omo.memory_object_address   
    OR ecp.memory_object_address = omo.parent_address  
WHERE cacheobjtype = 'Compiled Plan';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_plan_attributes &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_os_memory_objects &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)   
 [sys.dm_os_memory_cache_entries &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)   
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)  
  
  


