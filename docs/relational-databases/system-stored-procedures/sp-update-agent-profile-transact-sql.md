---
title: sp_update_agent_profile （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_update_agent_profile_TSQL
- sp_update_agent_profile
helpviewer_keywords:
- sp_update_agent_profile
ms.assetid: cc81f227-0df3-4151-bb4d-4f45ea997b71
author: stevestein
ms.author: sstein
ms.openlocfilehash: 835ae5b262426fabdc657e78f4961a7aafb14224
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006113"
---
# <a name="sp_update_agent_profile-transact-sql"></a>sp_update_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新复制代理所用的配置文件。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_update_agent_profile [@agent_type=] agent_type, [ @agent_id= ] agent_id, [ @profile_id= ] profile_id  
```  
  
## <a name="arguments"></a>参数  
 [ **\@agent_type =** ] **'***agent_type***'**  
 代理的类型。 *agent_type*的数据值为**int**，无默认值，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|快照代理。|  
|**2**|日志读取器代理。|  
|**3**|分发代理。|  
|**4**|合并代理。|  
|**9**|队列读取器代理。|  
  
 [ **\@agent_id =** ]*agent_id*  
 代理的 ID。 *agent_id*的值为**int**，无默认值。  
  
 [ **\@profile_id =** ]*profile_id*  
 代理应使用的配置文件的 ID。 *profile_id*的值为**int**，无默认值。 若要查看为每个代理定义的配置文件的列表，请使用[sp_help_agent_profile &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)。 有关系统配置文件的详细信息，请参阅[复制代理配置文件](../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_update_agent_profile**用于所有类型的复制。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能执行**sp_update_agent_profile**。  
  
## <a name="see-also"></a>请参阅  
 [复制代理配置文件](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
