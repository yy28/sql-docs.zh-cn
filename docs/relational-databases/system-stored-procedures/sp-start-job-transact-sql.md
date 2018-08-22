---
title: sp_start_job (TRANSACT-SQL) |Microsoft Docs
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
- sp_start_job
- sp_start_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_start_job
ms.assetid: 8a91df6a-eb84-4512-9a17-4a6e32a9538a
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f640f88382653b5de1c70d1d9a22a8dbacbc283
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392051"
---
# <a name="spstartjob-transact-sql"></a>sp_start_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理立即执行作业。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_start_job   
     {   [@job_name =] 'job_name'  
       | [@job_id =] job_id }  
     [ , [@error_flag =] error_flag]  
     [ , [@server_name =] 'server_name']  
     [ , [@step_name =] 'step_name']  
     [ , [@output_flag =] output_flag]  
```  
  
## <a name="arguments"></a>参数  
 [ **@job_name=** ] **'***job_name***'**  
 要启动的作业的名称。 任一*job_id*或*job_name*必须指定，但不能同时指定两者。 *job_name*是**sysname**，默认值为 NULL。  
  
 [ **@job_id=** ] *job_id*  
 要启动的作业标识号。 任一*job_id*或*job_name*必须指定，但不能同时指定两者。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
 [ **@error_flag=** ] *error_flag*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@server_name=** ] **'***server_name***'**  
 启动作业的目标服务器。 *server_name*是**nvarchar （128)**，默认值为 NULL。 *server_name*必须是一个向其作业当前针对的目标服务器。  
  
 [ **@step_name=** ] **'***step_name***'**  
 开始执行作业的步骤名。 只应用于本地作业。 *step_name*是**sysname**，默认值为 NULL  
  
 [ **@output_flag=** ] *output_flag*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>Remarks  
 此存储的过程是在**msdb**数据库。  
  
## <a name="permissions"></a>Permissions  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 成员**SQLAgentUserRole**并**SQLAgentReaderRole**只能启动他们所拥有的作业。 成员**SQLAgentOperatorRole**可以启动包括由其他用户拥有的所有本地作业。 成员**sysadmin**可以启动所有本地和多服务器作业。  
  
## <a name="examples"></a>示例  
 以下示例启动名为 `Weekly Sales Data Backup` 的作业。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_delete_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_stop_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
