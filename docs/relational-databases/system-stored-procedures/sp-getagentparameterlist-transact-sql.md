---
title: sp_getagentparameterlist (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_getagentparameterlist
- sp_getagentparameterlist_TSQL
helpviewer_keywords:
- sp_getagentparameterlist
ms.assetid: 50d3d3c1-b9a1-417c-bad4-674089c9c60d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e512d0db07581ccc6b1a656a032d2e54f885b38d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833365"
---
# <a name="spgetagentparameterlist-transact-sql"></a>sp_getagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一个列表，其中包含可以在代理配置文件中为指定代理类型设置的所有复制代理参数。 此存储过程可在运行代理的分发服务器的任意数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_getagentparameterlist [ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>参数  
 [  **@agent_type =** ] **'***agent_type*****  
 要添加其参数的复制代理。 *agent_type*是**int**，可以是下列值之一：  
  
|ReplTest1|代理|  
|-----------|-----------|  
|**1**|快照|  
|**2**|日志读取器|  
|**3**|Distribution|  
|**4**|合并|  
|**9**|队列读取器|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_getagentparameter**。  
  
## <a name="see-also"></a>请参阅  
 [sp_add_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_add_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [复制代理配置文件](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
