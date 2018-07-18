---
title: sp_stop_job (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_stop_job_TSQL
- sp_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stop_job
ms.assetid: 64b4cc75-99a0-421e-b418-94e37595bbb0
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67e1476e8f0612796e3f31644aca192c2c25a90f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258692"
---
# <a name="spstopjob-transact-sql"></a>sp_stop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理停止执行作业。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_stop_job   
      [@job_name =] 'job_name'  
    | [@job_id =] job_id   
    | [@originating_server =] 'master_server'  
    | [@server_name =] 'target_server'  
```  
  
## <a name="arguments"></a>参数  
 [ **@job_name =**] **'***job_name***'**  
 要停止的作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
 [ **@job_id =**] *job_id*  
 要停止的作业的标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
 [ **@originating_server =**] **'***master_server***'**  
 主服务器的名称。 如果指定主服务器的名称，则将停止所有多服务器作业。 *master_server*是**nvarchar （128)**，默认值为 NULL。 仅在调用时，才指定此参数**sp_stop_job**在目标服务器。  
  
> [!NOTE]  
>  只能指定前三个参数之一。  
  
 [ **@server_name =**] **'***target_server***'**  
 要在其上停止多服务器作业的特定目标服务器的名称。 *target_server*是**nvarchar （128)**，默认值为 NULL。 仅在调用时，才指定此参数**sp_stop_job**在多服务器作业的主服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 **sp_stop_job**了停止信号发送至数据库。 某些进程可以立即停止和一些只有在达到稳定点 （或代码路径的入口点） 它们可以停止之前。 某些长时间运行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句（例如 BACKUP、RESTORE）和某些 DBCC 命令可能要花较长的时间才能完成。 这些运行时，它可能需要一些时间，取消作业之前。 停止作业导致在作业历史记录中记录“作业已取消”项。  
  
 如果作业当前正在执行的步骤类型**CmdExec**或**PowerShell**，正在运行的进程 (例如，MyProgram.exe) 强制提前结束。 提前结束可能导致不可预知的行为，如进程正在使用的文件保持为打开状态。 因此， **sp_stop_job**应使用仅在极端情况下，如果该作业所包含的类型的步骤**CmdExec**或**PowerShell**。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 成员**SQLAgentUserRole**和**SQLAgentReaderRole**只能停止他们拥有的作业。 成员**SQLAgentOperatorRole**可以停止包括那些由其他用户拥有的所有本地作业。 成员**sysadmin**可以停止所有本地和多服务器作业。  
  
## <a name="examples"></a>示例  
 以下示例将停止一个名为 `Weekly Sales Data Backup` 的作业。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_stop_job  
    N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_delete_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_start_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_update_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
