---
title: sp_update_alert (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_alert_TSQL
- sp_update_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_alert
ms.assetid: 4bbaeaab-8aca-4c9e-abc1-82ce73090bd3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54d96cf86b55a7c5a24917672bcae470a3bf7335
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529569"
---
# <a name="spupdatealert-transact-sql"></a>sp_update_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新现有警报的设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_update_alert   
     [ @name =] 'name'   
     [ , [ @new_name =] 'new_name']   
     [ , [ @enabled =] enabled]   
     [ , [ @message_id =] message_id]   
     [ , [ @severity =] severity]   
     [ , [ @delay_between_responses =] delay_between_responses]   
     [ , [ @notification_message =] 'notification_message']   
     [ , [ @include_event_description_in =] include_event_description_in]   
     [ , [ @database_name =] 'database']   
     [ , [ @event_description_keyword =] 'event_description_keyword']   
     [ , [ @job_id =] job_id | [@job_name =] 'job_name']   
     [ , [ @occurrence_count = ] occurrence_count]   
     [ , [ @count_reset_date =] count_reset_date]   
     [ , [ @count_reset_time =] count_reset_time]   
     [ , [ @last_occurrence_date =] last_occurrence_date]   
     [ , [ @last_occurrence_time =] last_occurrence_time]   
     [ , [ @last_response_date =] last_response_date]   
     [ , [ @last_response_time =] last_response _time]  
     [ , [ @raise_snmp_trap =] raise_snmp_trap]  
     [ , [ @performance_condition =] 'performance_condition' ]   
     [ , [ @category_name =] 'category']  
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @name = ] 'name'` 要更新的警报的名称。 *名称*是**sysname**，无默认值。  
  
`[ @new_name = ] 'new_name'` 警报的新名称。 该名称必须是唯一的。 *new_name*是**sysname**，默认值为 NULL。  
  
`[ @enabled = ] enabled` 指定是否启用警报 (**1**) 或未启用 (**0**)。 *已启用*是**tinyint**，默认值为 NULL。 必须启用警报，才能激发警报。  
  
`[ @message_id = ] message_id` 警报定义新消息或错误号。 通常情况下， *message_id*中的错误号相对应**sysmessages**表。 *message_id*是**int**，默认值为 NULL。 可以使用 ID，仅当警报的严重性级别设置为一条消息**0**。  
  
`[ @severity = ] severity` 新的严重级别 (从**1**通过**25**) 为警报定义。 任何[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]消息发送到具有指定的严重级别的 Windows 应用程序日志会激活警报。 *严重性*是**int**，默认值为 NULL。 可以使用严重级别，仅当警报的消息 ID 设置为**0**。  
  
`[ @delay_between_responses = ] delay_between_responses` 新的等待时间，以秒为单位对警报的响应。 *delay_between_responses*是**int**，默认值为 NULL。  
  
`[ @notification_message = ] 'notification_message'` 其他消息发送给操作员的电子邮件的一部分的修订后的文本**网络发送**，或寻呼通知。 *notification_message*是**nvarchar(512)**，默认值为 NULL。  
  
`[ @include_event_description_in = ] include_event_description_in` 指定是否的说明[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]来自 Windows 应用程序日志错误应包括在通知消息。 *include_event_description_in*是**tinyint**，默认值为 NULL，并且可以是一个或多个值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|None|  
|**1**|电子邮件|  
|**2**|寻呼程序|  
|**4**|**net send**|  
|**7**|All|  
  
`[ @database_name = ] 'database'` 在其中出现错误时必须触发该警报的数据库的名称。 *数据库*是**sysname。** 不允许用方括号 ([ ]) 将名称括起来。 默认值为 NULL。  
  
`[ @event_description_keyword = ] 'event_description_keyword'` 必须在错误消息日志中错误的描述中找到的字符序列。 可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 表达式模式匹配字符。 *event_description_keyword*是**nvarchar(100)**，默认值为 NULL。 此参数可用于筛选对象名称 (例如， **%customer_table%**)。  
  
`[ @job_id = ] job_id` 作业标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。 如果*job_id*指定，则*job_name*必须省略。  
  
`[ @job_name = ] 'job_name'` 响应该警报而执行作业的名称。 *job_name*是**sysname**，默认值为 NULL。 如果*job_name*指定，则*job_id*必须省略。  
  
`[ @occurrence_count = ] occurrence_count` 重置警报发生的次数。 *occurrence_count*是**int**，默认值为 NULL，并且可以设置为仅**0**。  
  
`[ @count_reset_date = ] count_reset_date` 重置上次重置发生计数的日期。 *count_reset_date*是**int**，默认值为 NULL。  
  
`[ @count_reset_time = ] count_reset_time` 重置上次重置发生计数的时间。 *count_reset_time*是**int**，默认值为 NULL。  
  
`[ @last_occurrence_date = ] last_occurrence_date` 重置警报上一次发生的日期。 *last_occurrence_date*是**int**，默认值为 NULL，并且可以设置为仅**0**。  
  
`[ @last_occurrence_time = ] last_occurrence_time` 重置警报上一次发生的时间。 *last_occurrence_time*是**int**，默认值为 NULL，并且可以设置为仅**0**。  
  
`[ @last_response_date = ] last_response_date` 重置 SQLServerAgent 服务上次响应警报的日期。 *last_response_date*是**int**，默认值为 NULL，并且可以设置为仅**0**。  
  
`[ @last_response_time = ] last_response_time` 重置 SQLServerAgent 服务上次响应警报的时间。 *last_response_time*是**int**，默认值为 NULL，并且可以设置为仅**0**。  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` 保留。  
  
`[ @performance_condition = ] 'performance_condition'` 格式表示的值 **'***itemcomparatorvalue*****。 *performance_condition*是**nvarchar(512)**，默认值为 NULL，并包含这些元素。  
  
|格式元素|Description|  
|--------------------|-----------------|  
|*项*|性能对象、性能计数器或计数器的命名实例|  
|*Comparator*|以下运算符之一： **>**， **<**， **=**|  
|*ReplTest1*|计数器的数值|  
  
`[ @category_name = ] 'category'` 警报类别的名称。 *类别*是**sysname**默认值为 NULL。  
  
`[ @wmi_namespace = ] 'wmi_namespace'` 事件的查询的 WMI 命名空间。 *wmi_namespace*是**sysname**，默认值为 NULL。  
  
`[ @wmi_query = ] 'wmi_query'` 指定警报的 WMI 事件查询。 *wmi_query*是**nvarchar(512)**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 仅**sysmessages**写入到[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 应用程序日志能够激发警报。  
  
 **sp_update_alert**更改仅这些参数提供值的警报设置。 如果省略某一参数，则保留其当前设置。  
  
## <a name="permissions"></a>权限  
 若要运行此存储的过程，用户必须属于**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例将已启用的 `Test Alert` 设置更改为 `0`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_alert  
    @name = N'Test Alert',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_add_alert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
