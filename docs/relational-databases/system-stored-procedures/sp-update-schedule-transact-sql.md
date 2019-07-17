---
title: sp_update_schedule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_schedule
- sp_update_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_schedule
ms.assetid: 97b3119b-e43e-447a-bbfb-0b5499e2fefe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 51e21d189a9302c2dc7b74a013846460e9cb7bc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946645"
---
# <a name="spupdateschedule-transact-sql"></a>sp_update_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理计划设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_update_schedule   
    {   [ @schedule_id = ] schedule_id   
      | [ @name = ] 'schedule_name' }  
    [ , [ @new_name = ] new_name ]  
    [ , [ @enabled = ] enabled ]  
    [ , [ @freq_type = ] freq_type ]  
    [ , [ @freq_interval = ] freq_interval ]   
    [ , [ @freq_subday_type = ] freq_subday_type ]   
    [ , [ @freq_subday_interval = ] freq_subday_interval ]   
    [ , [ @freq_relative_interval = ] freq_relative_interval ]   
    [ , [ @freq_recurrence_factor = ] freq_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time = ] active_start_time ]   
    [ , [ @active_end_time = ] active_end_time ]   
    [ , [ @owner_login_name = ] 'owner_login_name' ]  
    [ , [ @automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>参数  
`[ @schedule_id = ] schedule_id` 要修改的计划的标识符。 *schedule_id*是**int**，无默认值。 任一*schedule_id*或*schedule_name*必须指定。  
  
`[ @name = ] 'schedule_name'` 要修改的计划的名称。 *schedule_name*是**sysname**，无默认值。 任一*schedule_id*或*schedule_name*必须指定。  
  
`[ @new_name = ] new_name` 计划的新名称。 *new_name*是**sysname**，默认值为 NULL。 当*new_name*为 NULL，计划的名称保持不变。  
  
`[ @enabled = ] enabled` 指示计划的当前状态。 *已启用*是**tinyint**，默认值为**1** （启用）。 如果**0**，不启用计划。 如果不启用计划，则作业不会按此计划运行。  
  
`[ @freq_type = ] freq_type` 指示作业时要执行的值。 *freq_type*是**int**，默认值为**0**，可以是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**4**|每天|  
|**8**|每周|  
|**16**|每月|  
|**32**|每月，相对于*freq 间隔*|  
|**64**|SQLServerAgent 服务启动时运行|  
|**128**|计算机空闲时运行|  
  
`[ @freq_interval = ] freq_interval` 执行作业的天数。 *freq_interval*是**int**，默认值为**0**，并取决于值*freq_type*。  
  
|值*freq_type*|在影响*freq_interval*|  
|---------------------------|--------------------------------|  
|**1** （一次）|*freq_interval*是未使用。|  
|**4** （每日）|每个*freq_interval*天。|  
|**8** （每周）|*freq_interval*是一个或多个以下 (结合**OR**逻辑运算符):<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **4** = 星期二<br /><br /> **8** = 星期三<br /><br /> **16** = 星期四<br /><br /> **32** = 星期五<br /><br /> **64** = 星期六|  
|**16** （每月）|上*freq_interval*天的月份。|  
|**32** （每月相对）|*freq_interval*是以下之一：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **3** = 星期二<br /><br /> **4** = 星期三<br /><br /> **5** = 星期四<br /><br /> **6** = 星期五<br /><br /> **7** = 星期六<br /><br /> **8** = 天<br /><br /> **9** = 工作日<br /><br /> **10** = 休息日|  
|**64** （SQLServerAgent 服务启动时）|*freq_interval*是未使用。|  
|**128**|*freq_interval*是未使用。|  
  
`[ @freq_subday_type = ] freq_subday_type` 指定的单位*freq_subday_interval * *。* *freq_subday_type*是**int**，默认值为**0**，可以是下列值之一。  
  
|ReplTest1|说明（单位）|  
|-----------|--------------------------|  
|**0x1**|在指定的时间|  
|**0x2**|Seconds|  
|**0x4**|Minutes|  
|**0x8**|Hours|  
  
`[ @freq_subday_interval = ] freq_subday_interval` 数*freq_subday_type*周期每次执行作业之间。 *freq_subday_interval*是**int**，默认值为**0**。  
  
`[ @freq_relative_interval = ] freq_relative_interval` 作业的匹配项*freq_interval*中每个月中，如果*freq_interval*是**32** （每月相对）。 *freq_relative_interval*是**int**，默认值为**0**，可以是下列值之一。  
  
|ReplTest1|说明（单位）|  
|-----------|--------------------------|  
|**1**|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
  
`[ @freq_recurrence_factor = ] freq_recurrence_factor` 周数或计划作业的执行之间的月数。 *freq_recurrence_factor*时才使用*freq_type*是**8**， **16**，或**32**。 *freq_recurrence_factor*是**int**，默认值为**0**。  
  
`[ @active_start_date = ] active_start_date` 可以开始执行作业的日期。 *active_start_date*是**int**，默认值为 NULL，表示今天的日期。 日期的格式为 YYYYMMDD。 如果*active_start_date*不为 NULL，日期必须大于或等于 19900101。  
  
 创建了计划后，请检查其开始日期，确认该日期是否正确。 详细信息，请参阅"计划开始日期"一节中[创建和计划附加到作业](../../ssms/agent/create-and-attach-schedules-to-jobs.md)。  
  
`[ @active_end_date = ] active_end_date` 可以在其停止执行作业的日期。 *active_end_date*是**int**，默认值为**99991231**，这指示年 12 月 31 日到 9999。 其格式为 YYYYMMDD。  
  
`[ @active_start_time = ] active_start_time` 之间的任何日期时间*active_start_date*并*active_end_date*开始执行作业。 *active_start_time*是**int**，默认值为 000000，指示上午 12:00:00 并且必须使用 HHMMSS 格式输入。  
  
`[ @active_end_time = ] active_end_time` 之间的任何日期时间*active_start_date*并*active_end_date*结束执行作业。 *active_end_time*是**int**，默认值为**235959**，指示 11:59:59 PM 并且必须使用 HHMMSS 格式输入。  
  
`[ @owner_login_name = ] 'owner_login_name']` 拥有计划的服务器主体的名称。 *owner_login_name*是**sysname**，默认值为 NULL，指示计划是否归创建者。  
  
`[ @automatic_post = ] automatic_post` 保留。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 所有使用该计划的作业将立即使用新设置。 但是，更改计划不会停止当前正在运行的作业。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有的成员**sysadmin**可以修改其他用户拥有的计划。  
  
## <a name="examples"></a>示例  
 下面的示例将 `NightlyJobs` 计划的启用状态更改为 `0`，并将所有者设置为 `terrid`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_schedule  
    @name = 'NightlyJobs',  
    @enabled = 0,  
    @owner_login_name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [创建并将计划附加到作业](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [计划作业](../../ssms/agent/schedule-a-job.md)   
 [创建计划](../../ssms/agent/create-a-schedule.md)   
 [SQL Server 代理存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobschedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
