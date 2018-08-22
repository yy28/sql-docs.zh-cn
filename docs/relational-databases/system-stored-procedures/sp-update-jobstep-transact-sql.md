---
title: sp_update_jobstep (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43dfe2a04a6c4f12fad0df12c3cf520d7d08d7a7
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394433"
---
# <a name="spupdatejobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改执行自动活动的作业中某一步骤的设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_update_jobstep   
     {   [@job_id =] job_id   
       | [@job_name =] 'job_name' } ,  
     [@step_id =] step_id  
     [ , [@step_name =] 'step_name' ]  
     [ , [@subsystem =] 'subsystem' ]   
     [ , [@command =] 'command' ]  
     [ , [@additional_parameters =] 'parameters' ]  
     [ , [@cmdexec_success_code =] success_code ]  
     [ , [@on_success_action =] success_action ]   
     [ , [@on_success_step_id =] success_step_id ]  
     [ , [@on_fail_action =] fail_action ]   
     [ , [@on_fail_step_id =] fail_step_id ]  
     [ , [@server =] 'server' ]   
     [ , [@database_name =] 'database' ]  
     [ , [@database_user_name =] 'user' ]   
     [ , [@retry_attempts =] retry_attempts ]  
     [ , [@retry_interval =] retry_interval ]   
     [ , [@os_run_priority =] run_priority ]  
     [ , [@output_file_name =] 'file_name' ]   
     [ , [@flags =] flags ]  
     [ ,  {   [ @proxy_id = ] proxy_id   
            | [ @proxy_name = ] 'proxy_name' }   
```  
  
## <a name="arguments"></a>参数  
 [ **@job_id =**] *job_id*  
 步骤所属的作业的标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。 任一*job_id*或*job_name*必须指定但不能同时指定两者。  
  
 [ **@job_name =**] **'***job_name***'**  
 步骤所属的作业的名称。 *job_name*是**sysname**，默认值为 NULL。 任一*job_id*或*job_name*必须指定但不能同时指定两者。  
  
 [ **@step_id =**] *step_id*  
 要修改的作业步骤的标识号。 不能更改该标识号。 *step_id*是**int**，无默认值。  
  
 [ **@step_name =**] **'***step_name***'**  
 步骤的新名称。 *step_name*是**sysname**，默认值为 NULL。  
  
 [ **@subsystem =**] **'***subsystem***'**  
 使用 Microsoft SQL Server 代理执行子系统*命令*。 *子系统*是**nvarchar(40)**，默认值为 NULL。  
  
 [  **@command =**] **'***命令*****  
 通过执行命令*子系统*。 *命令*是**nvarchar （max)**，默认值为 NULL。  
  
 [ **@additional_parameters =**] **'***parameters***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@cmdexec_success_code =**] *success_code*  
 返回的值**CmdExec**子系统命令，以指示*命令*成功执行。 *success_code*是**int**，默认值为 NULL。  
  
 [ **@on_success_action =**] *success_action*  
 要在步骤成功时执行的操作。*success_action*是**tinyint**，默认值为 NULL，并且可以是下列值之一。  
  
|ReplTest1|说明（操作）|  
|-----------|----------------------------|  
|**1**|成功后退出。|  
|**2**|失败后退出。|  
|**3**|请转到下一步。|  
|**4**|转到步骤*success_step_id。*|  
  
 [ **@on_success_step_id =**] *success_step_id*  
 步骤成功时要执行此作业中步骤的标识号并*success_action*是**4**。 *success_step_id*是**int**，默认值为 NULL。  
  
 [ **@on_fail_action =**] *fail_action*  
 步骤失败时执行的操作。 *fail_action*是**tinyint**，默认值为 NULL 并且可以具有下列值之一。  
  
|ReplTest1|说明（操作）|  
|-----------|----------------------------|  
|**1**|成功后退出。|  
|**2**|失败后退出。|  
|**3**|请转到下一步。|  
|**4**|转到步骤*fail_step_id * *。*|  
  
 [ **@on_fail_step_id =**] *fail_step_id*  
 在此步骤失败时执行的作业步骤的标识号并*fail_action*是**4**。 *fail_step_id*是**int**，默认值为 NULL。  
  
 [ **@server =**] **'***server***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *服务器*是**nvarchar （128)**，默认值为 NULL。  
  
 [ **@database_name =**] **'***database***'**  
 要在其中执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 步骤的数据库的名称。 *数据库*是**sysname**。 不允许用方括号 ([ ]) 将名称括起来。 默认值为 NULL。  
  
 [ **@database_user_name =**] **'***user***'**  
 执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 步骤时要使用的用户帐户的名称。 *用户*是**sysname**，默认值为 NULL。  
  
 [ **@retry_attempts =**] *retry_attempts*  
 该步骤失败时要进行的重试次数。 *retry_attempts*是**int**，默认值为 NULL。  
  
 [ **@retry_interval =**] *retry_interval*  
 两次重试之间的间隔时间（分钟）。 *retry_interval*是**int**，默认值为 NULL。  
  
 [ **@os_run_priority =**] *run_priority*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@output_file_name =**] **'***file_name***'**  
 用于保存该步骤输出的文件的名称。 *file_name*是**nvarchar(200)**，默认值为 NULL。 此参数只对于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 CmdExec 子系统中运行的命令有效。  
  
 若要将 output_file_name 重新设置回 NULL，必须设置*output_file_name*为空字符串 () 或字符串的空白字符，但您不能使用**CHAR(32)** 函数。 例如，按如下所示将此参数设置为空字符串：  
  
 **@output_file_name = ' '**  
  
 [ **@flags =**] *flags*  
 控制行为的选项。 *标志*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0** （默认值）|覆盖输出文件。|  
|**2**|追加到输出文件|  
|**4**|将 Transact-SQL 作业步骤输出写入步骤历史记录|  
|**8**|将日志写入表（覆盖现有的历史记录）|  
|**16**|将日志写入表（追加到现有的历史记录）|  
  
 [ **@proxy_id**= ] *proxy_id*  
 作业步骤作为代理运行时，代理的 ID 号。 *proxy_id*是类型**int**，默认值为 NULL。 如果没有*proxy_id*指定，则没有*proxy_name*指定，且未*user_name*的服务帐户运行该作业步骤的指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理。  
  
 [ **@proxy_name**= ] **'***proxy_name***'**  
 作业步骤作为代理运行时，代理的名称。 *proxy_name*是类型**sysname**，默认值为 NULL。 如果没有*proxy_id*指定，则没有*proxy_name*指定，且未*user_name*的服务帐户运行该作业步骤的指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_update_jobstep**必须从运行**msdb**数据库。  
  
 更新作业步骤将增加作业的版本号。  
  
## <a name="permissions"></a>Permissions  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有的成员**sysadmin**可以更新其他用户拥有的作业步骤。  
  
 如果作业步骤需要访问代理，则该作业步骤的创建者必须拥有对该作业步骤的代理的访问权限。 除 Transact-SQL 之外的所有子系统都需要一个代理帐户。 成员**sysadmin**有权访问所有代理，并且可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理的代理服务帐户。  
  
## <a name="examples"></a>示例  
 下面的示例更改 `Weekly Sales Data Backup` 作业的第一步的重试次数。 在运行此示例后，重试次数将为 `10`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1,  
    @retry_attempts = 10 ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [查看或修改作业](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_delete_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
