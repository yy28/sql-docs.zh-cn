---
title: sp_add_job (TRANSACT-SQL) |Microsoft 文档
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
- sp_add_job_TSQL
- sp_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_job
ms.assetid: 6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: baa693e0765a8796a4f6fbed3284d440f5a1327d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spaddjob-transact-sql"></a>sp_add_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  添加由 SQLServerAgent 服务执行的新作业。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_job [ @job_name = ] 'job_name'  
     [ , [ @enabled = ] enabled ]   
     [ , [ @description = ] 'description' ]   
     [ , [ @start_step_id = ] step_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @category_id = ] category_id ]   
     [ , [ @owner_login_name = ] 'login' ]   
     [ , [ @notify_level_eventlog = ] eventlog_level ]   
     [ , [ @notify_level_email = ] email_level ]   
     [ , [ @notify_level_netsend = ] netsend_level ]   
     [ , [ @notify_level_page = ] page_level ]   
     [ , [ @notify_email_operator_name = ] 'email_name' ]   
          [ , [ @notify_netsend_operator_name = ] 'netsend_name' ]   
     [ , [ @notify_page_operator_name = ] 'page_name' ]   
     [ , [ @delete_level = ] delete_level ]   
     [ , [ @job_id = ] job_id OUTPUT ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@job_name =** ] **'***job_name***'**  
 作业的名称。 名称必须是唯一的并且不能包含百分比 (**%**) 字符。 *job_name*是**nvarchar （128)**，无默认值。  
  
 [  **@enabled =** ]*启用*  
 指示添加的作业的状态。 *启用*是**tinyint**，默认值为 1 （已启用）。 如果**0**，该作业未启用，并且不会根据其计划运行; 但是，它可以手动运行。  
  
 [ **@description =** ] **'***description***'**  
 作业的说明。 *说明*是**nvarchar(512)**，默认值为 NULL。 如果*说明*是省略，将使用"没有描述"。  
  
 [ **@start_step_id =** ] *step_id*  
 作业中要执行的第一个步骤的标识号。 *step_id*是**int**，默认值为 1。  
  
 [ **@category_name =** ] **'***category***'**  
 作业的类别。 *类别*是**sysname**，默认值为 NULL。  
  
 [ **@category_id =** ] *category_id*  
 一种与语言无关的机制，用于指定作业类别。 *category_id*是**int**，默认值为 NULL。  
  
 [ **@owner_login_name =** ] **'***login***'**  
 拥有该作业的登录的名称。 *登录名*是**sysname**，默认值为 NULL，则它被解释为当前的登录名。 只有的成员**sysadmin**固定的服务器角色可以设置或更改的值**@owner_login_name**。 如果不是成员的用户的**sysadmin**角色设置或更改的值**@owner_login_name**，此存储过程的执行将失败并返回错误。  
  
 [ **@notify_level_eventlog =** ] *eventlog_level*  
 一个值，用于指示何时在 Microsoft Windows 应用程序日志中放入与该作业对应的项。 *eventlog_level*是**int**，并且可以为这些值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**0**|从不|  
|**1**|成功时|  
|**2** （默认值）|失败|  
|**3**|始终|  
  
 [ **@notify_level_email =** ] *email_level*  
 一个值，用于指示完成该作业后何时发送电子邮件。 *email_level*是**int**，默认值为**0**，永远不会指示。 *email_level*使用相同的值*eventlog_level*。  
  
 [ **@notify_level_netsend =** ] *netsend_level*  
 一个值，用于指示完成该作业后何时发送网络消息。 *netsend_level*是**int**，默认值为**0**，永远不会指示。 *netsend_level*使用相同的值*eventlog_level*。  
  
 [ **@notify_level_page =** ] *page_level*  
 一个值，用于指示完成该作业后何时发送寻呼。 *page_level*是**int**，默认值为**0**，永远不会指示。 *page_level*使用相同的值*eventlog_level*。  
  
 [ **@notify_email_operator_name =** ] **'***email_name***'**  
 若要向时发送电子邮件的人员的电子邮件名称*email_level*为止。 *email_name*是**sysname**，默认值为 NULL。  
  
 [ **@notify_netsend_operator_name =** ] **'***netsend_name***'**  
 完成该作业后接收到网络消息的操作员的名称。 *netsend_name*是**sysname**，默认值为 NULL。  
  
 [ **@notify_page_operator_name =** ] **'***page_name***'**  
 完成该作业后收到寻呼的接收人的名称。 *page_name*是**sysname**，默认值为 NULL。  
  
 [ **@delete_level =** ] *delete_level*  
 一个值，用于指示何时删除作业。 *delete_value*是**int**，默认值为 0，这意味着永远不会。 *delete_level*使用相同的值*eventlog_level*。  
  
> [!NOTE]  
>  当*delete_level*是**3**、 一次执行作业、 作业而不考虑任何计划定义。 而且，如果作业将自身删除，则将同时删除该作业的历史记录。  
  
 [ **@job_id =** ] *job_id***OUTPUT**  
 成功创建作业后分配给作业的作业标识号。 *job_id*是类型的一个输出变量**uniqueidentifier**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 **@originating_server** 中存在**sp_add_job，**但未列在自变量。 **@originating_server** 是保留供内部使用。  
  
 后**sp_add_job**已执行来添加作业， **sp_add_jobstep**可以用于添加作业执行活动的步骤。 **sp_add_jobschedule**可用于创建此计划[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务将使用来执行该作业。 使用**sp_add_jobserver**设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作业的执行位置的实例和**sp_delete_jobserver**若要删除的作业[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。  
  
 如果该作业将执行在多服务器环境中的一个或多个目标服务器上，使用**sp_apply_job_to_targets**设置目标服务器或目标的作业的服务器组。 若要从目标服务器或目标服务器组中删除作业，请使用**sp_remove_job_from_targets**。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 为管理作业提供了一种图形化的简便方法，建议使用此方法来创建和管理作业基础结构。  
  
## <a name="permissions"></a>权限  
 若要运行此存储的过程，用户必须是属于**sysadmin**固定服务器角色，或授予以下项之一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理固定数据库角色，驻留在**msdb**数据库：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关与每个这些固定相关联的特定权限的信息数据库角色，请参阅[SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 只有的成员**sysadmin**固定的服务器角色可以设置或更改的值**@owner_login_name**。 如果不是成员的用户的**sysadmin**角色设置或更改的值**@owner_login_name**，此存储过程的执行将失败并返回错误。  
  
## <a name="examples"></a>示例  
  
### <a name="a-adding-a-job"></a>A. 添加作业  
 此示例将添加一个名为 `NightlyBackups` 的新作业。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-adding-a-job-with-pager-e-mail-and-net-send-information"></a>B. 添加一个具有寻呼、电子邮件和网络发送信息的作业  
 该示例将创建一个名为 `Ad hoc Sales Data Backup` 的作业。如果该作业失败，则会通知 `François Ajenstat`（通过寻呼、电子邮件或网络弹出消息）；如果作业成功，则删除该作业。  
  
> [!NOTE]  
>  本例假定已经存在一个名为 `François Ajenstat` 的操作员和名为 `françoisa` 的登录名。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'Ad hoc Sales Data Backup',   
    @enabled = 1,  
    @description = N'Ad hoc backup of sales data',  
    @owner_login_name = N'françoisa',  
    @notify_level_eventlog = 2,  
    @notify_level_email = 2,  
    @notify_level_netsend = 2,  
    @notify_level_page = 2,  
    @notify_email_operator_name = N'François Ajenstat',  
    @notify_netsend_operator_name = N'François Ajenstat',   
    @notify_page_operator_name = N'François Ajenstat',  
    @delete_level = 1 ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobstep &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_apply_job_to_targets &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [sp_help_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
