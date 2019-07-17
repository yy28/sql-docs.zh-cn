---
title: sp_trace_generateevent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_generateevent_TSQL
- sp_trace_generateevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_generateevent
ms.assetid: 3ef05bfb-b467-4403-89cc-6e77ef9247dd
author: stevestein
ms.author: sstein
ms.openlocfilehash: cfeacf9f3c18d3f80b7ad83a3697e33a5797ba22
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096022"
---
# <a name="sptracegenerateevent-transact-sql"></a>sp_trace_generateevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建用户定义事件。  
  
>**注意**：此存储过程**不**已弃用。 不推荐使用所有其他与跟踪相关的存储过程。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_trace_generateevent [ @eventid = ] event_id   
     [ , [ @userinfo = ] 'user_info' ]  
     [ , [ @userdata = ] user_data ]  
```  
  
## <a name="arguments"></a>参数  
`[ @eventid = ] event_id` 是要打开的事件的 ID。 *event_id*是**int**，无默认值。 ID 必须是一个从 82 到 91，表示为集的用户定义的事件的事件号[sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)。  
  
`[ @userinfo = ] 'user_info'` 用户定义的可选字符串，标识事件的原因。 *user_info*是**nvarchar （128)** ，默认值为 NULL。  
  
`[ @userdata = ] user_data` 是事件的可选用户定义数据。 *user_data*是**varbinary(8000)** ，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 下表说明在存储过程完成后用户可能获得的代码值。  
  
|返回代码|描述|  
|-----------------|-----------------|  
|**0**|没有错误。|  
|**1**|未知错误。|  
|**3**|指定的事件无效。 该事件可能不存在或者它不适用于此存储过程。|  
|**13**|内存不足。 在没有足够内存执行指定的操作时返回此代码。|  
  
## <a name="remarks"></a>备注  
 **sp_trace_generateevent**执行以前执行的操作的许多**xp_trace_\*** 扩展存储的过程。 使用**sp_trace_generateevent**而不是**xp_trace_generate_event**。  
  
 只有用户定义事件的 ID 号可能与一起使用**sp_trace_generateevent**。 如果使用其他事件 ID 号，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将产生错误。  
  
 参数的所有 SQL 跟踪存储过程 (**sp_trace_xx**) 已严格类型化。 如果没有用正确的输入参数数据类型（参数说明中指定的类型）来调用这些参数，则存储过程将返回错误。  
  
## <a name="permissions"></a>权限  
 用户必须拥有 ALTER TRACE 权限。  
  
## <a name="examples"></a>示例  
 以下示例对一个示例表创建用户可配置的事件。  
  
```  
--Create a sample table.  
CREATE TABLE user_config_test(col1 int, col2 char(10));  
  
--DROP the trigger if it already exists.  
IF EXISTS  
   (SELECT * FROM sysobjects WHERE name = 'userconfig_trg')  
   DROP TRIGGER userconfig_trg;  
  
--Create an ON INSERT trigger on the sample table.  
CREATE TRIGGER userconfig_trg  
   ON user_config_test FOR INSERT;  
AS  
EXEC master..sp_trace_generateevent  
   @event_class = 82, @userinfo = N'Inserted row into user_config_test';  
  
--When an insert action happens, the user-configurable event fires. If   
you were capturing the event id=82, you will see it in the Profiler output.  
INSERT INTO user_config_test VALUES(1, 'abc');  
```  
  
## <a name="see-also"></a>请参阅  
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SQL 跟踪](../../relational-databases/sql-trace/sql-trace.md)  
  
  
