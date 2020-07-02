---
title: sp_drop_agent_profile （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_drop_agent_profile
- sp_drop_agent_profile_TSQL
helpviewer_keywords:
- sp_drop_agent_profile
ms.assetid: b884f9ef-ae89-4cbc-a917-532c3ff6ed41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 57815e94737837ec9beb096f1a1840ffc46ad6a4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717314"
---
# <a name="sp_drop_agent_profile-transact-sql"></a>sp_drop_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  从**MSagent_profiles**表中删除配置文件。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_drop_agent_profile [ @profile_id = ] profile_id  
```  
  
## <a name="arguments"></a>自变量  
`[ @profile_id = ] profile_id`要删除的配置文件的 ID。 *profile_id*为**int**，没有默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_drop_agent_profile**在所有类型的复制中使用。  
  
 给定配置文件的参数也从**MSagent_parameters**表中删除。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能**sp_drop_agent_profile**执行。  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
