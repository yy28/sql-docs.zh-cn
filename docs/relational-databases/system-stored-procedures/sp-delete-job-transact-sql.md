---
title: sp_delete_job (Transact SQL) |Microsoft 文档
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
- sp_delete_job
- sp_delete_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_job
ms.assetid: b85db6e4-623c-41f1-9643-07e5ea38db09
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 90d213daa9d5a17a6630142e06e5b7ef441a9e9c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262910"
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
 [ **@job_id=** ] *job_id*  
 要删除的作业的标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
 [ **@job_name=** ] **'***job_name***'**  
 要删除的作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定; 不能同时指定。  
  
 [ **@originating_server=** ] **'***server***'**  
 供内部使用。  
  
 [  **@delete_history=** ] *delete_history*  
 指定是否删除作业的历史记录。 *delete_history*是**位**，默认值为**1**。 当*delete_history*是**1**，删除该作业的作业历史记录。 当*delete_history*是**0**，作业历史记录不会被删除。  
  
 请注意，将删除的作业，不会删除历史记录时有关作业的历史信息将不显示在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理图形用户界面作业历史记录，但信息将仍驻留在**sysjobhistory**表中**msdb**数据库。  
  
 [  **@delete_unused_schedule=** ] *delete_unused_schedule*  
 指定是否删除附加到该作业的计划（如果这些计划没有附加到任何其他作业）。 *delete_unused_schedule*是**位**，默认值为**1**。 当*delete_unused_schedule*是**1**，如果没有其他作业引用计划则会删除附加到此作业计划。 当*delete_unused_schedule*是**0**，计划不会被删除。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 **@originating_server**参数保留供内部使用。  
  
 **@delete_unused_schedule**自变量提供与以前版本的 SQL Server 的向后兼容性，通过自动删除未连接到任何作业的计划。 请注意，此参数默认为向后兼容行为。 若要保留未附加到作业的计划，你必须提供的值**0**作为**@delete_unused_schedule**自变量。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 为管理作业提供了一种图形化的简便方法，建议使用此方法来创建和管理作业基础结构。  
  
 此存储过程不能删除维护计划，也不能删除维护计划中包含的作业。 请改用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来删除维护计划。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [sp_add_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_help_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
