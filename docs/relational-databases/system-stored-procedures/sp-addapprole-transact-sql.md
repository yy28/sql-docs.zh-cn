---
title: sp_addapprole (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addapprole_TSQL
- sp_addapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addapprole
ms.assetid: 24200295-9a54-4cab-9922-fb2e88632721
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 04163593c48a22bebdd933881b165af3418e0dfa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690685"
---
# <a name="spaddapprole-transact-sql"></a>sp_addapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  向当前数据库中添加应用程序角色。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addapprole [ @rolename = ] 'role' , [ @password = ] 'password'  
```  
  
## <a name="arguments"></a>参数  
 [  **@rolename =** ] **'***角色*****  
 新应用程序角色的名称。 *角色*是**sysname**，无默认值。 *角色*必须是有效标识符，并且不能存在于当前数据库中。  
  
 应用程序角色名称可以包含 1 到 128 个字符，包括字母、符号及数字。 角色名称不能包含反斜杠 (\\)，也不为 NULL 或空字符串 （"）。  
  
 [  **@password =** ] **'***密码*****  
 激活应用程序角色所需的密码。 *密码*是**sysname**，无默认值。 *密码*不能为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的更早版本中，用户（和角色）与架构并非完全不同。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，架构与角色已完全不同。 此新体系结构反映在 CREATE APPLICATION ROLE 的行为中。 此语句取代了**sp_addapprole**。  
  
 若要保持与早期版本的向后兼容性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， **sp_addapprole**将执行以下操作：  
  
-   如果尚未存在与应用程序角色同名的架构，则创建这样的架构。 新的架构将由应用程序角色拥有，并且它将是该应用程序角色的默认架构。  
  
-   如果与应用程序角色同名的架构已经存在，则该过程将失败。  
  
-   不检查密码复杂性**sp_addapprole**。 但 CREATE APPLICATION ROLE 会检查密码复杂性。  
  
 将参数*密码*作为单向哈希存储。  
  
 **Sp_addapprole**不能从用户定义的事务中执行存储的过程。  
  
> [!IMPORTANT]  
>  Microsoft ODBC**加密**选项不受**SqlClient**。 如果您可以，请在运行时提示用户输入应用程序角色凭据。 不要将凭据存储在一个文件中。 如果必须使凭据持久化，请使用 CryptoAPI 函数将它们加密。  
  
## <a name="permissions"></a>Permissions  
 需要对数据库具有 ALTER ANY APPLICATION ROLE 权限。 如果尚未存在具有与新角色相同名称和所有者的架构，则还需要拥有对该数据库的 CREATE SCHEMA 权限。  
  
## <a name="examples"></a>示例  
 下面的示例添加新的应用程序角色`SalesApp`使用的密码`x97898jLJfcooFUYLKm387gf3`到当前数据库。  
  
```  
EXEC sp_addapprole 'SalesApp', 'x97898jLJfcooFUYLKm387gf3' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [CREATE APPLICATION ROLE (Transact-SQL)](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
