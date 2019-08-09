---
title: sp_certify_removable (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_certify_removable_TSQL
- sp_certify_removable
dev_langs:
- TSQL
helpviewer_keywords:
- sp_certify_removable
ms.assetid: ca12767f-0ae5-4652-b523-c23473f100a1
author: stevestein
ms.author: sstein
ms.openlocfilehash: c39665f54a915282a6c59fe7d57b24d0cde0a5e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045936"
---
# <a name="sp_certify_removable-transact-sql"></a>sp_certify_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  验证是否正确配置数据库以便在可移动介质上分发，并向用户报告所有问题。  
  
> **重要说明!!** [!INCLUDE[ssNoteDepFutureAvoid](../../t-sql/statements/create-database-sql-server-transact-sql.md) instead.  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_certify_removable [ @dbname= ] 'dbname'  
     [ , [ @autofix = ] 'auto' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @dbname = ] 'dbname'` 指定要验证的数据库。 *dbname*是**sysname**。  
  
`[ @autofix = ] 'auto'` 对系统管理员授予数据库及所有数据库对象的所有权，并除去任何用户创建的数据库用户及非默认的权限。 *自动*是**nvarchar(4)** ，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 如果正确配置数据库，则**sp_certify_removable**执行以下：  
  
-   将数据库设置为脱机，以便复制文件。  
  
-   更新所有表的统计信息，并报告任何所有权问题或用户问题。  
  
-   将数据文件组标记为只读，以便将这些文件复制到只读介质中。  
  
 系统管理员必须是数据库和所有数据库对象的所有者。 系统管理员是存在于正在运行的所有服务器的已知的用户[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以及可以预期存在更高版本分发和安装数据库时。  
  
 如果在运行**sp_certify_removable**而无需**自动**值并返回有关以下条件的任何信息：  
  
-   系统管理员不是数据库所有者。  
  
-   存在用户创建的任何用户。  
  
-   系统管理员并非拥有数据库中的所有对象。  
  
-   已授予非默认权限。  
  
 可以使用下列方法更正这些情况：  
  
-   使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]工具和过程，以及然后运行**sp_certify_removable**试。  
  
-   只需运行**sp_certify_removable**与**自动**值。  
  
 注意，该存储过程只检查用户和用户权限。 可以向数据库添加组并且对这些组授予权限。 有关详细信息，请参阅 [GRANT (Transact-SQL)](../../t-sql/statements/grant-transact-sql.md)的信息。  
  
## <a name="permissions"></a>权限  
 执行权限仅限于的成员**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 下面的示例验证 `inventory` 数据库已准备好删除。  
  
```  
EXEC sp_certify_removable inventory, AUTO;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_create_removable &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-removable-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
