---
title: sp_apply_job_to_targets (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f293e906d647d318bca5d730d0164b75cc88fc6f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62998027"
---
# <a name="spapplyjobtotargets-transact-sql"></a>sp_apply_job_to_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将作业应用于一个或多个目标服务器或属于一个或多个目标服务器组的目标服务器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_apply_job_to_targets { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]   
     [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>参数  
`[ @job_id = ] job_id` 要应用到指定的目标服务器或目标服务器组作业标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
`[ @job_name = ] 'job_name'` 要应用于指定的相关的目标服务器或目标服务器组的作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定，但不能同时指定两者。  
  
`[ @target_server_groups = ] 'target_server_groups'` 指定的作业是要应用的目标服务器组中的逗号分隔列表。 *target_server_groups*是**nvarchar(2048)**，默认值为 NULL。  
  
`[ @target_servers = ] 'target_servers'` 以逗号分隔的目标服务器指定的作业是要应用的列表。 *target_servers*是**nvarchar(2048)**，默认值为 NULL。  
  
`[ @operation = ] 'operation'` 是否应用于或从指定的目标服务器或目标服务器组中删除指定的作业。 *操作*是**varchar(7)**，使用默认值为 APPLY。 有效的操作是**APPLY**并**删除**。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_apply_job_to_targets**提供一种简便方法应用 （或删除） 某个作业从多个目标服务器，并且是调用的替代方法**sp_add_jobserver** (或**sp_delete_jobserver**)一次为每个所需的目标服务器。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色才能执行此过程。  
  
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
  
## <a name="see-also"></a>请参阅  
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
