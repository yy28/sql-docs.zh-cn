---
title: sp_syspolicy_repair_policy_automation (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_repair_policy_automation
- sp_syspolicy_repair_policy_automation_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_repair_policy_automation
ms.assetid: d81682e3-2444-4d66-ad00-1cf628632e8b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 67e73bd412299910b0fdd0927466ea953c7991fe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828155"
---
# <a name="spsyspolicyrepairpolicyautomation-transact-sql"></a>sp_syspolicy_repair_policy_automation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修复基于策略的管理中的策略自动化。 例如，您可以使用此存储过程修复与配置为使用“按计划”或“更改时”评估模式的策略相关联的触发器和作业。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syspolicy_repair_policy_automation  
```  
  
## <a name="arguments"></a>参数  
 该存储过程没有参数。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 您必须在 msdb 系统数据库的上下文中运行 sp_syspolicy_repair_policy_automation。  
  
## <a name="permissions"></a>Permissions  
 要求具有 PolicyAdministratorRole 固定数据库角色的成员身份。  
  
> [!IMPORTANT]  
>  可能的凭据提升：具有 PolicyAdministratorRole 角色的用户可以创建服务器触发器并计划策略执行，这可能会影响[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的正常运行。 例如，PolicyAdministratorRole 角色中的用户可以创建一个策略，它可能会禁止在[!INCLUDE[ssDE](../../includes/ssde-md.md)]中创建大多数对象。 由于此可能的凭据提升，应仅向可信任其控制的配置的用户授予 PolicyAdministratorRole 角色[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
## <a name="examples"></a>示例  
 下面的示例将修复策略自动化。  
  
```  
EXEC msdb.dbo.sp_syspolicy_repair_policy_automation;  
  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [基于策略的管理存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
