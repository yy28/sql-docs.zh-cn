---
description: sp_delete_jobschedule (Transact-SQL)
title: sp_delete_jobschedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobschedule
- sp_delete_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobschedule
ms.assetid: 82fbb48b-603a-4016-a7fb-1ce17fb76919
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ee25a531baeaf96b4090f0cb0f165e6cd4c8d203
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474402"
---
# <a name="sp_delete_jobschedule-transact-sql"></a>sp_delete_jobschedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  删除作业计划。  
  
 提供**sp_delete_jobschedule**仅用于向后兼容性。  
  
  
## <a name="remarks"></a>备注  
 作业计划现在可以独立于作业进行管理。 若要从作业中删除计划，请使用 **sp_detach_schedule**。 若要删除计划，请使用 **sp_delete_schedule**。  
  
> **注意： sp_delete_jobschedule** 不支持附加到多个作业的计划。 如果现有脚本调用 **sp_delete_jobschedule** 删除附加到多个作业的计划，则该过程将返回错误。  
  
## <a name="permissions"></a>权限  
 默认情况下， **sysadmin** 固定服务器角色的成员可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 **Sysadmin**角色的成员可以删除任何作业计划。 不是 **sysadmin** 角色成员的用户只能删除他们所拥有的作业计划。  
  
## <a name="see-also"></a>另请参阅  
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [查看或修改作业](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_help_jobschedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobschedule-transact-sql.md)   
 [sp_update_jobschedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-jobschedule-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
