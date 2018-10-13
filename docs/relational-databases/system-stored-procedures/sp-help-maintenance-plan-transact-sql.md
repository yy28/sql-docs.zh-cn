---
title: sp_help_maintenance_plan (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_maintenance_plan_TSQL
- sp_help_maintenance_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_maintenance_plan
ms.assetid: e972a510-960e-41d6-93c5-c71cd581a585
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9fac8fd56139b340df2a2c4cdcfc7376de02dcab
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2018
ms.locfileid: "49168847"
---
# <a name="sphelpmaintenanceplan-transact-sql"></a>sp_help_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关指定的维护计划的信息。 如果没有指定计划，那么该存储过程将返回有关所有维护计划的信息。  
  
> **注意：** 与数据库维护计划使用此存储的过程。 但此功能已由不使用此存储过程的维护计划取代。 可使用此过程对从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本升级的安装维护数据库维护计划。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@plan_id =**] **'**_计划\_id_  
 指定维护计划的计划 ID。 *plan_id*是**UNIQUEIDENTIFIER**。 默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 None  
  
## <a name="result-sets"></a>结果集  
 如果*plan_id*指定，则**sp_help_maintenance_plan**将返回三个表： 计划、 数据库和作业。  
  
### <a name="plan-table"></a>Plan 表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|维护计划 ID。|  
|**plan_name**|**sysname**|维护计划名称。|  
|**date_created**|**datetime**|创建维护计划的日期。|  
|**所有者**|**sysname**|维护计划的所有者。|  
|**max_history_rows**|**int**|在系统表中，为记录维护计划的历史记录所分配的最大行数。|  
|**remote_history_server**|**int**|可以写入历史报表的远程服务器的名称。|  
|**max_remote_history_rows**|**int**|可以写入历史报表的远程服务器上系统表所分配的最大行数。|  
|**user_defined_1**|**int**|默认值为 NULL。|  
|**user_defined_2**|**nvarchar(100)**|默认值为 NULL。|  
|**user_defined_3**|**datetime**|默认值为 NULL。|  
|**user_defined_4**|**uniqueidentifier**|默认值为 NULL。|  
  
### <a name="database-table"></a>Database 表  
  
|列名|Description|  
|-----------------|-----------------|  
|**database_name**|所有与维护计划相关的数据库的名称。 database_name 的数据类型为 sysname。|  
  
### <a name="job-table"></a>Job 表  
  
|列名|Description|  
|-----------------|-----------------|  
|**job_id**|所有与维护计划相关的作业的 ID。 *job_id*是**uniqueidentifier**。|  
  
## <a name="remarks"></a>备注  
 **sp_help_maintenance_plan**处于**msdb**数据库。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_help_maintenance_plan**。  
  
## <a name="examples"></a>示例  
 此示例提供有关维护计划 FAD6F2AB-3571-11D3-9D4A-00C04FB925FC 的说明性信息。  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>请参阅  
 [维护计划](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [数据库维护计划存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
