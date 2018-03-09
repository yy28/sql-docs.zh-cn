---
title: "sp_update_agent_profile (Transact SQL) |Microsoft 文档"
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
- sp_update_agent_profile_TSQL
- sp_update_agent_profile
helpviewer_keywords:
- sp_update_agent_profile
ms.assetid: cc81f227-0df3-4151-bb4d-4f45ea997b71
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4f3088c28098611567b80de916b84b73800dc2e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spupdateagentprofile-transact-sql"></a>sp_update_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新复制代理所用的配置文件。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_update_agent_profile [@agent_type=] agent_type, [ @agent_id= ] agent_id, [ @profile_id= ] profile_id  
```  
  
## <a name="arguments"></a>参数  
 [**@agent_type=**] *agent_type*  
 代理的类型。 *agent_type*是**int**，无默认值，并且可为这些值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|快照代理。|  
|**2**|日志读取器代理。|  
|**3**|分发代理。|  
|**4**|合并代理。|  
|**9**|队列读取器代理。|  
  
 [**@agent_id=**] *agent_id*  
 是代理程序的 ID。 *agent_id*是**int**，无默认值。  
  
 [**@profile_id=**] *profile_id*  
 代理应使用的配置文件的 ID。 *profile_id*是**int**，无默认值。 若要查看每个代理定义的配置文件的列表，请使用[sp_help_agent_profile &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). 有关系统配置文件的详细信息，请参阅[复制代理配置文件](../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_update_agent_profile**在所有类型的复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_update_agent_profile**。  
  
## <a name="see-also"></a>另请参阅  
 [复制代理配置文件](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
