---
title: "sp_attach_schedule (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_attach_schedule_TSQL
- sp_attach_schedule
dev_langs: TSQL
helpviewer_keywords: sp_attach_schedule
ms.assetid: 80c80eaf-cf23-4ed8-b8dd-65fe59830dd1
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e8359436d7e220c7bef3068ad9e73ded455ea497
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spattachschedule-transact-sql"></a>sp_attach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  设置一个作业计划。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_attach_schedule  
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     { [ @schedule_id = ] schedule_id   
     | [ @schedule_name = ] 'schedule_name' }  
```  
  
## <a name="arguments"></a>参数  
 [  **@job_id=** ] *job_id*  
 向其中添加计划的作业的标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
 [  **@job_name =** ] *job_name*  
 要向其添加计划作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定，但不能同时指定。  
  
 [  **@schedule_id =** ] *schedule_id*  
 为作业设置的计划的标识号。 *schedule_id*是**int**，默认值为 NULL。  
  
 [  **@schedule_name =** ] *schedule_name*  
 为作业设置的计划的名称。 *schedule_name*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*schedule_id*或*schedule_name*必须指定，但不能同时指定。  
  
## <a name="remarks"></a>注释  
 计划和作业的所有者必须相同。  
  
 可以为多个作业设置一个计划。 可以根据多个计划运行作业。  
  
 必须从运行此存储的过程**msdb**数据库。  
  
## <a name="permissions"></a>Permissions  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 请注意，作业所有者可以将作业附加到计划以及从计划中分离作业，而不必要求也是计划所有者。 但是，计划不能删除如果分离会将其保留没有作业，除非调用方是计划所有者。  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将检查用户是否同时拥有作业和计划。  
  
## <a name="examples"></a>示例  
 以下示例将创建一个名为 `NightlyJobs` 的计划： 使用此计划的作业每天在服务器上的时间为 `01:00` 时执行。 该示例将计划附加到作业 `BackupDatabase` 和作业 `RunReports`。  
  
> [!NOTE]  
>  此示例假定作业 `BackupDatabase` 和作业 `RunReports` 已存在。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_schedule &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_detach_schedule 将 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
