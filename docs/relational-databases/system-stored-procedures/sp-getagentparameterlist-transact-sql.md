---
description: sp_getagentparameterlist (Transact-SQL)
title: sp_getagentparameterlist (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getagentparameterlist
- sp_getagentparameterlist_TSQL
helpviewer_keywords:
- sp_getagentparameterlist
ms.assetid: 50d3d3c1-b9a1-417c-bad4-674089c9c60d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 111ced1495557fdbfe151ee54bec20786df5d685
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469439"
---
# <a name="sp_getagentparameterlist-transact-sql"></a>sp_getagentparameterlist (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  返回一个列表，其中包含可以在代理配置文件中为指定代理类型设置的所有复制代理参数。 此存储过程可在运行代理的分发服务器的任意数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_getagentparameterlist [ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>参数  
`[ @agent_type = ] 'agent_type'` 正在为其添加参数的复制代理。 *agent_type* 为 **int**，可以是下列值之一：  
  
|值|代理|  
|-----------|-----------|  
|**1**|快照|  
|**2**|日志读取器|  
|**3**|分发|  
|**4**|合并|  
|**9**|队列读取器|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="remarks"></a>备注  
  
## <a name="permissions"></a>权限  
 只有 **sysadmin** 固定服务器角色的成员才能 **sp_getagentparameter**执行。  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_add_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [复制代理配置文件](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
