---
title: sp_help_agent_default (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_default
- sp_help_agent_default_TSQL
helpviewer_keywords:
- sp_help_agent_default
ms.assetid: 7ba55e39-05dd-43c7-b5da-b268ed8426dd
author: stevestein
ms.author: sstein
ms.openlocfilehash: c0797b8fe4a2ba496b28f0c347eb5349e77e91e0
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762765"
---
# <a name="sphelpagentdefault-transact-sql"></a>sp_help_agent_default (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  检索作为参数传递的代理类型的默认配置 ID。 此存储过程可在分发服务器的任意数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_agent_default [ @profile_id= ] profile_id OUTPUT   
        , [ @agent_type = ] agent_type  
```  
  
## <a name="arguments"></a>参数  
`[ @profile_id = ] _profile_idOUTPUT`代理类型的默认配置的 ID。 *profile_id*的值为**int**, 无默认值。*profile_id*也是一个输出参数, 它返回代理类型默认配置的 id。  
  
`[ @agent_type = ] 'agent_type'`代理的类型。 *agent_type*的数据值为**int**, 无默认值, 可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|快照代理。|  
|**2**|日志读取器代理。|  
|**3**|分发代理。|  
|**4**|合并代理。|  
|**9**|队列读取器代理|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或**1** (失败)  
  
## <a name="remarks"></a>备注  
 **sp_help_agent_default**用于所有类型的复制。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**replmonitor**固定数据库角色的成员才能执行**sp_help_agent_default**。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
