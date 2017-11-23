---
title: "sp_add_jobschedule (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/28/2016
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
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 63ebaeb737f3e1d1b6abbf2a8b4800161a82e9ef
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="spaddjobschedule-transact-sql"></a>sp_add_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建作业计划。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_jobschedule [ @job_id = ] job_id, | [ @job_name = ] 'job_name', [ @name = ] 'name'  
     [ , [ @enabled = ] enabled_flag ]  
     [ , [ @freq_type = ] frequency_type ]  
     [ , [ @freq_interval = ] frequency_interval ]  
     [ , [ @freq_subday_type = ] frequency_subday_type ]  
     [ , [ @freq_subday_interval = ] frequency_subday_interval ]  
     [ , [ @freq_relative_interval = ] frequency_relative_interval ]  
     [ , [ @freq_recurrence_factor = ] frequency_recurrence_factor ]  
     [ , [ @active_start_date = ] active_start_date ]  
     [ , [ @active_end_date = ] active_end_date ]  
     [ , [ @active_start_time = ] active_start_time ]  
     [ , [ @active_end_time = ] active_end_time ]  
     [ , [ @schedule_id = ] schedule_id OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@job_id=** ] *job_id*  
 添加计划的作业的作业标识号。 *job_id*是**uniqueidentifier**，无默认值。  
  
 [  **@job_name=** ] *job_name*  
 向其中添加计划的作业的名称。 *job_name*是**nvarchar （128)**，无默认值。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定，但不能同时指定。  
  
 [  **@name=** ] *名称*  
 计划名称。 *名称*是**nvarchar （128)**，无默认值。  
  
 [  **@enabled=** ] *enabled_flag*  
 指示计划的当前状态。 *enabled_flag*是**tinyint**，默认值为**1** （启用）。 如果**0**，不启用了计划。 禁用该计划时，将不运行作业。  
  
 [  **@freq_type=** ] *frequency_type*  
 指示作业执行时间的值。 *frequency_type*是**int**，默认值为**0**，和可以是以下值之一：  
  
|值|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**4**|每天|  
|**8**|每周|  
|**16**|每月|  
|**32**|每月，相对于*frequency_interval。*|  
|**64**|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务启动时运行。|  
|**128**|在计算机空闲时运行。|  
  
 [  **@freq_interval=** ] *frequency_interval*  
 执行作业的日期。 *frequency_interval*是**int**，默认值为 0，并且依赖于的值*frequency_type*按下表中所示：  
  
|值|效果|  
|-----------|------------|  
|**1** （一次）|*frequency_interval*未使用。|  
|**4** （每日）|每个*frequency_interval*天。|  
|**8** （每周一次）|*frequency_interval*是一个或多个以下 （使用 OR 逻辑运算符组合起来）：<br /><br /> 1 = 星期日<br /><br /> 2 = 星期一<br /><br /> 4 = 星期二<br /><br /> 8 = 星期三<br /><br /> 16 = 星期四<br /><br /> 32 = 星期五<br /><br /> 64 = 星期六|  
|**16** （按月）|上*frequency_interval*天的月份。|  
|**32** （每月相对）|*frequency_interval*是以下之一：<br /><br /> 1 = 星期日<br /><br /> 2 = 星期一<br /><br /> 3 = 星期二<br /><br /> 4 = 星期三<br /><br /> 5 = 星期四<br /><br /> 6 = 星期五<br /><br /> 7 = 星期六<br /><br /> 8 = 天<br /><br /> 9 = 工作日<br /><br /> 10 = 休息日|  
|**64** (时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务启动)|*frequency_interval*未使用。|  
|**128**|*frequency_interval*未使用。|  
  
 [  **@freq_subday_type=** ] *frequency_subday_type*  
 指定的单位*frequency_subday_interval*。 *frequency_subday_type*是**int**，无默认值，并且可为以下值之一：  
  
|值|说明（单位）|  
|-----------|--------------------------|  
|**0x1**|在指定的时间|  
|**0x4**|Minutes|  
|**0x8**|Hours|  
  
 [  **@freq_subday_interval=** ] *frequency_subday_interval*  
 数*frequency_subday_type*期间发生的作业的每个执行之间。 *frequency_subday_interval*是**int**，默认值为 0。  
  
 [  **@freq_relative_interval=** ] *frequency_relative_interval*  
 进一步定义*frequency_interval*时*frequency_type*设置为**32** （每月相对）。  
  
 *frequency_relative_interval*是**int**，无默认值，并且可为以下值之一：  
  
|值|说明（单位）|  
|-----------|--------------------------|  
|**1**|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
  
 *frequency_relative_interval*指示间隔的匹配项。 例如，如果*frequency_relative_interval*设置为**2**， *frequency_type*设置为**32**，和*frequency_间隔*设置为**3**，计划的作业将在每个月的第二个星期二发生。  
  
 [  **@freq_recurrence_factor=** ] *frequency_recurrence_factor*  
 作业执行计划之间相隔的周数或月数。 *frequency_recurrence_factor*仅当使用*frequency_type*设置为**8**， **16**，或**32**。 *frequency_recurrence_factor*是**int**，默认值为 0。  
  
 [  **@active_start_date=** ] *active_start_date*  
 哪些作业执行可以开始的日期。 *active_start_date*是**int**，无默认值。 日期的格式为 YYYYMMDD。 如果*active_start_date* ，则日期必须是大于或等于 19900101。  
  
 创建了计划后，请检查其开始日期，确认该日期是否正确。 详细信息，请参阅"计划开始日期"一节中[创建并将计划附加到作业](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)。  
  
 [  **@active_end_date=** ] *active_end_date*  
 可以在哪些作业停止执行的日期。 *active_end_date*是**int**，无默认值。 日期的格式为 YYYYMMDD。  
  
 [  **@active_start_time=** ] *active_start_time*  
 在时间和日期之间*active_start_date*和*active_end_date*开始作业执行。 *active_start_time*是**int**，无默认值。 其时间采用 24 小时制格式为 HHMMSS。  
  
 [  **@active_end_time=***active_end_time*  
 在时间和日期之间*active_start_date*和*active_end_date*以结束作业执行。 *active_end_time*是**int**，无默认值。 其时间采用 24 小时制格式为 HHMMSS。  
  
 [  **@schedule_id=***schedule_id***输出**  
 成功创建计划时分配给计划的计划标识号。 *schedule_id*是类型的一个输出变量**int**，无默认值。  
  
 [  **@schedule_uid** =] *schedule_uid***输出**  
 计划的唯一标识符。 *schedule_uid*是类型的变量**uniqueidentifier**。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 作业计划现在可以独立于作业进行管理。 若要向作业添加计划，使用**sp_add_schedule**以创建的计划和**sp_attach_schedule**以将计划附加到作业。  
  
## <a name="permissions"></a>Permissions  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
 
 ## <a name="example"></a>示例
 以下示例将分配到的作业计划`SaturdayReports`其将执行每个星期六的凌晨 2:00。
```tsql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>另请参阅  
 [创建并将计划附加到作业](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)   
 [计划作业](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)   
 [创建计划](http://msdn.microsoft.com/library/8c7ef3b3-c06d-4a27-802d-ed329dc86ef3)   
 [SQL Server 代理存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
