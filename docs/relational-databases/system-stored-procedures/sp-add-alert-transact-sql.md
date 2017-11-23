---
title: "sp_add_alert (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_alert
- sp_add_alert_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_add_alert
ms.assetid: d9b41853-e22d-4813-a79f-57efb4511f09
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb817f23a97ff491c213cde35ba5e1d8eef4387b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
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
 [  **@name =** ] *名称*  
 警报的名称。 该名称显示在为响应警报而发送的电子邮件或寻呼消息中。 它必须是唯一的并且可以包含百分比 (**%**) 字符。 *名称*是**sysname**，无默认值。  
  
 [  **@message_id =** ] *message_id*  
 定义警报消息错误号。 (它通常对应于中的错误号**sysmessages**表。)*message_id*是**int**，默认值为**0**。 如果*严重性*用于定义该警报， *message_id*必须**0**或 NULL。  
  
> [!NOTE]  
>  仅**sysmessages**写入 Microsoft Windows 应用程序日志的错误可能会导致发送警报。  
  
 [  **@severity =** ]*严重性*  
 严重性级别 (从**1**通过**25**)，它定义警报。 任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]消息存储在**sysmessages**发送到的表[!INCLUDE[msCoName](../../includes/msconame-md.md)]指示严重级别的 Windows 应用程序日志会导致发送警报。 *严重性*是**int**，默认值为 0。 如果*message_id*用于定义该警报，*严重性*必须**0**。  
  
 [  **@enabled =** ]*启用*  
 指示警报的当前状态。 *启用*是**tinyint**，默认值为 1 （已启用）。 如果**0**，警报未启用，并且不会触发。  
  
 [  **@delay_between_responses =** ] *delay_between_responses*  
 警报响应之间的等待间隔（以秒为单位）。 *delay_between_responses*是**int**，默认值为**0**，这意味着没有无需任何等待两个响应 （警报的每个实例生成一个响应）。 响应可以为下面的一种或两种形式：  
  
-   通过电子邮件或寻呼发送的一个或多个通知。  
  
-   要执行的作业。  
  
 例如，当警报在短时间内重复产生时，通过设置该值就有可能避免发送重复的电子邮件。  
  
 [  **@notification_message =** ] *notification_message*  
 是一种可选的其他消息，向操作员发送的电子邮件，一部分**网络发送**，或寻呼机通知。 *notification_message*是**nvarchar(512)**，默认值为 NULL。 指定*notification_message*对于添加特殊的说明，如更正过程非常有用。  
  
 [  **@include_event_description_in =** ] *include_event_description_in*  
 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误说明是否应包含在通知消息中。 *include_event_description_in*是**tinyint**，默认值为**5** (电子邮件和**网络发送**)，并可以将一个或多个值结合**或**逻辑运算符。  
  
> [!IMPORTANT]  
>  在 **的未来版本中，将从** 代理中删除寻呼程序和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net send [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]选项。 请避免在新的开发工作中使用这些功能，并考虑修改当前使用这些功能的应用程序。  
  
|值|说明|  
|-----------|-----------------|  
|**0**|无|  
|**1**|电子邮件|  
|**2**|寻呼程序|  
|**4**|**net send**|  
  
 [  **@database_name =** ] *数据库*  
 只有其中出现错误时才能触发警报的数据库。 如果*数据库*未提供，无论该错误发生在触发警报。 *数据库*是**sysname**。 不允许用方括号 ([ ]) 将名称括起来。 默认值为 NULL。  
  
 [  **@event_description_keyword =** ] *event_description_keyword_pattern*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误说明必须与之类似的字符序列。 可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 表达式模式匹配字符。 *event_description_keyword_pattern*是**nvarchar(100)**，默认值为 NULL。 此参数可用于筛选对象名称 (例如， **%customer_table%**)。  
  
 [  **@job_id =** ] *job_id*  
 为响应该警报而运行的作业的标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
 [  **@job_name =** ] *job_name*  
 为响应该警报而执行的作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定，但不能同时指定。  
  
 [  **@raise_snmp_trap =** ] *raise_snmp_trap*  
 未在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版中实现。 *raise_snmp_trap*是**tinyint**，默认值为 0。  
  
 [  **@performance_condition =** ] *performance_condition*  
 是以格式表示的值*itemcomparatorvalue*。 *performance_condition*是**nvarchar(512)**默认值为 NULL，并且这些元素组成。  
  
|格式元素|Description|  
|--------------------|-----------------|  
|*项*|性能对象、性能计数器或计数器的命名实例|  
|*比较运算符*|下列运算符之一：>、< 或 =|  
|*值*|计数器的数值|  
  
 [  **@category_name =** ] *类别*  
 警报类别的名称。 *类别*是**sysname**，默认值为 NULL。  
  
 [  **@wmi_namespace** =] *wmi_namespace*  
 用于查询事件的 WMI 命名空间。 *wmi_namespace*是**sysname**，默认值为 NULL。 只支持本地服务器上的命名空间。  
  
 [  **@wmi_query** =] *wmi_query*  
 用于指定警报的 WMI 事件的查询。 *wmi_query*是**nvarchar(512)**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 **sp_add_alert**必须从运行**msdb**数据库。  
  
 在下列情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 应用程序产生的错误/消息将发送到 Windows 应用程序日志，并因此引发警报：  
  
-   19 或更高严重性**sys.messages**错误  
  
-   任何使用 WITH LOG 语法调用的 RAISERROR 语句  
  
-   任何**sys.messages**错误修改或创建使用**sp_altermessage**  
  
-   使用记入日志的任何事件**xp_logevent**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一种易用的图形方式来管理整个警报系统，这也是配置警报基础结构的推荐方式。  
  
 如果一个警报没有正常工作，请检查：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务是否正在运行。  
  
-   事件是否出现在 Windows 应用程序日志中。  
  
-   警报是否已被启用。  
  
-   用 **xp_logevent** 生成的事件在 master 数据库中发生。 因此，除非警报的 **xp_logevent** 为 **@database_name** 或 NULL，否则 **@database_name** 不触发警报。  
  
## <a name="permissions"></a>Permissions  
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
  
## <a name="see-also"></a>另请参阅  
 [sp_add_notification &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact SQL &#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
