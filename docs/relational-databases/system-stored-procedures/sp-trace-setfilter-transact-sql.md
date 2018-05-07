---
title: sp_trace_setfilter (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_trace_setfilter
- sp_trace_setfilter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setfilter
ms.assetid: 11e7c7ac-a581-4a64-bb15-9272d5c1f7ac
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dc23abf114ce4458f40051db3d2bb86b667efca5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sptracesetfilter-transact-sql"></a>sp_trace_setfilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将筛选应用于跟踪。 **sp_trace_setfilter**可能已停止的现有跟踪上执行 (*状态*是**0**)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果在跟踪不存在或其上执行此存储的过程返回错误*状态*不**0**。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用扩展事件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_trace_setfilter [ @traceid = ] trace_id   
          , [ @columnid = ] column_id  
          , [ @logical_operator = ] logical_operator  
          , [ @comparison_operator = ] comparison_operator  
          , [ @value = ] value  
```  
  
## <a name="arguments"></a>参数  
 [ **@traceid=** ] *trace_id*  
 要为其设置筛选器的跟踪的 ID。 *trace_id*是**int**，无默认值。 用户使用这*trace_id*值来识别、 修改和控制跟踪。  
  
 [ **@columnid=** ] *column_id*  
 应用了筛选器的列的 ID。 *column_id*是**int**，无默认值。 如果*column_id*为 NULL，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]清除所有筛选器指定的跟踪。  
  
 [ **@logical_operator** = ] *logical_operator*  
 指定是否 AND (**0**) 或 OR (**1**) 运算符应用。 *logical_operator*是**int**，无默认值。  
  
 [ **@comparison_operator=** ] *comparison_operator*  
 指定要执行的比较的类型。 *comparison_operator*是**int**，无默认值。 下表包含比较运算符及其代表的值。  
  
|“值”|比较运算符|  
|-----------|-------------------------|  
|**0**|= （等于）|  
|**1**|<>（不等于）|  
|**2**|>（大于）|  
|**3**|<（小于）|  
|**4**|>=（大于或等于）|  
|**5**|< = （小于或等于）|  
|**6**|LIKE|  
|**7**|不类似于|  
  
 [  **@value=** ]*值*  
 指定要在其上进行筛选的值。 数据类型*值*必须匹配要筛选的列的数据类型。 例如，如果在对象 ID 列上设置筛选器，则**int**数据类型，*值*必须**int**。如果*值*是**nvarchar**或**varbinary**，它可以具有的最大长度为 8000。  
  
 比较运算符为 LIKE 或 NOT LIKE 时，逻辑运算符可以包括“%”或其他适合 LIKE 运算的筛选器。  
  
 你可以指定 NULL 为*值*筛选出与 NULL 列值的事件。 仅**0** （= 等） 和**1** (<> 不等于) 运算符可为 null。 在这种情况下，这些运算符等同于 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 和 IS NOT NULL 运算符。  
  
 若要应用之间的列的值，范围筛选器**sp_trace_setfilter**必须执行两次 — 一次更高的比-或-等于 (> =) 比较运算符和较低的比-或-等于另一个时间 (< =) 运算符.  
  
 有关数据列数据类型的详细信息，请参阅[SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
## <a name="return-code-values"></a>返回代码值  
 下表说明在存储过程完成后用户可能获得的代码值。  
  
|返回代码|Description|  
|-----------------|-----------------|  
|0|没有错误。|  
|1|未知错误。|  
|2|本跟踪当前正在运行。 更改跟踪，在此时间将导致错误。|  
|4|指定的列不是有效的。|  
|5|不允许筛选指定的列。 此值返回只能从**sp_trace_setfilter**。|  
|6|指定的比较运算符无效。|  
|7|指定的逻辑运算符无效。|  
|9|指定的跟踪句柄无效。|  
|13|内存不足。 在没有足够内存执行指定的操作时返回此代码。|  
|16|该函数对此跟踪无效。|  
  
## <a name="remarks"></a>注释  
 **sp_trace_setfilter**是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存储执行的许多以前由早期版本中可用的扩展存储过程执行操作的过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 使用**sp_trace_setfilter**而不是**xp_trace_set\*筛选器**扩展存储的过程来创建，应用、 删除或操作筛选器中的跟踪。 有关详细信息，请参阅[筛选跟踪](../../relational-databases/sql-trace/filter-a-trace.md)。  
  
 一个执行过程中必须一起启用某个特定列的所有筛选器**sp_trace_setfilter**。 例如，如果用户想对应用程序名称列应用两个筛选器，对用户名列应用一个筛选器，则用户必须按顺序对应用程序名称指定筛选器。 如果用户试图在一次存储过程调用中先对应用程序名称指定一个筛选器，接着对用户名指定筛选器，然后对应用程序名称指定另一个筛选器，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误。  
  
 参数的所有 SQL 跟踪存储过程 (**sp_trace_xx**) 已严格类型化。 如果这些参数不是使用正确的输入参数数据类型（正如参数说明中指定的一样）调用的，则存储过程会返回错误。  
  
## <a name="permissions"></a>权限  
 用户必须拥有 ALTER TRACE 权限。  
  
## <a name="examples"></a>示例  
 以下示例对 Trace `1` 设置三个筛选器。 筛选器 `N'SQLT%'` 和 `N'MS%'` 使用“`AppName`”比较运算符对一列（`10`，其值为 `LIKE`）进行操作。 筛选器 `N'joe'` 使用“`UserName`”比较运算符对另一列（`11`，其值为 `EQUAL`）进行操作。  
  
```  
sp_trace_setfilter  1, 10, 0, 6, N'SQLT%';  
sp_trace_setfilter  1, 10, 0, 6, N'MS%';  
sp_trace_setfilter  1, 11, 0, 0, N'joe';  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.fn_trace_getfilterinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sys.fn_trace_getinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [SQL 跟踪](../../relational-databases/sql-trace/sql-trace.md)  
  
  
