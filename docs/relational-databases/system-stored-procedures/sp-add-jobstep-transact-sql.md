---
title: sp_add_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobstep_TSQL
- sp_add_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobstep
ms.assetid: 97900032-523d-49d6-9865-2734fba1c755
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: afa9128537cf699277385de3b7dce6aabd900191
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494409"
---
# <a name="spaddjobstep-transact-sql"></a>sp_add_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在作业中添加步骤（操作）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_jobstep [ @job_id = ] job_id | [ @job_name = ] 'job_name'   
     [ , [ @step_id = ] step_id ]   
     { , [ @step_name = ] 'step_name' }   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @command = ] 'command' ]   
     [ , [ @additional_parameters = ] 'parameters' ]   
          [ , [ @cmdexec_success_code = ] code ]   
     [ , [ @on_success_action = ] success_action ]   
          [ , [ @on_success_step_id = ] success_step_id ]   
          [ , [ @on_fail_action = ] fail_action ]   
          [ , [ @on_fail_step_id = ] fail_step_id ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @database_user_name = ] 'user' ]   
     [ , [ @retry_attempts = ] retry_attempts ]   
     [ , [ @retry_interval = ] retry_interval ]   
     [ , [ @os_run_priority = ] run_priority ]   
     [ , [ @output_file_name = ] 'file_name' ]   
     [ , [ @flags = ] flags ]   
     [ , { [ @proxy_id = ] proxy_id   
         | [ @proxy_name = ] 'proxy_name' } ]  
```  
  
## <a name="arguments"></a>参数  
`[ @job_id = ] job_id` 要添加步骤的作业标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
`[ @job_name = ] 'job_name'` 要添加步骤的作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定，但不能同时指定两者。  
  
`[ @step_id = ] step_id` 作业步骤序列标识号。 步骤标识数字开始**1**并无间断递增。 如果在现有序列中插入一个步骤，则将自动调整序列号。 如果提供了值*step_id*未指定。 *step_id*是**int**，默认值为 NULL。  
  
`[ @step_name = ] 'step_name'` 步骤的名称。 *step_name*是**sysname**，无默认值。  
  
`[ @subsystem = ] 'subsystem'` 使用的子系统[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务，才能执行*命令*。 *子系统*是**nvarchar(40)**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|'**ACTIVESCRIPTING**|活动脚本<br /><br /> **\*\* 重要提示 \*\*** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|'**CMDEXEC**'|操作系统命令或可执行程序|  
|'**分发**|复制分发代理作业|  
|'**快照**|复制快照代理作业|  
|'**日志读取器**|复制日志读取器代理作业|  
|'**合并**|复制合并代理作业|  
|'**QueueReader**|复制队列读取器代理作业|  
|'**ANALYSISQUERY**|Analysis Services 查询 (MDX、DMX)。|  
|'**ANALYSISCOMMAND**|Analysis Services 命令 (XMLA)。|  
|'**Dts**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包执行|  
|'**PowerShell**|PowerShell 脚本|  
|'**TSQL**（默认值）|[!INCLUDE[tsql](../../includes/tsql-md.md)] 语句|  
  
`[ @command = ] 'command'` 执行的命令**SQLServerAgent**服务通过*子系统*。 *命令*是**nvarchar （max)**，默认值为 NULL。 SQL Server 代理提供标记替换功能；在编写软件程序时，它可提供与变量相同的灵活性。  
  
> [!IMPORTANT]  
>  作业步骤中使用的所有标记现在必须附带转义宏，否则，这些作业步骤将会失败。 此外，您现在还必须用括号将标记名称括起来，并在标记语法开头加上美元符号 (`$`)。 例如：  
>   
>  `$(ESCAPE_` *宏名* `(DATE))`  
  
 有关这些令牌和更新作业步骤以使用新的标记语法的详细信息，请参阅[作业步骤中使用令牌](../../ssms/agent/use-tokens-in-job-steps.md)。  
  
> [!IMPORTANT]  
>  对 Windows 事件日志拥有写入权限的任何 Windows 用户都可以访问由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理警报或 WMI 警报激活的作业步骤。 为了防范此安全隐患，默认情况下，可以在由警报激活的作业中使用的特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理标记已被禁用。 这些标记包括：A-DBN、A-SVR、A-ERR、A-SEV、A-MSG 和 WMI（属性）。 请注意，在此版本中，对标记的使用扩展至所有警报。  
>   
>  如果您需要使用这些标记，请首先确保只有可信任的 Windows 安全组（如 Administrators 组）成员才对安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机的事件日志拥有写入权限。 然后在对象资源管理器中右键单击“SQL Server 代理”，选择“属性”，并在“警报系统”页上选择“为警报的所有作业响应替换标记”以启用这些标记。  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *参数*是**ntext**，默认值为 NULL。  
  
`[ @cmdexec_success_code = ] code` 返回的值**CmdExec**子系统命令，以指示*命令*成功执行。 *代码*是**int**，默认值为**0**。  
  
`[ @on_success_action = ] success_action` 要在步骤成功时执行的操作。 *success_action*是**tinyint**，可以是下列值之一。  
  
|ReplTest1|说明（操作）|  
|-----------|----------------------------|  
|**1** （默认值）|成功后退出|  
|**2**|失败后退出|  
|**3**|转到下一步|  
|**4**|转到步骤*on_success_step_id*|  
  
`[ @on_success_step_id = ] success_step_id` 步骤成功时要执行此作业中步骤的 ID 和*success_action*是**4**。 *success_step_id*是**int**，默认值为**0**。  
  
`[ @on_fail_action = ] fail_action` 在步骤失败时要执行的操作。 *fail_action*是**tinyint**，可以是下列值之一。  
  
|ReplTest1|说明（操作）|  
|-----------|----------------------------|  
|**1**|成功后退出|  
|**2** （默认值）|失败后退出|  
|**3**|转到下一步|  
|**4**|转到步骤*on_fail_step_id*|  
  
`[ @on_fail_step_id = ] fail_step_id` 该步骤失败时要执行此作业中步骤的 ID 和*fail_action*是**4**。 *fail_step_id*是**int**，默认值为**0**。  
  
`[ @server = ] 'server'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *服务器*是**nvarchar(30)**，默认值为 NULL。  
  
`[ @database_name = ] 'database'` 在其中执行的数据库的名称[!INCLUDE[tsql](../../includes/tsql-md.md)]步骤。 *数据库*是**sysname**，默认值为 NULL，这种情况下**主**使用数据库。 不允许用方括号 ([ ]) 将名称括起来。 对于 ActiveX 作业步骤，*数据库*是该步骤使用的脚本语言的名称。  
  
`[ @database_user_name = ] 'user'` 若要在执行时使用的用户帐户的名称[!INCLUDE[tsql](../../includes/tsql-md.md)]步骤。 *用户*是**sysname**，默认值为 NULL。 当*用户*上为 NULL，在作业所有者的用户上下文中的步运行*数据库*。  只有在作业所有者是 SQL Server sysadmin 时，SQL Server 代理才包括此参数。 如果是这样，则给定的 Transact-SQL 步骤将在给定的 SQL Server 用户名的上下文中执行。 如果作业所有者不是 SQL Server sysadmin，则 TRANSACT-SQL 步骤将始终在拥有该作业的登录名的上下文中执行和@database_user_name参数将被忽略。  
  
`[ @retry_attempts = ] retry_attempts` 尝试使用此步骤失败时的重试数。 *retry_attempts*是**int**，默认值为**0**，指示不重试。  
  
`[ @retry_interval = ] retry_interval` 在重试尝试之间的分钟的时间量。 *retry_interval*是**int**，默认值为**0**，这表示**0**-分钟间隔。  
  
`[ @os_run_priority = ] run_priority` 保留。  
  
`[ @output_file_name = ] 'file_name'` 在其中保存该步骤的输出文件的名称。 *file_name*是**nvarchar(200)**，默认值为 NULL。 *file_name*可以包含一个或多个下列出的令牌*命令*。 仅上运行的命令中，此参数才有效[!INCLUDE[tsql](../../includes/tsql-md.md)]， **CmdExec**， **PowerShell**， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，或[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]子系统。  
  
`[ @flags = ] flags` 控制行为的选项。 *标志*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0** （默认值）|覆盖输出文件|  
|**2**|追加到输出文件|  
|**4**|将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作业步骤输出写入步骤历史记录|  
|**8**|将日志写入表（覆盖现有的历史记录）|  
|**16**|将日志写入表（追加到现有的历史记录）|  
|**32**|将所有输出写入作业历史记录|  
|**64**|创建一个 Windows 事件以便用作 Cmd jobstep 要中止的信号|  
  
`[ @proxy_id = ] proxy_id` 运行该作业步骤的代理 id 号。 *proxy_id*是类型**int**，默认值为 NULL。 如果没有*proxy_id*指定，则没有*proxy_name*指定，且未*user_name*的服务帐户运行该作业步骤的指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理。  
  
`[ @proxy_name = ] 'proxy_name'` 运行该作业步骤的代理的名称。 *proxy_name*是类型**sysname**，默认值为 NULL。 如果没有*proxy_id*指定，则没有*proxy_name*指定，且未*user_name*的服务帐户运行该作业步骤的指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sp_add_jobstep**必须从运行**msdb**数据库。  
  
 SQL Server Management Studio 为管理作业提供了一种图形化的简便方法，建议使用此方法来创建和管理作业基础结构。  
  
 作业步骤必须指定一个代理，除非作业步骤的创建者的成员，否则**sysadmin**固定的安全角色。  
  
 代理可以由标识*proxy_name*或*proxy_id*。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 作业步骤的创建者必须有权访问作业步骤的代理。 成员**sysadmin**固定的服务器角色有权访问所有代理。 其他用户必须经过显式授予才能访问代理。  
  
## <a name="examples"></a>示例  
 以下示例可创建一个作业步骤，将销售数据库的访问权限更改为只读。 此外，此示例还指定了 5 次重试，每次重试之间的间隔为 5 分钟。  
  
> [!NOTE]  
>  此示例假定`Weekly Sales Data Backup`作业已存在。  
  
```  
USE msdb;  
GO  
EXEC sp_add_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_name = N'Set database to read only',  
    @subsystem = N'TSQL',  
    @command = N'ALTER DATABASE SALES SET READ_ONLY',   
    @retry_attempts = 5,  
    @retry_interval = 5 ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [查看或修改作业](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
