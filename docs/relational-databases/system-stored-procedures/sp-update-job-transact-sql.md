---
title: sp_update_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_job
- sp_update_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_job
ms.assetid: cbdfea38-9e42-47f3-8fc8-5978b82e2623
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c12e078505c8049511e59973c26d6a1417c7eae0
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537849"
---
# <a name="spupdatejob-transact-sql"></a>sp_update_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改作业的属性。  
  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_update_job [ @job_id =] job_id | [@job_name =] 'job_name'  
     [, [@new_name =] 'new_name' ]   
     [, [@enabled =] enabled ]  
     [, [@description =] 'description' ]   
     [, [@start_step_id =] step_id ]  
     [, [@category_name =] 'category' ]   
     [, [@owner_login_name =] 'login' ]  
     [, [@notify_level_eventlog =] eventlog_level ]  
     [, [@notify_level_email =] email_level ]  
     [, [@notify_level_netsend =] netsend_level ]  
     [, [@notify_level_page =] page_level ]  
     [, [@notify_email_operator_name =] 'operator_name' ]  
     [, [@notify_netsend_operator_name =] 'netsend_operator' ]  
     [, [@notify_page_operator_name =] 'page_operator' ]  
     [, [@delete_level =] delete_level ]   
     [, [@automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>参数  
`[ @job_id = ] job_id` 要更新的作业标识号。 *job_id*是**uniqueidentifier**。  
  
`[ @job_name = ] 'job_name'` 作业的名称。 *job_name* is **nvarchar(128)**.  
  
> **注意**：任一*job_id*或*job_name*必须指定但不能同时指定两者。  
  
`[ @new_name = ] 'new_name'` 作业的新名称。 *new_name*是**nvarchar （128)**。  
  
`[ @enabled = ] enabled` 指定是否启用作业 (**1**) 或未启用 (**0**)。 *已启用*是**tinyint**。  
  
`[ @description = ] 'description'` 作业的说明。 *描述*是**nvarchar(512)**。  
  
`[ @start_step_id = ] step_id` 要执行的作业的第一个步骤的标识号。 *step_id*是**int**。  
  
`[ @category_name = ] 'category'` 作业的类别。 *类别*是**nvarchar （128)**。  
  
`[ @owner_login_name = ] 'login'` 拥有作业的登录名的名称。 *登录名*是**nvarchar （128)** 只有的成员**sysadmin**固定的服务器角色可以更改作业所有权。  
  
`[ @notify_level_eventlog = ] eventlog_level` 指定的项放入此作业在 Microsoft Windows 应用程序日志。 *eventlog_level*是**int**，可以是下列值之一。  
  
|ReplTest1|说明（操作）|  
|-----------|----------------------------|  
|**0**|从不|  
|**1**|成功时|  
|**2**|在失败|  
|**3**|始终|  
  
`[ @notify_level_email = ] email_level` 指定何时发送一封电子邮件时完成该作业。 *email_level*是**int**。*email_level*使用相同的值作为*eventlog_level*。  
  
`[ @notify_level_netsend = ] netsend_level` 指定何时发送网络消息的此作业完成后。 *netsend_level*是**int**。*netsend_level*使用相同的值作为*eventlog_level*。  
  
`[ @notify_level_page = ] page_level` 指定在完成该作业后发送页。 *page_level*是**int**。*page_level*使用相同的值作为*eventlog_level*。  
  
`[ @notify_email_operator_name = ] 'operator_name'` 其电子邮件时要发送到操作员的名称*email_level*为止。 *email_name*是**nvarchar （128)**。  
  
`[ @notify_netsend_operator_name = ] 'netsend_operator'` 向其发送网络消息的操作员的名称。 *netsend_operator* is **nvarchar(128)**.  
  
`[ @notify_page_operator_name = ] 'page_operator'` 向其发送一个页面的操作员的名称。 *page_operator* is **nvarchar(128)**.  
  
`[ @delete_level = ] delete_level` 指定何时删除作业。 *delete_value*是**int**。*delete_level*使用相同的值作为*eventlog_level*。  
  
`[ @automatic_post = ] automatic_post` 保留。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_update_job**必须从运行**msdb**数据库。  
  
 **sp_update_job**更改提供了哪些参数值的那些设置。 如果省略某一参数，则保留其当前设置。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有的成员**sysadmin**可以使用此存储的过程来编辑由其他用户拥有的作业的属性。  
  
## <a name="examples"></a>示例  
 下面的示例更改名称、 说明和已启用的作业状态`NightlyBackups`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_job  
    @job_name = N'NightlyBackups',  
    @new_name = N'NightlyBackups -- Disabled',  
    @description = N'Nightly backups disabled during server migration.',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_add_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
