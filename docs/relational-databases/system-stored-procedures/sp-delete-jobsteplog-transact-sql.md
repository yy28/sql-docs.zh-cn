---
title: sp_delete_jobsteplog (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2d4284f32030339a5c60e211b911c5e7cd783b9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33257324"
---
# <a name="spdeletejobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除用参数指定的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤日志。 使用此存储的过程来维护**sysjobstepslogs**表中**msdb**数据库。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@job_id =**] **'***job_id***'**  
 包含要删除的作业步骤日志的作业的标识号。 *job_id*是**int**，默认值为 NULL。  
  
 [ **@job_name =**] **'***job_name***'**  
 作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> **注意：** 任一*job_id*或*job_name*必须指定，但不能同时指定。  
  
 [ **@step_id =**] *step_id*  
 要删除其作业步骤日志的作业中的步骤标识号。 如果不包含，除非删除在作业中的所有作业步骤日志**@older_than**或**@larger_than**指定。 *step_id*是**int**，默认值为 NULL。  
  
 [ **@step_name =**] **'***step_name***'**  
 将删除其作业步骤日志的作业中步骤的名称。 *step_name*是**sysname**，默认值为 NULL。  
  
> **注意：** 任一*step_id*或*step_name*可指定，但不能同时指定。  
  
 [ **@older_than =**] **'***date***'**  
 要保留的最早的作业步骤日志的日期和时间。 将删除早于该日期和时间的所有作业步骤日志。 *日期*是**datetime**，默认值为 NULL。 同时**@older_than**和**@larger_than**可以指定。  
  
 [  **@larger_than =**] *****size_in_bytes*****  
 要保留的最大作业步骤日志的大小（字节）。 大于此大小的所有作业步骤日志都会被删除。 同时**@larger_than**和**@older_than**可以指定。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 **sp_delete_jobsteplog**处于**msdb**数据库。  
  
 如果没有自变量除外**@job_id**或**@job_name**指定，删除所有指定作业的作业步骤日志。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 只有的成员**sysadmin**可以删除由另一个用户拥有的作业步骤日志。  
  
## <a name="examples"></a>示例  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>A. 删除作业中的所有作业步骤日志  
 以下示例删除作业 `Weekly Sales Data Backup` 的所有作业步骤日志。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup';  
GO  
```  
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>B. 删除特定作业步骤的作业步骤日志  
 以下示例删除作业 `Weekly Sales Data Backup` 中步骤 2 的作业步骤日志。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>C. 基于存在时间和大小删除所有作业步骤日志  
 以下示例从作业 `Weekly Sales Data Backup` 中删除时间早于 2005 年 10 月 25 日中午、大小大于 100 兆字节 (MB) 的所有作业步骤日志。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @older_than = '10/25/2005 12:00:00',  
    @larger_than = 104857600;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_help_jobsteplog &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [SQL Server 代理存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
