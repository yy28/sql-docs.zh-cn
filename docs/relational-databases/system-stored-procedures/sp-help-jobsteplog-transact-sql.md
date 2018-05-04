---
title: sp_help_jobsteplog (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
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
- sp_help_jobsteplog_TSQL
- sp_help_jobsteplog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobsteplog
ms.assetid: 1a0be7b1-8f31-4b4c-aadb-586c0e00ed04
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d439a2fb01d2b6590a6bba226f98cf0a011657eb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpjobsteplog-transact-sql"></a>sp_help_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关特定元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理作业步骤日志。 **sp_help_jobsteplog**不返回实际的日志。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]  
     [ , [ @step_name = ] 'step_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@job_id =**] **'***job_id***'**  
 要为其返回作业步骤日志信息的作业标识号。 *job_id*是**int**，默认值为 NULL。  
  
 [ **@job_name =**] **'***job_name***'**  
 作业的名称。 *job_name*是**sysname**，默认值 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定，但不能同时指定。  
  
 [ **@step_id =**] *step_id*  
 作业中步骤的标识号。 如果尚未包括，则包括作业中的所有步骤。 *step_id*是**int**，默认值为 NULL。  
  
 [ **@step_name =**] **'***step_name***'**  
 作业中步骤的名称。 *step_name*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|作业的唯一标识符。|  
|**job_name**|**sysname**|作业的名称。|  
|**step_id**|**int**|作业中步骤的标识符。 例如，如果在步骤在作业中的第一步其*step_id*为 1。|  
|**step_name**|**sysname**|作业中的步骤名称。|  
|**step_uid**|**uniqueidentifier**|作业中步骤的唯一标识符（由系统生成）。|  
|**date_created**|**datetime**|创建步骤的日期。|  
|**date_modified**|**datetime**|上次修改步骤的日期。|  
|**log_size**|**float**|作业步骤日志的大小 (MB)。|  
|**日志**|**nvarchar(max)**|作业步骤日志输出。|  
  
## <a name="remarks"></a>注释  
 **sp_help_jobsteplog**处于**msdb**数据库。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 成员**SQLAgentUserRole**只能查看他们所拥有的作业步骤的作业步骤日志元数据。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returns-job-step-log-information-for-all-steps-in-a-specific-job"></a>A. 返回特定作业中所有步骤的作业步骤日志信息  
 以下示例返回作业 `Weekly Sales Data Backup` 的所有作业步骤日志信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-job-step-log-information-about-a-specific-job-step"></a>B. 返回有关特定作业步骤的作业步骤日志信息  
 以下示例返回作业 `Weekly Sales Data Backup` 的第一个作业步骤的作业步骤日志信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_jobstep &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_delete_jobsteplog &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)   
 [SQL Server 代理存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
