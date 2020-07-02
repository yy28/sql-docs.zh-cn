---
title: sys. fn_trace_getfilterinfo （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 306357f87ffa30dbdd6fca302089cf0d8967242f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754021"
---
# <a name="sysfn_trace_getfilterinfo-transact-sql"></a>sys.fn_trace_getfilterinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  返回有关应用于指定跟踪的筛选器的信息。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用扩展事件。  
  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
fn_trace_getfilterinfo ( trace_id )  
```  
  
## <a name="arguments"></a>自变量  
 *trace_id*  
 跟踪的 ID。 *trace_id*为**int**，没有默认值。  
  
## <a name="tables-returned"></a>返回的表  
 返回以下信息。 有关列的详细信息，请参阅[&#40;transact-sql&#41;sp_trace_setfilter ](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**columnid**|**int**|应用筛选器的列的 ID。|  
|**logical_operator**|**int**|指定是否应用 AND 或 OR 运算符。|  
|**comparison_operator**|**int**|指定比较类型：<br /><br /> 0 = 等于<br /><br /> 1 = 不等于<br /><br /> 2 = 大于<br /><br /> 3 = 小于<br /><br /> 4 = 大于或等于<br /><br /> 5 = 小于或等于<br /><br /> 6 = 类似于<br /><br /> 7 = 不类似于|  
|value|**sql_variant**|指定应用筛选器的值。|  
  
## <a name="remarks"></a>备注  
 用户设置*trace_id*值以标识、修改和控制跟踪。 当传递特定跟踪的 ID 时， **fn_trace_getfilterinfo**返回有关该跟踪的任何筛选器的信息。 如果指定的跟踪没有筛选器，则此函数将返回空行集。 传递无效 ID 时，此函数将返回空行集。 有关跟踪的类似信息，请参阅[transact-sql&#41;&#40;fn_trace_getinfo ](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 要求对服务器具有 ALTER TRACE 权限。  
  
## <a name="examples"></a>示例  
 以下示例返回有关编号为 2 的跟踪的所有筛选器的信息。  
  
```  
SELECT * FROM fn_trace_getfilterinfo(2) ;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql 创建跟踪&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_create &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys. fn_trace_geteventinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys. fn_trace_getinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [sys. fn_trace_gettable &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)  
  
  
