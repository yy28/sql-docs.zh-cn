---
title: sp_purge_jobhistory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_purge_jobhistory_TSQL
- sp_purge_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_jobhistory
ms.assetid: 237f9bad-636d-4262-9bfb-66c034a43e88
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab2f2fcb07fb181fd32d5a60f9fd2d8f25725f96
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535679"
---
# <a name="sppurgejobhistory-transact-sql"></a>sp_purge_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  删除作业的历史记录。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_purge_jobhistory   
   {   [ @job_name = ] 'job_name' |   
     | [ @job_id = ] job_id }  
   [ , [ @oldest_date = ] oldest_date ]  
```  
  
## <a name="arguments"></a>参数  
`[ @job_name = ] 'job_name'` 若要删除的历史记录的作业的名称。 *job_name*是**sysname**，默认值为 NULL。 任一*job_id*或*job_name*必须指定，但不能同时指定两者。  
  
> [!NOTE]  
>  成员**sysadmin**固定服务器角色或成员**SQLAgentOperatorRole**固定的数据库角色可以执行**sp_purge_jobhistory**而无需指定*job_name*或*job_id*。 当**sysadmin**用户未指定这些参数，在指定的时间内删除所有本地和多服务器作业的作业历史记录*oldest_date*。 当**SQLAgentOperatorRole**用户未指定这些参数，在指定的时间内删除所有本地作业的作业历史记录*oldest_date*。  
  
`[ @job_id = ] job_id` 要删除的记录作业作业标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。 任一*job_id*或*job_name*必须指定，但不能同时指定两者。 请参阅中的说明备注**@job_name**了解如何**sysadmin**或**SQLAgentOperatorRole**用户可以使用此参数。  
  
`[ @oldest_date = ] oldest_date` 历史记录中保留的最早记录。 *oldest_date*是**datetime**，默认值为 NULL。 当*oldest_date*指定，则**sp_purge_jobhistory**只会删除早于指定的值的记录。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 当**sp_purge_jobhistory**成功完成后，返回一条消息。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有的成员**sysadmin**固定的服务器角色或**SQLAgentOperatorRole**固定的数据库角色可以执行此存储的过程。 成员**sysadmin**可以清除所有本地和多服务器作业的作业历史记录。 成员**SQLAgentOperatorRole**可以清除仅所有本地作业的作业历史记录。  
  
 其他用户，包括的成员**SQLAgentUserRole**和的成员**SQLAgentReaderRole**，必须显式授予 EXECUTE 权限上**sp_purge_jobhistory**. 当被授予对此存储过程的 EXECUTE 权限之后，这些成员只可以清除其所拥有作业的历史记录。  
  
 **SQLAgentUserRole**， **SQLAgentReaderRole**，并**SQLAgentOperatorRole**固定的数据库角色位于**msdb**数据库。 其权限的详细信息，请参阅[SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-remove-history-for-a-specific-job"></a>A. 删除特定作业的历史记录  
 以下示例将删除名为 `NightlyBackups` 的作业的历史记录。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-remove-history-for-all-jobs"></a>B. 删除所有作业的历史记录  
  
> [!NOTE]  
>  只有的成员**sysadmin**固定服务器角色的成员以及**SQLAgentOperatorRole**可以删除所有作业的历史记录。 当**sysadmin**用户执行此存储的过程不带任何参数，清除所有本地和多服务器作业的作业历史记录。 当**SQLAgentOperatorRole**用户执行此存储的过程不带任何参数，清除所有本地作业的作业历史记录的仅。  
  
 以下示例将不带参数执行此过程以删除所有的历史记录。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [GRANT 对象权限 (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  
