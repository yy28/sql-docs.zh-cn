---
title: sp_delete_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_job
- sp_delete_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_job
ms.assetid: b85db6e4-623c-41f1-9643-07e5ea38db09
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b5ccd47f2b702c998a9e9268db523da1bfceaec
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536679"
---
# <a name="spdeletejob-transact-sql"></a>sp_delete_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除作业。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_job { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
     [ , [ @originating_server = ] 'server' ]   
     [ , [ @delete_history = ] delete_history ]  
     [ , [ @delete_unused_schedule = ] delete_unused_schedule ]  
```  
  
## <a name="arguments"></a>参数  
`[ @job_id = ] job_id` 是要删除作业的标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
`[ @job_name = ] 'job_name'` 是要删除的作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定; 不能同时指定两者。  
  
`[ @originating_server = ] 'server'` 供内部使用。  
  
`[ @delete_history = ] delete_history` 指定是否删除作业的历史记录。 *delete_history*是**位**，默认值为**1**。 当*delete_history*是**1**，删除该作业的作业历史记录。 当*delete_history*是**0**，不删除作业历史记录。  
  
 请注意，如果删除某个作业，不会删除历史记录作业的历史信息将不显示在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理图形用户界面作业历史记录，但信息仍可以驻留在**sysjobhistory**表中**msdb**数据库。  
  
`[ @delete_unused_schedule = ] delete_unused_schedule` 指定是否要删除计划附加到此作业是否它们未附加到任何其他作业。 *delete_unused_schedule*是**位**，默认值为**1**。 当*delete_unused_schedule*是**1**，如果没有其他作业引用计划，则删除附加到该作业的计划。 当*delete_unused_schedule*是**0**，将不删除计划。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **@originating_server**参数保留供内部使用。  
  
 **@delete_unused_schedule**参数通过自动删除未附加到任何作业的计划来提供与早期版本的 SQL Server 的向后兼容性。 请注意，此参数默认为向后兼容行为。 若要保留未附加到作业的计划，必须提供值**0**作为**@delete_unused_schedule**参数。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 为管理作业提供了一种图形化的简便方法，建议使用此方法来创建和管理作业基础结构。  
  
 此存储过程不能删除维护计划，也不能删除维护计划中包含的作业。 请改用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来删除维护计划。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 **sysadmin** 固定服务器角色成员可以通过执行 **sp_delete_job** 删除任何作业。 非 **sysadmin** 固定服务器角色成员的用户只能删除该用户所拥有的作业。  
  
## <a name="examples"></a>示例  
 以下示例删除作业 `NightlyBackups`。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_add_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
