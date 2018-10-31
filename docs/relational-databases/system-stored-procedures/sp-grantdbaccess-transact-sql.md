---
title: sp_grantdbaccess (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grantdbaccess
- sp_grantdbaccess_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantdbaccess
ms.assetid: 3eb09513-03f1-42f8-9917-3a1f3a579bec
ms.author: vanto
manager: craigg
ms.openlocfilehash: be0252386717bb2e9cffcef45918a0dd85d06b41
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652929"
---
# <a name="spgrantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将数据库用户添加到当前数据库。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE USER](../../t-sql/statements/create-user-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@loginame =** ]  **'* * * 登录* **'** 是 Windows 组，Windows 登录名的名称或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名映射到新数据库用户。Windows 组和 Windows 登录名的名称必须用在窗体中的 Windows 域名限定*域*\\*登录*; 例如， **LONDON\Joeb**。 登录名不能已映射到数据库中的用户。 *登录名*是**sysname**，无默认值。  
  
 [  **@name_in_db=**] **'***name_in_db***'** [**输出**]  
 新数据库用户的名称。 *name_in_db*是输出变量，其数据类型为**sysname**，和默认值为 NULL。 如果未指定，否则*登录名*使用。 如果指定为 OUTPUT 变量，其值为 NULL， **@name_in_db**设置为*登录*。 *name_in_db*必须已存在当前数据库中。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_grantdbaccess**调用 CREATE USER，后者支持其他选项。 有关创建数据库用户的信息，请参阅[CREATE USER &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)。 若要从数据库中删除的数据库用户，请使用[DROP USER](../../t-sql/statements/drop-user-transact-sql.md)。  
  
 **sp_grantdbaccess**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**db_owner**固定的数据库角色或**db_accessadmin**固定的数据库角色。  
  
## <a name="examples"></a>示例  
 下面的示例使用`CREATE USER`若要添加的 Windows 登录名的数据库用户`Edmonds\LolanSo`到当前数据库。 新用户名为 `Lolan`。 这是创建数据库用户的首选方法。  
  
```  
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER (Transact-SQL)](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER (Transact-SQL)](../../t-sql/statements/drop-user-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
