---
title: sp_help_jobschedule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobschedule
- sp_help_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobschedule
ms.assetid: 2cded902-9272-4667-ac4b-a4f95a9f008e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1a327b07384ce2c12e64612b19c611c57dbbf18b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850365"
---
# <a name="sphelpjobschedule-transact-sql"></a>sp_help_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 用来执行自动活动的计划作业的信息。  
 
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_jobschedule { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @schedule_name = ] 'schedule_name' ]  
     [ , [ @schedule_id = ] schedule_id ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@job_id=** ] *job_id*  
 作业标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
 [ **@job_name=** ] **'***job_name***'**  
 作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> **注意：** 任一*job_id*或*job_name*必须指定，但不能同时指定两者。  
  
 [  **@schedule_name=** ] **'***schedule_name*****  
 作业的计划项的名称。 *schedule_name*是**sysname**，默认值为 NULL。  
  
 [ **@schedule_id=** ] *schedule_id*  
 作业的计划项的标识号。 *schedule_id*是**int**，默认值为 NULL。  
  
 [  **@include_description=** ] *include_description*  
 指定是否在结果集中包含计划的说明。 *include_description*是**位**，默认值为**0**。 当*include_description*是**0**，计划的说明不包括在结果集中。 当*include_description*是**1**，计划的说明包括在结果集中。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|计划标识号。|  
|**schedule_name**|**sysname**|计划名称。|  
|**enabled**|**int**|是否启用了计划 (**1**) 或未启用 (**0**)。|  
|**freq_type**|**int**|指示何时执行作业的值。<br /><br /> **1** = 一次<br /><br /> **4** = 每日<br /><br /> **8** = 每周<br /><br /> **16** = 每月<br /><br /> **32** = 每月，相对于**freq_interval**<br /><br /> **64** = 时，运行**SQLServerAgent**服务启动。|  
|**freq_interval**|**int**|执行作业的天数。 值对的值取决于**freq_type**。 有关详细信息，请参阅[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_type**|**int**|单位**freq_subday_interval**。 有关详细信息，请参阅[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_interval**|**int**|数**freq_subday_type**周期每次执行作业之间。 有关详细信息，请参阅[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_relative_interval**|**int**|计划作业的匹配项**freq_interval**中每个月。 有关详细信息，请参阅[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_recurrence_factor**|**int**|作业的已计划执行日期之间的间隔月数。|  
|**active_start_date**|**int**|激活计划的日期。|  
|**active_end_date**|**int**|计划的结束日期。|  
|**active_start_time**|**int**|计划开始的时间。|  
|**active_end_time**|**int**|计划结束的时间。|  
|**date_created**|**datetime**|创建计划的日期。|  
|**schedule_description**|**nvarchar(4000)**|中的值派生的计划的英文说明**msdb.dbo.sysschedules**。 当*include_description*是**0**，此列包含文本消息指出未请求说明。|  
|**next_run_date**|**int**|计划下一次引发作业运行的日期。|  
|**next_run_time**|**int**|计划下一次引发作业运行的时间。|  
|**schedule_uid**|**uniqueidentifier**|计划的标识符。|  
|**job_count**|**int**|返回的作业数。|  
  
> **注意：****sp_help_jobschedule**中的值将返回**dbo.sysjobschedules**并**dbo.sysschedules**系统表中**msdb**.   **sysjobschedules**更新每隔 20 分钟。 这可能会影响此存储过程返回的值。  
  
## <a name="remarks"></a>备注  
 参数**sp_help_jobschedule**可以仅在某些组合中使用。 如果*schedule_id*指定，则既不*job_id*也不*job_name*可以指定。 否则为*job_id*或*job_name*参数，可用于*schedule_name*。  
  
## <a name="permissions"></a>Permissions  
 要求具有 **sysadmin** 固定服务器角色的成员身份。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 成员**SQLAgentUserRole**只能查看他们所拥有的作业计划的属性。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-job-schedule-for-a-specific-job"></a>A. 返回特定作业的作业计划  
 以下示例返回名为 `BackupDatabase` 的作业的计划信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'BackupDatabase' ;  
GO  
```  
  
### <a name="b-returning-the-job-schedule-for-a-specific-schedule"></a>B. 返回特定计划的作业计划  
 下面的示例返回名为 `NightlyJobs` 的计划和名为 `RunReports` 的作业的信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule   
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="c-returning-the-job-schedule-and-schedule-description-for-a-specific-schedule"></a>C. 返回特定计划的作业计划和计划说明  
 下面的示例返回名为 `NightlyJobs` 的计划和名为 `RunReports` 的作业的信息。 返回的结果集包括对计划的说明。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs',  
    @include_description = 1 ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_update_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
