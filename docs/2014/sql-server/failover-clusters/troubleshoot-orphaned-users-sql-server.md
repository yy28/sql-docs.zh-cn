---
title: 孤立用户故障排除 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- orphaned users [SQL Server]
- logins [SQL Server], orphaned users
- troubleshooting [SQL Server], user accounts
- user accounts [SQL Server], orphaned users
- failover [SQL Server], managing metadata
- database mirroring [SQL Server], metadata
- users [SQL Server], orphaned
ms.assetid: 11eefa97-a31f-4359-ba5b-e92328224133
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38a33b34b64cf285e94f66c547b2309b8daf1ae8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63035648"
---
# <a name="troubleshoot-orphaned-users-sql-server"></a>孤立用户故障排除 (SQL Server)
  要登录到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，主体必须有一个有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 在身份验证过程中会使用此登录名，以验证是否允许主体连接到该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 服务器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上的登录名**server_principals**在 syslogins 目录视图和**sys.syslogins**兼容性视图中可见。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名使用映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的数据库用户访问各个数据库。 此规则有两种例外情况：  
  
-   guest 帐户。  
  
     这个帐户在数据库中启用后，能够使未映射到数据库用户的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名作为 guest 用户进入数据库。  
  
-   Microsoft Windows 组成员身份。  
  
     如果某 Windows 用户是 Windows 组的成员，并且此组也是数据库中的用户，则基于该 Windows 用户创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名可以进入数据库。  
  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名与数据库用户的映射关系的信息存储在数据库中。 其中包括数据库用户的名称以及对应 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的 SID。 该数据库用户的权限用于在数据库中进行授权。  
  
 在服务器实例上未定义或错误定义了其相应 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的数据库用户无法登录到实例。 这样的用户被称为此服务器实例上的数据库的“孤立用户” ** 。 如果删除了对应的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，则数据库用户可能会变为孤立用户。 另外，在数据库还原或附加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其他实例之后，数据库用户也可能变为孤立用户。 如果未在新服务器实例中提供数据库用户映射到的 SID，则该用户可能变为孤立用户。  
  
> [!NOTE]  
>  除非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在数据库中启用了**guest** ，否则登录名无法访问其缺少相应的数据库用户的数据库。 有关创建数据库用户帐户的信息，请参阅[CREATE user &#40;transact-sql&#41;](/sql/t-sql/statements/create-user-transact-sql)。  
  
## <a name="to-detect-orphaned-users"></a>检测孤立用户  
 若要检测孤立用户，请执行下列 Transact-SQL 语句：  
  
```  
USE <database_name>;  
GO;   
sp_change_users_login @Action='Report';  
GO;  
```  
  
 输出中列出了当前数据库中未链接到任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的用户以及对应的安全标识符 (SID)。 有关详细信息，请参阅[&#40;transact-sql&#41;sp_change_users_login ](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)。  
  
> [!NOTE]  
>  **sp_change_users_login**不能与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过 Windows 创建的登录名一起使用。  
  
## <a name="to-resolve-an-orphaned-user"></a>解决孤立用户问题  
 若要解决孤立用户问题，请执行以下过程：  
  
1.  以下命令将 *<>login_name*指定的服务器登录帐户与 *<database_user>* 指定的数据库用户重新链接。  
  
    ```  
    USE <database_name>;  
    GO  
    sp_change_users_login @Action='update_one', @UserNamePattern='<database_user>', @LoginName='<login_name>';  
    GO  
  
    ```  
  
     有关详细信息，请参阅[&#40;transact-sql&#41;sp_change_users_login ](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)。  
  
2.  运行上述步骤中的代码后，该用户就可以访问数据库了。 然后，用户可以使用**sp_password**存储过程来更改 *<login_name>* 登录帐户的密码，如下所示：  
  
    ```  
    USE master   
    GO  
    sp_password @old=NULL, @new='password', @loginame='<login_name>';  
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  只有具有 ALTER ANY LOGIN 权限的登录帐户才能更改其他用户的登录密码。 但是，只有 **sysadmin** 角色的成员才能修改 **sysadmin** 角色成员的密码。  
  
    > [!NOTE]  
    >  不能将**sp_password**用于[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 通过 Windows 网络帐户连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的用户是由 Windows 进行身份验证的，因此其密码只能在 Windows 中更改。  
  
     有关详细信息，请参阅[&#40;transact-sql&#41;sp_password ](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE USER &#40;Transact-sql&#41;](/sql/t-sql/statements/create-user-transact-sql)   
 [CREATE LOGIN &#40;Transact-sql&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [sp_change_users_login &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)   
 [sp_addlogin &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)   
 [sp_grantlogin &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-grantlogin-transact-sql)   
 [sp_password &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)   
 [sysusers &#40;Transact-sql&#41;](/sql/relational-databases/system-compatibility-views/sys-sysusers-transact-sql)   
 [syslogins &#40;Transact-sql&#41;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)  
  
  
