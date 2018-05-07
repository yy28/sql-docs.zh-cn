---
title: sp_syspolicy_set_log_on_success (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_set_log_on_success_TSQL
- sp_syspolicy_set_log_on_success
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_set_log_on_success
ms.assetid: 6b33383b-5949-488a-a911-59299a270f46
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f4a5673eaea6d0bd77467274641b0c5dd10a55aa
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spsyspolicysetlogonsuccess-transact-sql"></a>sp_syspolicy_set_log_on_success (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定是否针对基于策略的管理将成功的策略评估记录在策略历史记录日志中。  
  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syspolicy_set_log_on_success [ @value = ] value  
```  
  
## <a name="arguments"></a>参数  
 [  **@value=** ]*值*  
 确定是否记录成功的策略评估。 *值*是**sqlvariant**，和可以是以下值之一：  
  
-   0 或 'false' = 不记录成功的策略评估。  
  
-   1 或 'true' = 记录成功的策略评估。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 您必须在 msdb 系统数据库的上下文中运行 sp_syspolicy_set_log_on_success。  
  
 当*值*仅设置为 0 或 'false'，失败策略评估都会记录。  
  
## <a name="permissions"></a>权限  
 要求具有 PolicyAdministratorRole 固定数据库角色的成员身份。  
  
> **重要说明!!** 可能的凭据提升：具有 PolicyAdministratorRole 角色的用户可以创建服务器触发器并计划策略执行，这可能会影响[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的正常运行。 例如，PolicyAdministratorRole 角色中的用户可以创建一个策略，它可能会禁止在[!INCLUDE[ssDE](../../includes/ssde-md.md)]中创建大多数对象。 由于凭据此可能提升，应仅向与控制的配置的受信任的用户授予 PolicyAdministratorRole 角色[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
## <a name="examples"></a>示例  
 下面的示例将启用成功的策略评估的日志记录。  
  
```  
EXEC msdb.dbo.sp_syspolicy_set_log_on_success @value = 1;  
  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [基于策略的管理存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_configure &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql.md)  
  
  
