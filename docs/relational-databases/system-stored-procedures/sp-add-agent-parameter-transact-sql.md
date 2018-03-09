---
title: "sp_add_agent_parameter (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_add_agent_parameter_TSQL
- sp_add_agent_parameter
helpviewer_keywords:
- sp_add_agent_parameter
ms.assetid: 055f4765-0574-47c3-bf7d-6ef6e9bd8b34
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3d3e893788ea8c8fe33e7f85c445953beb297e4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spaddagentparameter-transact-sql"></a>sp_add_agent_parameter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将新参数及其值添加到代理配置文件中。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_agent_parameter [ @profile_id = ] profile_id  
        , [ @parameter_name = ] 'parameter_name'   
        , [ @parameter_value = ] 'parameter_value'   
```  
  
## <a name="arguments"></a>参数  
 [  **@profile_id=** ] *profile_id*  
 是从配置文件的 ID **MSagent_profiles**表中**msdb**数据库。 *profile_id*是**int**，无默认值。  
  
 若要了解哪些代理，请键入此*profile_id*表示时，查找*profile_id*中[MSagent_profiles &#40;Transact SQL &#41;](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)表，并记下*agent_type*字段值。 这些值如下所示：  
  
|值|说明|  
|-----------|-----------------|  
|**1**|快照代理|  
|**2**|日志读取器代理|  
|**3**|分发代理|  
|**4**|合并代理|  
|**9**|队列读取器代理|  
  
 [  **@parameter_name=** ] *parameter_name*  
 为参数的名称。 *parameter_name*是**sysname**，无默认值。 已在系统配置文件中定义的参数的列表，请参阅[复制代理配置文件](../../relational-databases/replication/agents/replication-agent-profiles.md)。 若要查看每个代理的有效参数的完整列表，请参阅下列主题：  
  
-   [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [复制日志读取器代理](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [复制合并代理](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [复制队列读取器代理](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
 [  **@parameter_value=**] *parameter_value*  
 赋给参数的值。 *parameter_value*是**nvarchar （255)**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_add_agent_parameter**快照复制、 事务复制和合并复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_add_agent_parameter**。  
  
## <a name="see-also"></a>另请参阅  
 [使用复制代理配置文件](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [复制代理配置文件](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_change_agent_parameter &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
