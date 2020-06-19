---
title: contained database authentication 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- contained_database_authentication_TSQL
- contained database authentication
helpviewer_keywords:
- contained database, enabling
- contained database authentication option
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cf5bf07c8b0913ff81f31ff0ca64a18eee0f2ac2
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935438"
---
# <a name="contained-database-authentication-server-configuration-option"></a>contained database authentication 服务器配置选项
  使用 **contained database authentication** 选项对 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例启用包含的数据库。  
  
 此服务器选项允许您控制 **contained database authentication**。  
  
-   如果 **contained database authentication** 对实例关闭 (0)，则无法创建包含的数据库或将其附加到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
-   如果 **contained database authentication** 对实例打开 (1)，则可以创建包含的数据库或将其附加到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
 包含的数据库包括定义数据库所需的所有数据库设置和元数据，它与安装数据库的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例没有配置依赖关系。 用户可以连接到数据库而无需在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 级别对登录名进行身份验证。 将数据库与数据库引擎隔离可以轻松地将数据库移到另一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 在数据库中包括所有数据库设置有利于数据库所有者管理数据库的所有配置设置。 有关包含的数据库的详细信息，请参阅 [Contained Databases](../../relational-databases/databases/contained-databases.md)。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例具有包含数据库，则可以使用 **RECONFIGURE WITH OVERRIDE** 语句将 **contained database authentication** 设置为 0。 将 **contained database authentication** 设置为 0 将禁用包含数据库的包含数据库身份验证。  
  
> [!IMPORTANT]  
>  启用包含的数据库时，具有 ALTER ANY USER 权限的数据库用户（如 db_owner 和 db_accessadmin 数据库角色的成员）可以授予对数据库的访问权限，并由此授予对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的访问权限。 这意味着控制对服务器的访问权限不再限于 sysadmin 和 securityadmin 固定服务器角色的成员以及具有服务器级别 CONTROL SERVER 和 ALTER ANY LOGIN 权限的登录。 在允许包含的数据库之前，应了解与包含的数据库相关的风险。 有关详细信息，请参阅 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)。  
  
## <a name="examples"></a>示例  
 下面的示例对 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例启用包含的数据库。  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)  
  
  
