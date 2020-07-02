---
title: sp_purge_jobhistory （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 47952d7c246a0de94d4515774e89a185c0460f2a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783017"
---
# <a name="sp_purge_jobhistory-transact-sql"></a>sp_purge_jobhistory (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  删除作业的历史记录。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_purge_jobhistory   
   {   [ @job_name = ] 'job_name' |   
     | [ @job_id = ] job_id }  
   [ , [ @oldest_date = ] oldest_date ]  
```  
  
## <a name="arguments"></a>自变量  
`[ @job_name = ] 'job_name'`要删除其历史记录的作业的名称。 *job_name*的默认值为**sysname**，默认值为 NULL。 必须指定*job_id*或*job_name* ，但不能同时指定两者。  
  
> [!NOTE]  
>  **Sysadmin**固定服务器角色的成员或**SQLAgentOperatorRole**固定数据库角色的成员可以执行**sp_purge_jobhistory** ，而无需指定*job_name*或*job_id*。 如果**sysadmin**用户未指定这些参数，则所有本地作业和多服务器作业的作业历史记录在*oldest_date*指定的时间内被删除。 当**SQLAgentOperatorRole**用户未指定这些参数时，所有本地作业的作业历史记录将在*oldest_date*指定的时间内删除。  
  
`[ @job_id = ] job_id`要删除的记录的作业标识号。 *job_id*的值为**uniqueidentifier**，默认值为 NULL。 必须指定*job_id*或*job_name* ，但不能同时指定两者。 请参阅** \@ job_name**说明中的说明，了解**sysadmin**或**SQLAgentOperatorRole**用户可以使用此参数的相关信息。  
  
`[ @oldest_date = ] oldest_date`要保留在历史记录中的最早记录。 *oldest_date*为**datetime**，默认值为 NULL。 指定*oldest_date*时， **sp_purge_jobhistory**只删除早于指定值的记录。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 如果**sp_purge_jobhistory**成功完成，则返回一条消息。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有**sysadmin**固定服务器角色的成员或**SQLAgentOperatorRole**固定数据库角色的成员才可以执行此存储过程。 **Sysadmin**的成员可以清除所有本地和多服务器作业的作业历史记录。 **SQLAgentOperatorRole**的成员只能清除所有本地作业的作业历史记录。  
  
 其他用户（包括**SQLAgentUserRole**和**SQLAgentReaderRole**的成员）必须显式授予对**sp_purge_jobhistory**的 EXECUTE 权限。 当被授予对此存储过程的 EXECUTE 权限之后，这些成员只可以清除其所拥有作业的历史记录。  
  
 **SQLAgentUserRole**、 **SQLAgentReaderRole**和**SQLAgentOperatorRole**固定数据库角色在**msdb**数据库中。 有关其权限的详细信息，请参阅[SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
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
>  只有**sysadmin**固定服务器角色的成员和**SQLAgentOperatorRole**的成员才能删除所有作业的历史记录。 当**sysadmin**用户在没有参数的情况下执行此存储过程时，将清除所有本地作业和多服务器作业的历史记录。 当**SQLAgentOperatorRole**用户在没有参数的情况下执行此存储过程时，只会清除所有本地作业的作业历史记录。  
  
 以下示例将不带参数执行此过程以删除所有的历史记录。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobhistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [&#40;Transact-sql&#41;系统存储过程](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [GRANT 对象权限 (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  
