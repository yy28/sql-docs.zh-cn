---
title: sp_add_agent_profile (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_add_agent_profile
- sp_add_agent_profile_TSQL
helpviewer_keywords:
- sp_add_agent_profile
ms.assetid: 5c246a33-2c21-4a77-9c2a-a2c9f0c5dda1
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 448b07e1538f3d50f0bb2eb48ca5156176605133
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spaddagentprofile-transact-sql"></a>sp_add_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为复制代理创建新的配置文件。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_agent_profile [ [ @profile_id= ] profile_id OUTPUT ]  
        , [ @profile_name= ] 'profile_name'   
        , [ @agent_type= ] 'agent_type' ]   
    [ , [ @profile_type= ] profile_type ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @default= ] default ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@profile_id=** ] *profile_id*  
 与新插入的配置文件关联的 ID。 *profile_id*是**int** ，是可选的输出参数。 如果指定该 ID，则值将设置为新的配置文件 ID。  
  
 [  **@profile_name=** ] *****profile_name*****  
 配置文件的名称。 *profile_name*是**sysname**，无默认值。  
  
 [ **@agent_type=** ] **'***agent_type***'**  
 复制代理的类型。 *agent_type*是**int**，无默认值，并且可为这些值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|快照代理|  
|**2**|日志读取器代理|  
|**3**|分发代理|  
|**4**|合并代理|  
|**9**|队列读取器代理|  
  
 [  **@profile_type=** ] *profile_type*  
 是一种配置文件。*profile_type*是**int**，默认值为**1**。  
  
 **0**指示系统配置文件。 **1**指示自定义配置文件。 可以使用此存储的过程; 创建仅自定义配置文件因此唯一有效的值是**1**。 仅[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建系统配置文件。  
  
 [  **@description=** ] *****说明*****  
 是配置文件的说明。 *说明*是**nvarchar(3000)**，无默认值。  
  
 [  **@default=** ]*默认*  
 指示配置文件是否为默认*agent_type * *。* *默认*是**位**，默认值为**0**。 **1**指示正在添加的配置文件将成为的通过指定的代理的新默认配置文件*agent_type*。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_add_agent_profile**快照复制、 事务复制和合并复制中使用。  
  
 自定义代理配置文件与默认代理参数值一起添加。 使用[sp_change_agent_parameter &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)若要更改这些默认值或[sp_add_agent_parameter &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)以添加其他参数。  
  
 当**sp_add_agent_profile**是执行，在新的自定义配置文件添加一个行[MSagent_profiles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)表和关联的默认参数配置文件添加到[MSagent_parameters &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md)表。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_add_agent_profile**。  
  
## <a name="see-also"></a>另请参阅  
 [使用复制代理配置文件](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [复制代理配置文件](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_change_agent_parameter &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)  
  
  
