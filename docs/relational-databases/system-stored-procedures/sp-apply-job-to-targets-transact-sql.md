---
title: "sp_apply_job_to_targets (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_apply_job_to_targets
- sp_apply_job_to_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_apply_job_to_targets
ms.assetid: 4a3e9173-7e3c-4100-a9ac-2f5d2c60a8b0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 341a14b2ae6aa3d551ab90d4ff2f931d617aa3f2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
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
 [ **@job_id =**] *job_id*  
 要应用于指定目标服务器或目标服务器组的作业的标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
 [ **@job_name =**] **'***job_name***'**  
 要应用于指定的相关目标服务器或目标服务器组的作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定，但不能同时指定。  
  
 [ **@target_server_groups =**]  **'***target_server_groups***'**  
 以逗号分隔的目标服务器组的列表，指定的作业将应用于这些服务器组。 *target_server_groups*是**nvarchar(2048)**，默认值为 NULL。  
  
 [ **@target_servers=** ] **'***target_servers***'**  
 以逗号分隔的目标服务器的列表，指定的作业将应用于这些服务器。 *target_servers*是**nvarchar(2048)**，默认值为 NULL。  
  
 [ **@operation=** ]  **'***operation***'**  
 确定是将指定的作业应用于指定的目标服务器或目标服务器组，还是将其从指定的目标服务器或目标服务器组中移除。 *操作*是**varchar(7)**，默认值为应用。 有效的操作是**应用**和**删除**。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_apply_job_to_targets**可以轻松地应用 （或删除） 作业从多个目标服务器，并且调用的替代方法**sp_add_jobserver** (或**sp_delete_jobserver**) 一次针对每个所需的目标服务器。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行此过程。  
  
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
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
