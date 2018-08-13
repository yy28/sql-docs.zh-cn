---
title: sys.dm_exec_query_optimizer_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_info_TSQL
- dm_exec_query_optimizer_info
- sys.dm_exec_query_optimizer_info_TSQL
- sys.dm_exec_query_optimizer_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_info dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9e
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 282a55a0594a0d52a89066c997e6392bc8cc0dbb
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39557397"
---
# <a name="sysdmexecqueryoptimizerinfo-transact-sql"></a>sys.dm_exec_query_optimizer_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询优化器的操作的详细统计信息。 在优化工作负荷以确定查询优化的问题或改进之处时，可以使用此视图。 例如，可以用总优化次数、占用时间值以及最终开销值来对当前工作负荷的查询优化和优化过程中发现的任何变化进行比较。 某些计数器提供仅与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部诊断使用相关的数据。 这些计数器标记为“仅供内部使用”。  
  
> [!NOTE]  
>  若要调用此项从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_exec_query_optimizer_info**。  
  
|“属性”|数据类型|Description|  
|----------|---------------|-----------------|  
|**counter**|**nvarchar(4000)**|优化器统计信息事件的名称。|  
|**匹配项**|**bigint**|此计数器的优化事件的发生次数。|  
|**value**|**float**|每次发生事件的平均属性值。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="permissions"></a>Permissions  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
    
## <a name="remarks"></a>Remarks  
 **sys.dm_exec_query_optimizer_info**包含以下属性 （计数器）。 出现的所有值将累积并在系统重新启动时设置为 0。 系统重新启动时，值字段的所有值都设置为 NULL。 指定平均值的所有“值-列”的值使用同一行中的出现次数值作为计算平均值的分母。 所有查询优化时测量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]确定将变为**dm_exec_query_optimizer_info**，包括这两个用户和系统生成的查询。 已缓存的计划的执行不会更改中的值**dm_exec_query_optimizer_info**，只有优化会显著。  
  
|计数器|出现次数|ReplTest1|  
|-------------|----------------|-----------|  
|优化|总优化次数。|不适用|  
|占用时间|总优化次数。|每次优化单个语句（查询）所用的平均时间（秒）。|  
|最终开销|总优化次数。|优化计划的平均估计开销，以内部开销单位为单位。|  
|细微计划|仅供内部使用|仅供内部使用|  
|任务|仅供内部使用|仅供内部使用|  
|无计划|仅供内部使用|仅供内部使用|  
|搜索 0|仅供内部使用|仅供内部使用|  
|搜索 0 时间|仅供内部使用|仅供内部使用|  
|搜索 0 任务|仅供内部使用|仅供内部使用|  
|搜索 1|仅供内部使用|仅供内部使用|  
|搜索 1 时间|仅供内部使用|仅供内部使用|  
|搜索 1 任务|仅供内部使用|仅供内部使用|  
|搜索 2|仅供内部使用|仅供内部使用|  
|搜索 2 时间|仅供内部使用|仅供内部使用|  
|搜索 2 任务|仅供内部使用|仅供内部使用|  
|阶段 0 到阶段 1 的收益|仅供内部使用|仅供内部使用|  
|阶段 1 到阶段 2 的收益|仅供内部使用|仅供内部使用|  
|timeout|仅供内部使用|仅供内部使用|  
|超过内存限制|仅供内部使用|仅供内部使用|  
|插入语句|用于 INSERT 语句的优化数。|不适用|  
|删除语句|用于 DELETE 语句的优化数。|不适用|  
|更新语句|用于 UPDATE 语句的优化数。|不适用|  
|包含子查询|包含至少一个子查询的查询的优化数。|不适用|  
|取消嵌套失败|仅供内部使用|仅供内部使用|  
|表|总优化次数。|每个优化查询引用的平均表数。|  
|提示|指定某些提示的次数。 计数的提示包括：JOIN、GROUP、UNION 和 FORCE ORDER 查询提示，FORCE PLAN 设置选项和联接提示。|不适用|  
|排序提示|指定强制排序提示的次数。|不适用|  
|联接提示|联接提示强制联接算法的次数。|不适用|  
|视图引用|查询中引用视图的次数。|不适用|  
|远程查询|查询至少引用一个远程数据源（例如，具有四部分名称或 OPENROWSET 结果的表）的优化数。|不适用|  
|最大 DOP|总优化次数。|优化计划的平均有效 MAXDOP 值。 默认情况下，有效 MAXDOP 由**最大并行度**服务器配置选项，并可能被重写特定查询的 MAXDOP 查询提示值。|  
|最小递归级别|已用查询提示指定 MAXRECURSION 级别大于 0 的优化次数。|已用查询提示指定最大递归级别的优化中的平均 MAXRECURSION 级别。|  
|加载的索引视图|仅供内部使用|仅供内部使用|  
|匹配的索引视图|已匹配一个或多个索引视图的优化数。|匹配的平均视图数。|  
|使用的索引视图|在输出计划中使用经过匹配的一个或多个索引视图的优化次数。|使用的平均视图数。|  
|更新的索引视图|生成维护一个或多个索引视图的计划的 DML 语句的优化次数。|维护的平均视图数。|  
|动态游标请求|已指定动态游标请求的优化次数。|不适用|  
|快进游标请求|已指定快进游标请求的优化次数。|不适用|  
|合并 stmt|用于 MERGE 语句的优化数。|不适用|  
  
## <a name="examples"></a>示例  
  
### <a name="a-viewing-statistics-on-optimizer-execution"></a>A. 查看有关优化器执行的统计信息  
 哪些是此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的当前优化器执行统计信息？  
  
```  
SELECT * FROM sys.dm_exec_query_optimizer_info;  
```  
  
### <a name="b-viewing-the-total-number-of-optimizations"></a>B. 查看优化总数  
 执行了多少次优化？  
  
```  
SELECT occurrence AS Optimizations FROM sys.dm_exec_query_optimizer_info  
WHERE counter = 'optimizations';  
```  
  
### <a name="c-average-elapsed-time-per-optimization"></a>C. 每次优化占用的平均时间  
 每次优化占用的平均时间是多少？  
  
```  
SELECT ISNULL(value,0.0) AS ElapsedTimePerOptimization  
FROM sys.dm_exec_query_optimizer_info WHERE counter = 'elapsed time';  
```  
  
### <a name="d-fraction-of-optimizations-that-involve-subqueries"></a>D. 涉及子查询的优化部分  
 已优化查询的哪一部分包含子查询？  
  
```  
SELECT (SELECT CAST (occurrence AS float) FROM sys.dm_exec_query_optimizer_info WHERE counter = 'contains subquery') /  
       (SELECT CAST (occurrence AS float)   
        FROM sys.dm_exec_query_optimizer_info WHERE counter = 'optimizations')  
        AS ContainsSubqueryFraction;  
```  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与执行相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


