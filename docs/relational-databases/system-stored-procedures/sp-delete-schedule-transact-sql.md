---
title: sp_delete_schedule (Transact SQL) |Microsoft 文档
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
- sp_delete_schedule
- sp_delete_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_schedule
ms.assetid: 18b2c985-47b8-49c8-82d1-8a4af3d7d33a
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a02340dd4d5ca2e17044f34e521bc9ead793ed50
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spdeleteschedule-transact-sql"></a>sp_delete_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除计划。  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_schedule { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @force_delete = ] force_delete  
```  
  
## <a name="arguments"></a>参数  
 [ **@schedule_id=** ] *schedule_id*  
 要删除的计划的标识号。 *schedule_id*是**int**，默认值为 NULL。  
  
> **注意：**任一*schedule_id*或*schedule_name*必须指定，但不能同时指定。  
  
 [  **@schedule_name=** ] *****schedule_name*****  
 要删除的计划的名称。 *schedule_name*是**sysname**，默认值为 NULL。  
  
> **注意：**任一*schedule_id*或*schedule_name*必须指定，但不能同时指定。  
  
 [ **@force_delete** = ] *force_delete*  
 指定当计划附加到作业时此过程是否会失败。 *Force_delete*位，默认值为**0**。 当*force_delete*是**0**，如果计划附加到一个作业，存储的过程将失败。 当*force_delete*是**1**，无论是否计划附加到一个作业删除该计划。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 默认情况下，如果将计划附加到作业，则无法删除计划。 若要删除附加到作业的计划，指定的值**1**为*force_delete*。 删除计划不会停止当前正在运行的作业。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 请注意，作业所有者可以将作业附加到计划以及从计划中分离作业，而不必要求也是计划所有者。 但是，计划不能删除如果分离会将其保留没有作业，除非调用方是计划所有者。  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 只有的成员**sysadmin**角色可以删除由另一个用户拥有的作业计划。  
  
## <a name="examples"></a>示例  
  
### <a name="a-deleting-a-schedule"></a>A. 删除计划  
 以下示例删除计划 `NightlyJobs`。 如果该计划已附加到任何作业，则此示例不会删除该计划。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="b-deleting-a-schedule-attached-to-a-job"></a>B. 删除附加到作业的计划  
 以下示例删除计划 `RunOnce`，无论该计划是否已附加到作业。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = 'RunOnce',  
    @force_delete = 1;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [执行作业](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [sp_add_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
  
