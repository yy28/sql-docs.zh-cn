---
title: sp_apply_job_to_targets （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_apply_job_to_targets
- sp_apply_job_to_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_apply_job_to_targets
ms.assetid: 4a3e9173-7e3c-4100-a9ac-2f5d2c60a8b0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dbefdf6a045dce468365aa585b7efad775709c2c
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85874924"
---
# <a name="sp_apply_job_to_targets-transact-sql"></a>sp_apply_job_to_targets (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  将作业应用于一个或多个目标服务器或属于一个或多个目标服务器组的目标服务器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_apply_job_to_targets { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]   
     [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>参数  
`[ @job_id = ] job_id`要应用于指定目标服务器或目标服务器组的作业的标识号。 *job_id*的值为**uniqueidentifier**，默认值为 NULL。  
  
`[ @job_name = ] 'job_name'`要应用于指定的关联目标服务器或目标服务器组的作业的名称。 *job_name*的默认值为**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  必须指定*job_id*或*job_name* ，但不能同时指定两者。  
  
`[ @target_server_groups = ] 'target_server_groups'`以逗号分隔的目标服务器组列表，指定的作业将应用于这些组。 *target_server_groups*的值为**nvarchar （2048）**，默认值为 NULL。  
  
`[ @target_servers = ] 'target_servers'`以逗号分隔的目标服务器列表，指定的作业将应用于这些服务器。 *target_servers*的值为**nvarchar （2048）**，默认值为 NULL。  
  
`[ @operation = ] 'operation'`指定的作业是否应该应用于指定的目标服务器或目标服务器组。 *操作*为**varchar （7）**，默认值为 APPLY。 有效操作是 "**应用**" 和 "**删除**"。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_apply_job_to_targets**提供了一种简单的方法来应用（或从多个目标服务器删除）作业，并且是一种为每个所需的目标服务器调用一次**sp_add_jobserver** （或**sp_delete_jobserver**）的替代方法。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能执行此过程。  
  
## <a name="examples"></a>示例  
 以下示例将以前创建的 `Backup Customer Information` 作业应用于 `Servers Maintaining Customer Information` 组中的所有目标服务器。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_apply_job_to_targets  
    @job_name = N'Backup Customer Information',  
    @target_server_groups = N'Servers Maintaining Customer Information',   
    @operation = N'APPLY' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
