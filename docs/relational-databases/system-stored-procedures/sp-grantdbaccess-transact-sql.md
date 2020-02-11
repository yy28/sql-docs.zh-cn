---
title: sp_grantdbaccess （Transact-sql） |Microsoft Docs
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
author: VanMSFT
ms.openlocfilehash: 3b88badb8b1852617d9edd8acd31f2c19258cca7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "72304862"
---
# <a name="sp_grantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将数据库用户添加到当前数据库。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]请改用[CREATE USER](../../t-sql/statements/create-user-transact-sql.md) 。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>参数  
`[ @loginame = ] 'login_ '`要映射到新数据库用户的 Windows 组、Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名或登录名。 Windows 组和 windows 登录名的名称必须以*域*\\*登录*名的形式使用 windows 域名进行限定。例如， **LONDON\Joeb**。 登录名不能已映射到数据库中的用户。 *login*是**sysname**，无默认值。  
  
``[ @name_in_db = ] 'name_in_db' [ OUTPUT]``新数据库用户的名称。 *name_in_db*是数据类型为**sysname**的输出变量，默认值为 NULL。 如果未指定，则使用*登录名*。 如果指定为值为 NULL 的输出变量， ** \@则 name_in_db**设置为*login*。 当前数据库中不能存在*name_in_db* 。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_grantdbaccess**调用 CREATE USER，后者支持其他选项。 有关创建数据库用户的信息，请参阅[CREATE USER &#40;transact-sql&#41;](../../t-sql/statements/create-user-transact-sql.md)。 若要从数据库中删除数据库用户，请使用[DROP user](../../t-sql/statements/drop-user-transact-sql.md)。  
  
 不能在用户定义的事务中执行**sp_grantdbaccess** 。  
  
## <a name="permissions"></a>权限  
 需要**db_owner**固定数据库角色的成员身份或**db_accessadmin**固定数据库角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例使用`CREATE USER`将 Windows 登录名`Edmonds\LolanSo`的数据库用户添加到当前数据库。 新用户名为 `Lolan`。 这是创建数据库用户的首选方法。  
  
```sql
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER &#40;Transact-sql&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-sql&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
