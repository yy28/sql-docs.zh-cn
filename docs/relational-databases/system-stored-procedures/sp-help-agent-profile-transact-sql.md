---
title: sp_help_agent_profile (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_profile
- sp_help_agent_profile_TSQL
helpviewer_keywords:
- sp_help_agent_profile
ms.assetid: 5637b671-4aa3-497e-9a1c-c99798a1afb4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d75fde4ff1ccabd56243e1a1ccdff8051923fefb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794889"
---
# <a name="sphelpagentprofile-transact-sql"></a>sp_help_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示指定代理的配置文件。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_agent_profile [ [ @agent_type = ] agent_type ]   
    [ , [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@agent_type=**] *agent_type*  
 代理的类型。 *agent_type*是**int**，默认值为**0**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|快照代理|  
|**2**|日志读取器代理|  
|**3**|分发代理|  
|**4**|合并代理|  
|**9**|队列读取器代理|  
  
 [  **@profile_id=**] *profile_id*  
 要显示的配置文件的 ID。 *profile_id*是**int**，默认值为 **-1**，这会返回中的所有配置文件**MSagent_profiles**表。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|配置文件的 ID。|  
|**profile_name**|**sysname**|对代理类型唯一。|  
|**agent_type**|**int**|**1** = 快照代理<br /><br /> **2** = 日志读取器代理<br /><br /> **3** = 分发代理<br /><br /> **4** = 合并代理<br /><br /> **9** = 队列读取器代理|  
|**类型**|**int**|**0** = 系统<br /><br /> **1** = 自定义|  
|**description**|**varchar(3000)**|配置文件的说明。|  
|**def_profile**|**bit**|指定该配置文件是否是该代理类型的默认值。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_help_agent_profile**用于所有类型的复制。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**replmonitor**固定的数据库角色可以执行**sp_help_agent_profile**。  
  
## <a name="see-also"></a>请参阅  
 [使用复制代理配置文件](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
