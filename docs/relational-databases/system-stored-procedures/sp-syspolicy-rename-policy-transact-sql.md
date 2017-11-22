---
title: "sp_syspolicy_rename_policy (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_rename_policy_TSQL
- sp_syspolicy_rename_policy
dev_langs: TSQL
helpviewer_keywords: sp_syspolicy_rename_policy
ms.assetid: ce2b07f5-23b1-4f49-8e7b-c18cf3f3d45b
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd1296c5d0a7fc4d1798b88fc1bb8f34c9b09b0b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="spsyspolicyrenamepolicy-transact-sql"></a>sp_syspolicy_rename_policy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在基于策略的管理中重命名现有策略。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syspolicy_rename_policy { [ @name = ] 'name' | [ @policy_id = ] policy_id }  
    , [ @new_name = ] 'new_name'  
```  
  
## <a name="arguments"></a>参数  
 [  **@name=** ] *名称*  
 您要重命名的策略的名称。 *名称*是**sysname**，并且如果必须指定*policy_id*为 NULL。  
  
 [  **@policy_id=** ] *policy_id*  
 您要重命名的策略的标识符。 *policy_id*是**int**，并且如果必须指定*名称*为 NULL。  
  
 [  **@new_name=** ] *new_name*  
 是为策略的新名称。 *new_name*是**sysname**，和是必需的。 不能为 NULL 或空字符串。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 您必须在 msdb 系统数据库的上下文中运行 sp_syspolicy_rename_policy。  
  
 必须为指定值*名称*或*policy_id*。 两者不能均为 NULL。 若要获取这些值，请查询 msdb.dbo.syspolicy_policies 系统视图。  
  
## <a name="permissions"></a>Permissions  
 要求具有 PolicyAdministratorRole 固定数据库角色的成员身份。  
  
> [!IMPORTANT]  
>  可能的凭据提升：具有 PolicyAdministratorRole 角色的用户可以创建服务器触发器并计划策略执行，这可能会影响[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的正常运行。 例如，PolicyAdministratorRole 角色中的用户可以创建一个策略，它可能会禁止在[!INCLUDE[ssDE](../../includes/ssde-md.md)]中创建大多数对象。 由于凭据此可能提升，应仅向与控制的配置的受信任的用户授予 PolicyAdministratorRole 角色[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
## <a name="examples"></a>示例  
 下面的示例将名为“Test Policy 1”的策略重命名为“Test Policy 2”。  
  
```  
EXEC msdb.dbo.sp_syspolicy_rename_policy @name = N'Test Policy 1'  
, @new_name = N'Test Policy 2';  
  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [基于策略的管理存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
