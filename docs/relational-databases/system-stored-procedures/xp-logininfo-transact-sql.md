---
title: xp_logininfo (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_logininfo_TSQL
- xp_logininfo
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logininfo
ms.assetid: ee7162b5-e11f-4a0e-a09c-1878814dbbbd
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3eb400fed1fe0cbd25ef884dc56a89fe448717fe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="xplogininfo-transact-sql"></a>xp_logininfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关 Windows 用户和 Windows 组的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_logininfo [ [ @acctname = ] 'account_name' ]   
     [ , [ @option = ] 'all' | 'members' ]   
     [ , [ @privilege = ] variable_name OUTPUT]  
```  
  
## <a name="arguments"></a>参数  
 [  **@acctname =** ] *****account_name*****  
 被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 访问权限的 Windows 用户或组的名称。 *account_name*是**sysname**，默认值为 NULL。 如果*account_name*未指定，则所有 Windows 组和 Windows 用户已被显式都授予登录权限报告。 *account_name*必须是完全限定的。 例如，“ADVWKS4\macraes”或“BUILTIN\Administrators”。  
  
 **'all'** | **成员**  
 指定是报告有关帐户的所有权限路径的信息，还是报告有关 Windows 组成员的信息。 **@option** 是**varchar(10)**，默认值为 NULL。 除非**所有**指定，则会显示仅的第一个权限路径。  
  
 [  **@privilege =** ] *variable_name*  
 返回指定 Windows 帐户的特权级别的输出参数。 *variable_name*是**varchar(10)**，默认值为不需要。 权限级别，则返回**用户**，**管理员**，或**null**。  
  
 OUTPUT  
 当指定，会将*variable_name*输出参数中。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**帐户名称**|**sysname**|完全限定的 Windows 帐户名。|  
|**类型**|**char （8)**|Windows 帐户类型。 有效值为**用户**或**组**。|  
|**特权**|**char(9)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的访问特权。 有效值为**管理员**，**用户**，或**null**。|  
|**映射的登录名**|**sysname**|为具有用户特权的用户帐户**映射登录名**显示映射的登录名[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]尝试使用在它之前添加此帐户使用的域名的映射的规则的帐户登录时。|  
|**权限路径**|**sysname**|使帐户得到访问权限的组成员身份。|  
  
## <a name="remarks"></a>注释  
 如果*account_name*指定，则**xp_logininfo**报告指定的 Windows 用户或组的最高特权级别。 如果 Windows 用户同时拥有系统管理员和域用户访问权限，则会报告为系统管理员。 如果该用户是多个具有相等特权级别的 Windows 组的成员，则只报告第一个被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 访问权限的组。  
  
 如果*account_name*是有效的 Windows 用户或组都不关联[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名，则返回空结果集。 如果*account_name*无法识别为有效的 Windows 用户或组中，返回错误消息。  
  
 如果*account_name*和**所有**是指定，返回的 Windows 用户或组的所有权限路径。 如果*account_name*属于多个组，它们都已授予访问权[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，不会返回多个行。 **管理员**之前返回特权行**用户**权限行，和中特权级别的行的顺序在返回相应[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建登录名。  
  
 如果*account_name*和**成员**是指定，则返回的下一步级别成员的组的列表。 如果*account_name*是本地组，该列表可以包括本地用户、 域用户和组。 如果*account_name*是域帐户，域用户组成的列表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须连接到域控制器，才能检索组成员身份信息。 如果该服务器无法联系域控制器，则不返回任何信息。  
  
 **xp_logininfo**仅返回从 Active Director 全局组、 不通用组的信息。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定服务器角色或中的成员身份**公共**中的固定的数据库角色**master**授予 EXECUTE 权限的数据库。  
  
## <a name="examples"></a>示例  
 下面的示例显示有关的信息`BUILTIN\Administrators`Windows 组。  
  
```  
EXEC xp_logininfo 'BUILTIN\Administrators';  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_denylogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [常规扩展存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
