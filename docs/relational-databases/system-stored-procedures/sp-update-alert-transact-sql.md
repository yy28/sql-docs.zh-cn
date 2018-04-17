---
title: sp_update_alert (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_alert_TSQL
- sp_update_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_alert
ms.assetid: 4bbaeaab-8aca-4c9e-abc1-82ce73090bd3
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64a669e37edf07ff897c94122e7e49d5899c1b6c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
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
 [ **@name =**] **'***name***'**  
 要更新的警报的名称。 *名称*是**sysname**，无默认值。  
  
 [ **@new_name =**] **'***new_name***'**  
 警报的新名称。 该名称必须是唯一的。 *new_name*是**sysname**，默认值为 NULL。  
  
 [  **@enabled =**]*启用*  
 指定是否启用了警报 (**1**) 或未启用 (**0**)。 *启用*是**tinyint**，默认值为 NULL。 必须启用警报，才能激发警报。  
  
 [ **@message_id =**] *message_id*  
 警报定义的新消息或错误号。 通常情况下， *message_id*对应于中的错误号**sysmessages**表。 *message_id*是**int**，默认值为 NULL。 可以使用 ID，仅当警报的严重性级别设置为一条消息**0**。  
  
 [  **@severity =**]*严重性*  
 一个新的严重性级别 (从**1**通过**25**) 为该警报定义。 任何[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]消息发送到指定的严重级别的 Windows 应用程序日志将激活警报。 *严重性*是**int**，默认值为 NULL。 可以使用的严重性级别，仅当警报的消息 ID 设置为**0**。  
  
 [ **@delay_between_responses =**] *delay_between_responses*  
 警报响应之间的新的等待间隔（以秒为单位）。 *delay_between_responses*是**int**，默认值为 NULL。  
  
 [ **@notification_message =**] **'***notification_message***'**  
 其他消息作为电子邮件的一部分发送给操作员的修订后的文本**网络发送**，或寻呼机通知。 *notification_message*是**nvarchar(512)**，默认值为 NULL。  
  
 [ **@include_event_description_in =**] *include_event_description_in*  
 指定是否应该在通知消息中包含 Windows 应用程序日志中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的说明。 *include_event_description_in*是**tinyint**，默认值为 NULL，并且可以是一个或多个值。  
  
|“值”|说明|  
|-----------|-----------------|  
|**0**|InclusionThresholdSetting|  
|**1**|电子邮件|  
|**2**|寻呼程序|  
|**4**|**net send**|  
|**7**|全部|  
  
 [ **@database_name =**] **'***database***'**  
 只有其中出现错误时才能激发警报的数据库的名称。 *数据库*是**sysname。** 不允许用方括号 ([ ]) 将名称括起来。 默认值为 NULL。  
  
 [ **@event_description_keyword =**] **'***event_description_keyword***'**  
 必须是在错误消息日志的错误说明中找到的字符序列。 可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 表达式模式匹配字符。 *event_description_keyword*是**nvarchar(100)**，默认值为 NULL。 此参数可用于筛选对象名称 (例如， **%customer_table%**)。  
  
 [ **@job_id =**] *job_id*  
 作业标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。 如果*job_id*指定，则*job_name*必须省略。  
  
 [ **@job_name =**] **'***job_name***'**  
 为响应该警报而执行的作业名称。 *job_name*是**sysname**，默认值为 NULL。 如果*job_name*指定，则*job_id*必须省略。  
  
 [ **@occurrence_count =** ] *occurrence_count*  
 重置警报发生的次数。 *occurrence_count*是**int**，默认值为 NULL，并且可以将仅为**0**。  
  
 [ **@count_reset_date =**] *count_reset_date*  
 重置上一次重置发生计数的日期。 *count_reset_date*是**int**，默认值为 NULL。  
  
 [ **@count_reset_time =**] *count_reset_time*  
 重置上一次重置发生计数的时间。 *count_reset_time*是**int**，默认值为 NULL。  
  
 [ **@last_occurrence_date =**] *last_occurrence_date*  
 重置上一次发生警报的日期。 *last_occurrence_date*是**int**，默认值为 NULL，并且可以将仅为**0**。  
  
 [ **@last_occurrence_time =**] *last_occurrence_time*  
 重置上一次发生警报的时间。 *last_occurrence_time*是**int**，默认值为 NULL，并且可以将仅为**0**。  
  
 [ **@last_response_date =**] *last_response_date*  
 重置 SQLServerAgent 服务上一次响应警报的日期。 *last_response_date*是**int**，默认值为 NULL，并且可以将仅为**0**。  
  
 [ **@last_response_time =**] *last_response_time*  
 重置 SQLServerAgent 服务上一次响应警报的时间。 *last_response_time*是**int**，默认值为 NULL，并且可以将仅为**0**。  
  
 [ **@raise_snmp_trap =**] *raise_snmp_trap*  
 保留。  
  
 [ **@performance_condition =**] **'***performance_condition***'**  
 一个表示格式值*****itemcomparatorvalue*****。 *performance_condition*是**nvarchar(512)**，默认值为 NULL，并且这些元素组成。  
  
|格式元素|Description|  
|--------------------|-----------------|  
|*项*|性能对象、性能计数器或计数器的命名实例|  
|*Comparator*|这些运算符之一： **>**， **<**， **=**|  
|*Value*|计数器的数值|  
  
 [ **@category_name =**] **'***category***'**  
 警报类别的名称。 *类别*是**sysname**默认值为 NULL。  
  
 [ **@wmi_namespace**= ] **'***wmi_namespace***'**  
 用于查询事件的 WMI 命名空间。 *wmi_namespace*是**sysname**，默认值为 NULL。  
  
 [ **@wmi_query**= ] **'***wmi_query***'**  
 用于指定警报的 WMI 事件的查询。 *wmi_query*是**nvarchar(512)**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 仅**sysmessages**写入[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 应用程序日志可能会引发警报。  
  
 **sp_update_alert**更改只有这些哪些参数提供值的警报设置。 如果省略某一参数，则保留其当前设置。  
  
## <a name="permissions"></a>权限  
 若要运行此存储的过程，用户必须是属于**sysadmin**固定的服务器角色。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [sp_add_alert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
