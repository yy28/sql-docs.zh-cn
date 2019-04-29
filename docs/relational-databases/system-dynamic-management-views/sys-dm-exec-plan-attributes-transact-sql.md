---
title: sys.dm_exec_plan_attributes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_plan_attributes_TSQL
- dm_exec_plan_attributes_TSQL
- dm_exec_plan_attributes
- sys.dm_exec_plan_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_plan_attributes dynamic management function
ms.assetid: dacf3ab3-f214-482e-aab5-0dab9f0a3648
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c17f1ba2b6e57fe9194d4cbf4a6e365e65a89d6c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013223"
---
# <a name="sysdmexecplanattributes-transact-sql"></a>sys.dm_exec_plan_attributes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  针对计划句柄所指定计划的每个计划属性返回一行。 可以使用此表值函数获取有关特定计划的详细信息，例如计划的缓存键值或当前同步执行次数。  
  
> [!NOTE]  
>  通过返回的信息的一些此函数将映射到[sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)向后兼容性视图。

## <a name="syntax"></a>语法  
```  
sys.dm_exec_plan_attributes ( plan_handle )  
```  
  
## <a name="arguments"></a>参数  
 *plan_handle*  
 用于唯一标识已执行并且其计划驻留在计划缓存中的批处理的查询计划。 *plan_handle*是**varbinary(64)**。 可以从获取的计划句柄[sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)动态管理视图。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|属性|**varchar(128)**|与此计划关联的属性的名称。 立即下此表列出了可能的属性、 其数据类型和及其说明。|  
|value|**sql_variant**|与此计划关联的属性的值。|  
|is_cache_key|**bit**|指示此属性是否用作计划的缓存查找密钥的一部分。|  

从上表中，**特性**可以具有以下值：

|特性|数据类型|Description|  
|---------------|---------------|-----------------|  
|set_options|**int**|指示编译计划所使用的选项值。|  
|objectid|**int**|用于在缓存中查找对象的主键之一。 这是 ID 中存储的对象[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)的数据库对象 （过程、 视图、 触发器等）。 对于类型为“即席”或“已准备好”的计划，它是批处理文本的内部哈希。|  
|dbid|**int**|是包含计划引用的实体的数据库 ID。<br /><br /> 对于即席计划或已准备好的计划，它是执行批处理的数据库 ID。|  
|dbid_execute|**int**|为系统对象存储在**资源**数据库，请从其执行缓存的计划的数据库 ID。 对于所有其他情况，均为 0。|  
|user_id|**int**|值 -2 指示已提交的批处理不依赖于隐式名称解析并可在不同的用户间共享。 这是首选方法。 任何其他值表示数据库中提交查询的用户的用户 ID。| 
|language_id|**smallint**|创建缓存对象的连接的语言 ID。 有关详细信息，请参阅[sys.syslanguages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)。|  
|date_format|**smallint**|创建缓存对象的连接的日期格式。 有关详细信息，请参阅 [SET DATEFORMAT (Transact-SQL)](../../t-sql/statements/set-dateformat-transact-sql.md).|  
|date_first|**tinyint**|第一个日期值。 有关详细信息，请参阅 [SET DATEFIRST (Transact-SQL)](../../t-sql/statements/set-datefirst-transact-sql.md).|  
|status|**int**|缓存查找密钥中的内部状态位。|  
|required_cursor_options|**int**|用户指定的游标选项，例如游标类型。|  
|acceptable_cursor_options|**int**|为了支持语句的执行，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以隐式转换采用的游标选项。 例如，用户可能指定一个动态游标，但允许查询优化器将此游标类型转换为静态游标。|  
|inuse_exec_context|**int**|使用查询计划并且当前正在执行的批处理的数目。|  
|free_exec_context|**int**|当前未使用的查询计划的缓存执行上下文数目。|  
|hits_exec_context|**int**|从计划缓存获取执行上下文并重用从而节省 SQL 语句编译开销的次数。 该值是目前所有批处理执行的聚合。|  
|misses_exec_context|**int**|无法在计划缓存中找到执行上下文而导致为批处理执行创建新的执行上下文的次数。|  
|removed_exec_context|**int**|由于缓存计划的内存压力而删除的执行上下文数目。|  
|inuse_cursors|**int**|包含一个或多个使用缓存计划的游标的当前正在执行的批数。|  
|free_cursors|**int**|缓存计划的空闲或可用游标数。|  
|hits_cursors|**int**|从缓存计划获得不活动游标并重用的次数。 该值是目前所有批处理执行的聚合。|  
|misses_cursors|**int**|无法在缓存中找到不活动游标的次数。|  
|removed_cursors|**int**|由于缓存计划的内存压力而删除的游标数。|  
|sql_handle|**varbinary**(64)|批处理的 SQL 句柄。|  
|merge_action_type|**smallint**|用作 MERGE 语句结果的触发器执行计划的类型。<br /><br /> 0 表示非触发器计划，或者不会作为 MERGE 语句结果来执行的触发器计划，或者作为仅指定 DELETE 操作的 MERGE 语句结果执行的触发器计划。<br /><br /> 1 表示作为 MERGE 语句结果运行的 INSERT 触发器计划。<br /><br /> 2 表示作为 MERGE 语句结果运行的 UPDATE 触发器计划。<br /><br /> 3 表示一个作为包含对应的 INSERT 或 UPDATE 操作的 MERGE 语句结果运行的 DELETE 触发器计划。<br /><br /> 对于由级联操作运行的嵌套触发器，此值是导致级联的 MERGE 语句的操作。|  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="remarks"></a>备注  
  
## <a name="set-options"></a>Set 选项  
 相同编译计划的副本可能只是中的值不同**set_options**列。 这说明不同的连接为相同的查询使用不同的 SET 选项集。 通常不希望使用不同的选项集，因为这可能导致额外的编译工作、减少计划重用并由于缓存中的多个计划副本而导致计划缓存膨胀。  
  
### <a name="evaluating-set-options"></a>计算 Set 选项  
 转换中返回的值**set_options**编译计划所用的选项，减去这些值**set_options**值，直到你从最大值，达到 0。 所减去的每个值对应于查询计划中所用的一个选项。 例如，如果中的值**set_options**为 251，编译计划所使用的选项为 ANSI_NULL_DFLT_ON (128)、 QUOTED_IDENTIFIER (64)、 ANSI_NULLS(32)、 ANSI_WARNINGS (16)、 CONCAT_NULL_YIELDS_NULL (8)、 并行 Plan(2)和 ANSI_PADDING (1)。  
  
|Option|ReplTest1|  
|------------|-----------|  
|ANSI_PADDING|1|  
|Parallel Plan|2|  
|FORCEPLAN|4|  
|CONCAT_NULL_YIELDS_NULL|8|  
|ANSI_WARNINGS|16|  
|ANSI_NULLS|32|  
|QUOTED_IDENTIFIER|64|  
|ANSI_NULL_DFLT_ON|128|  
|ANSI_NULL_DFLT_OFF|256|  
|NoBrowseTable<br /><br /> 指示计划不使用工作表实现 FOR BROWSE 操作。|512|  
|TriggerOneRow<br /><br /> 指示计划包含针对 AFTER 触发器 delta 表的单行优化。|1024|  
|ResyncQuery<br /><br /> 指示查询由内部系统存储过程提交。|2048|  
|ARITH_ABORT|4096|  
|NUMERIC_ROUNDABORT|8192|  
|DATEFIRST|16384|  
|DATEFORMAT|32768|  
|LanguageID|65536|  
|UPON<br /><br /> 指示编译计划时数据库选项 PARAMETERIZATION 设置为 FORCED。|131072|  
|ROWCOUNT|**适用于：** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /><br /> 262144|  
  
## <a name="cursors"></a>游标  
 不活动游标缓存在编译的计划中，以便游标的并发用户可以重用存储游标所使用的内存。 例如，假设某批处理声明并使用了一个游标，但未释放该游标。 如果有两个用户执行同一个批处理，将有两个活动游标。 游标释放（可能在不同批处理中）后，用于存储该游标的内存就会缓存但不释放。 此不活动游标列表保存在编译的计划中。 下次用户执行该批处理时，缓存的游标内存将重用并相应地初始化为活动游标。  
  
### <a name="evaluating-cursor-options"></a>计算游标选项  
 转换中返回的值**required_cursor_options**并**acceptable_cursor_options**编译计划所用的选项，减去的列值，并从开始值最大值，直到达到 0。 所减去的每个值对应于查询计划中所用的一个游标选项。  
  
|Option|ReplTest1|  
|------------|-----------|  
|None|0|  
|INSENSITIVE|1|  
|SCROLL|2|  
|READ ONLY|4|  
|FOR UPDATE|8|  
|LOCAL|16|  
|GLOBAL|32|  
|FORWARD_ONLY|64|  
|KEYSET|128|  
|DYNAMIC|256|  
|SCROLL_LOCKS|512|  
|OPTIMISTIC|1024|  
|STATIC|2048|  
|FAST_FORWARD|4096|  
|IN PLACE|8192|  
|FOR select_statement|16384|  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-attributes-for-a-specific-plan"></a>A. 返回特定计划的属性  
 下例将返回指定计划的所有计划属性。 将首先查询 `sys.dm_exec_cached_plans` 动态管理视图以获得指定计划的计划句柄。 在第二次查询中，用第一次查询中的计划句柄值替换 `<plan_handle>`。  
  
```sql  
SELECT plan_handle, refcounts, usecounts, size_in_bytes, cacheobjtype, objtype   
FROM sys.dm_exec_cached_plans;  
GO  
SELECT attribute, value, is_cache_key  
FROM sys.dm_exec_plan_attributes(<plan_handle>);  
GO  
```  
  
### <a name="b-returning-the-set-options-for-compiled-plans-and-the-sql-handle-for-cached-plans"></a>B. 返回编译计划的 SET 选项和缓存计划的 SQL 句柄  
 下例将返回代表编译每个计划时所用选项的值。 此外，还将返回所有缓存计划的 SQL 句柄。  
  
```sql  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
    SELECT plan_handle, epa.attribute, epa.value   
    FROM sys.dm_exec_cached_plans   
        OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
    WHERE cacheobjtype = 'Compiled Plan') AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_cached_plans &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  

