---
title: sys.fn_trace_getfilterinfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_trace_getfilterinfo
- fn_trace_getfilterinfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], filters
- sys.fn_trace_getfilterinfo function
- filters [SQL Server], traces
- fn_trace_getfilterinfo function
ms.assetid: 09fe4a28-ff8a-4655-9da1-4654d5bc514d
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e29c80f8a8c0999e1c635c7271c48f4d87697283
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysfntracegetfilterinfo-transact-sql"></a>sys.fn_trace_getfilterinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关应用于指定跟踪的筛选器的信息。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用扩展事件。  
  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
fn_trace_getfilterinfo ( trace_id )  
```  
  
## <a name="arguments"></a>参数  
 *trace_id*  
 是的 ID。 *trace_id*是**int**，无默认值。  
  
## <a name="tables-returned"></a>返回的表  
 返回以下信息。 有关列的详细信息，请参阅[sp_trace_setfilter &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md).  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**columnid**|**int**|在其应用筛选器的列的 ID。|  
|**logical_operator**|**int**|指定是否应用 AND 或 OR 运算符。|  
|**comparison_operator**|**int**|指定比较类型：<br /><br /> 0 = 等于<br /><br /> 1 = 不等于<br /><br /> 2 = 大于<br /><br /> 3 = 小于<br /><br /> 4 = 大于或等于<br /><br /> 5 = 小于或等于<br /><br /> 6 = 类似于<br /><br /> 7 = 不类似于|  
|**值**|**sql_variant**|指定应用筛选器的值。|  
  
## <a name="remarks"></a>注释  
 用户集*trace_id*值来识别、 修改和控制跟踪。 传递特定的跟踪的 ID 时**fn_trace_getfilterinfo**返回该跟踪的任何筛选器信息。 如果指定的跟踪没有筛选器，则此函数将返回空行集。 传递无效 ID 时，此函数将返回空行集。 有关跟踪的类似信息，请参阅[sys.fn_trace_getinfo &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md).  
  
## <a name="permissions"></a>权限  
 要求对服务器具有 ALTER TRACE 权限。  
  
## <a name="examples"></a>示例  
 以下示例返回有关编号为 2 的跟踪的所有筛选器的信息。  
  
```  
SELECT * FROM fn_trace_getfilterinfo(2) ;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建跟踪 (Transact-SQL)](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [sp_trace_setfilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_create (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [sys.fn_trace_gettable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)  
  
  
