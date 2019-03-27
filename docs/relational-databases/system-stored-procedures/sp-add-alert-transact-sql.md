---
title: sp_add_alert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_alert
- sp_add_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_alert
ms.assetid: d9b41853-e22d-4813-a79f-57efb4511f09
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 750d299b951b403ed6fe51baa43b047505860c3f
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493799"
---
# <a name="spaddalert-transact-sql"></a>sp_add_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建一个警报。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_alert [ @name = ] 'name'   
     [ , [ @message_id = ] message_id ]   
     [ , [ @severity = ] severity ]   
     [ , [ @enabled = ] enabled ]  
     [ , [ @delay_between_responses = ] delay_between_responses ]   
     [ , [ @notification_message = ] 'notification_message' ]   
     [ , [ @include_event_description_in = ] include_event_description_in ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @event_description_keyword = ] 'event_description_keyword_pattern' ]   
     [ , { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ]   
     [ , [ @raise_snmp_trap = ] raise_snmp_trap ]   
     [ , [ @performance_condition = ] 'performance_condition' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @name = ] 'name'` 警报的名称。 该名称显示在为响应警报而发送的电子邮件或寻呼消息中。 它必须是唯一的并且可以包含百分比 (**%**) 字符。 *名称*是**sysname**，无默认值。  
  
`[ @message_id = ] message_id` 定义警报消息错误号。 (它通常与中的错误号相对应**sysmessages**表。)*message_id*是**int**，默认值为**0**。 如果*严重性*用来定义警报， *message_id*必须是**0**或为 NULL。  
  
> [!NOTE]  
>  仅**sysmessages**错误写入 Microsoft Windows 应用程序日志可能会导致发送警报。  
  
`[ @severity = ] severity` 严重级别 (从**1**通过**25**)，它定义警报。 任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]消息存储在**sysmessages**发送到的表[!INCLUDE[msCoName](../../includes/msconame-md.md)]使用指示的严重级别的 Windows 应用程序日志会导致发送警报。 *严重性*是**int**，默认值为 0。 如果*message_id*用来定义警报，*严重性*必须是**0**。  
  
`[ @enabled = ] enabled` 指示警报的当前状态。 *已启用*是**tinyint**，默认值为 1 （启用）。 如果**0**，警报未启用，并且不会激发。  
  
`[ @delay_between_responses = ] delay_between_responses` 等待期 （以秒为单位，警报响应之间）。 *delay_between_responses*是**int**，默认值为**0**，这意味着的响应 （警报的每个匹配项都生成响应） 之间不等待。 响应可以为下面的一种或两种形式：  
  
-   通过电子邮件或寻呼发送的一个或多个通知。  
  
-   要执行的作业。  
  
 例如，当警报在短时间内重复产生时，通过设置该值就有可能避免发送重复的电子邮件。  
  
`[ @notification_message = ] 'notification_message'` 发送给操作员的电子邮件的一部分的可选附加消息**网络发送**，或寻呼通知。 *notification_message*是**nvarchar(512)**，默认值为 NULL。 指定*notification_message*对于添加特殊说明如补救过程很有用。  
  
`[ @include_event_description_in = ] include_event_description_in` 是是否的说明[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]错误应包含在通知消息。 *include_event_description_in*是**tinyint**，默认值为**5** (电子邮件和**网络发送**)，并可以具有一个或多个值与组合**或**逻辑运算符。  
  
> [!IMPORTANT]
>  在 **的未来版本中，将从** 代理中删除寻呼程序和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net send [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]选项。 请避免在新的开发工作中使用这些功能，并考虑修改当前使用这些功能的应用程序。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|None|  
|**1**|电子邮件|  
|**2**|寻呼程序|  
|**4**|**net send**|  
  
`[ @database_name = ] 'database'` 在其中出现错误时必须触发该警报数据库。 如果*数据库*未提供，而不考虑发生错误的位置触发警报。 *数据库*是**sysname**。 不允许用方括号 ([ ]) 将名称括起来。 默认值为 NULL。  
  
`[ @event_description_keyword = ] 'event_description_keyword_pattern'` 一系列字符的说明[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]错误必须与之类似。 可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 表达式模式匹配字符。 *event_description_keyword_pattern*是**nvarchar(100)**，默认值为 NULL。 此参数可用于筛选对象名称 (例如， **%customer_table%**)。  
  
`[ @job_id = ] job_id` 作业以响应该警报而运行的作业标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
`[ @job_name = ] 'job_name'` 为了响应该警报而执行作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定，但不能同时指定两者。  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` 在中未实现[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本 7.0。 *raise_snmp_trap*是**tinyint**，默认值为 0。  
  
`[ @performance_condition = ] 'performance_condition'` 格式表示的值*itemcomparatorvalue*。 *performance_condition*是**nvarchar(512)** 默认值为 NULL，并包含这些元素。  
  
|格式元素|Description|  
|--------------------|-----------------|  
|*项*|性能对象、性能计数器或计数器的命名实例|  
|*Comparator*|下列运算符之一：>、< 或 =|  
|*ReplTest1*|计数器的数值|  
  
`[ @category_name = ] 'category'` 警报类别的名称。 *类别*是**sysname**，默认值为 NULL。  
  
`[ @wmi_namespace = ] 'wmi_namespace'` 事件的查询的 WMI 命名空间。 *wmi_namespace*是**sysname**，默认值为 NULL。 只支持本地服务器上的命名空间。  
  
`[ @wmi_query = ] 'wmi_query'` 指定警报的 WMI 事件查询。 *wmi_query*是**nvarchar(512)**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sp_add_alert**必须从运行**msdb**数据库。  
  
 在下列情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 应用程序产生的错误/消息将发送到 Windows 应用程序日志，并因此引发警报：  
  
-   严重级别为 19 或更高版本**sys.messages**错误  
  
-   任何使用 WITH LOG 语法调用的 RAISERROR 语句  
  
-   任何**sys.messages**错误修改或创建使用**sp_altermessage**  
  
-   记录使用的任何事件**xp_logevent**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一种易用的图形方式来管理整个警报系统，这也是配置警报基础结构的推荐方式。  
  
 如果一个警报没有正常工作，请检查：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务是否正在运行。  
  
-   事件是否出现在 Windows 应用程序日志中。  
  
-   警报是否已被启用。  
  
-   用 **xp_logevent** 生成的事件在 master 数据库中发生。 因此，除非警报的 **xp_logevent** 为 **@database_name** 或 NULL，否则 **@database_name** 不触发警报。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才能执行 **sp_add_alert**。  
  
## <a name="examples"></a>示例  
 以下示例在触发警报时添加一个运行 `Back up the AdventureWorks2012 Database` 作业的警报（测试警报）。  
  
> [!NOTE]  
>  此示例假定消息 55001 和 `Back up the AdventureWorks2012 Database` 作业已存在。 此示例只用于说明用途。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_alert  
    @name = N'Test Alert',  
    @message_id = 55001,   
   @severity = 0,   
   @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
   @job_name = N'Back up the AdventureWorks2012 Database' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_add_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
