---
title: sp_help_schedule (Transact SQL) |Microsoft 文档
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
- sp_help_schedule
- sp_help_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_schedule
ms.assetid: b2fc4ce1-0a8e-44d2-b206-7dc7b258d8c9
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e39dd55a3794af5fdbe2188bc1a57773944ff8b4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpschedule-transact-sql"></a>sp_help_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出有关计划的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_schedule   
     [ @schedule_id = ] id ,  
     [ @schedule_name = ] 'schedule_name'   
     [ , [ @attached_schedules_only = ] attached_schedules_only ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@schedule_id =** ] *id*  
 要列出的计划的标识符。 *schedule_name*是**int**，无默认值。 任一*schedule_id*或*schedule_name*可指定。  
  
 [ **@schedule_name =** ] **'***schedule_name***'**  
 到列表计划的名称。 *schedule_name*是**sysname**，无默认值。 任一*schedule_id*或*schedule_name*可指定。  
  
 [ **@attached_schedules_only** =] *attached_schedules_only* ]  
 指定是否仅显示作业附加到的计划。 *attached_schedules_only*是**位**，默认值为**0**。 当*attached_schedules_only*是**0**，显示所有计划。 当*attached_schedules_only*是**1**，结果集包含附加到作业的计划。  
  
 [ **@include_description** =] *include_description*  
 指定是否在结果集中包含说明。 *include_description*是**位**，默认值为**0**。 当*include_description*是**0**、 *schedule_description*结果集的列都包含一个占位符。 当*include_description*是**1**，在结果集中包括的计划的说明。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 此过程返回以下结果集：  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|计划标识号。|  
|**schedule_uid**|**uniqueidentifier**|计划的标识符。|  
|**schedule_name**|**sysname**|计划名称。|  
|**enabled**|**int**|是否启用了计划 (**1**) 或未启用 (**0**)。|  
|**freq_type**|**int**|指示何时执行作业的值。<br /><br /> **1** = 一次<br /><br /> **4** = 每日<br /><br /> **8** = 每周<br /><br /> **16** = 每月<br /><br /> **32**相对于 = 每月、 **freq_interval**<br /><br /> **64** = SQLServerAgent 服务启动时运行。|  
|**freq_interval**|**int**|执行作业的天数。 值的值取决于**freq_type**。 有关详细信息，请参阅[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_type**|**int**|单位**freq_subday_interval**。 有关详细信息，请参阅[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_interval**|**int**|数**freq_subday_type**期间发生的作业的每个执行之间。 有关详细信息，请参阅[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_relative_interval**|**int**|计划作业的匹配项**freq_interval**中每个月。 有关详细信息，请参阅[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_recurrence_factor**|**int**|作业的已计划执行日期之间的间隔月数。|  
|**active_start_date**|**int**|激活计划的日期。|  
|**active_end_date**|**int**|计划的结束日期。|  
|**active_start_time**|**int**|计划开始的时间。|  
|**active_end_time**|**int**|计划结束的时间。|  
|**date_created**|**datetime**|创建计划的日期。|  
|**schedule_description**|**nvarchar(4000)**|对计划的英语说明（如果需要的话）。|  
|**job_count**|**int**|返回多少作业引用此计划。|  
  
## <a name="remarks"></a>注释  
 当未提供参数时， **sp_help_schedule**列出实例中的所有计划的信息。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 成员**SQLAgentUserRole**只能查看他们所拥有的计划。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-information-for-all-schedules-in-the-instance"></a>A. 列出实例中所有计划的信息  
 以下示例列出了实例中所有计划的信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-schedule"></a>B. 列出特定计划的信息  
 以下示例列出了名为 `NightlyJobs` 的计划的信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule 将&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
