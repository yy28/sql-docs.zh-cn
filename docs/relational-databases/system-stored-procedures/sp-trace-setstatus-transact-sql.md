---
title: sp_trace_setstatus (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setstatus_TSQL
- sp_trace_setstatus
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setstatus
ms.assetid: 29e7a7d7-b9c1-414a-968a-fc247769750d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1e6d3ed9c31307fb032d4ccc3cc950565c39c52c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095935"
---
# <a name="sptracesetstatus-transact-sql"></a>sp_trace_setstatus (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改指定跟踪的当前状态。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用扩展事件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_trace_setstatus [ @traceid = ] trace_id , [ @status = ] status  
```  
  
## <a name="arguments"></a>参数  
`[ @traceid = ] trace_id` 是要修改的 ID。 *trace_id*是**int**，无默认值。 用户采用该*trace_id*值来标识、 修改和控制跟踪。 有关检索*trace_id*，请参阅[sys.fn_trace_getinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)。  
  
`[ @status = ] status` 指定要在跟踪上实现的操作。 *状态*是**int**，无默认值。  
  
 下表列出了可以指定的状态。  
  
|“登录属性”|描述|  
|------------|-----------------|  
|**0**|停止指定的跟踪。|  
|**1**|启动指定的跟踪。|  
|**2**|关闭指定的跟踪并从服务器中删除其定义。|  
  
> [!NOTE]  
>  在关闭跟踪前首先必须先停止它。 在查看跟踪前首先必须先停止并关闭它。  
  
## <a name="return-code-values"></a>返回代码值  
 下表说明在存储过程完成后用户可能获得的代码值。  
  
|返回代码|描述|  
|-----------------|-----------------|  
|**0**|没有错误。|  
|**1**|未知错误。|  
|**8**|指定的状态无效。|  
|**9**|指定的跟踪句柄无效。|  
|**13**|内存不足。 在没有足够内存执行指定的操作时返回此代码。|  
  
 如果在跟踪中指定的状态，已存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将返回**0**。  
  
## <a name="remarks"></a>备注  
 参数的所有 SQL 跟踪存储过程 (**sp_trace_xx**) 已严格类型化。 如果没有用正确的输入参数数据类型（参数说明中指定的类型）来调用这些参数，则存储过程将返回错误。  
  
 有关使用跟踪存储过程的示例，请参阅[创建跟踪 (Transact-SQL)](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 用户必须拥有 ALTER TRACE 权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getfilterinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sp_trace_generateevent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [SQL 跟踪](../../relational-databases/sql-trace/sql-trace.md)  
  
  
