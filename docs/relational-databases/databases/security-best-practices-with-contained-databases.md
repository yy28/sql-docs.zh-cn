---
title: 针对包含数据库的安全最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- contained database, threats
ms.assetid: 026ca5fc-95da-46b6-b882-fa20f765b51d
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c18410a29b500b3fd4fadfac987b1e94503ec7bb
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
# <a name="security-best-practices-with-contained-databases"></a>针对包含数据库的安全性最佳方法
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  包含的数据库面临着一些独有的威胁， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 管理员应该了解并缓解这些威胁。 大部分威胁与 **USER WITH PASSWORD** 身份验证过程相关，该过程会将身份验证的范围从 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 级别转到数据库级别。  
  
## <a name="threats-related-to-users"></a>与用户相关的威胁  
 包含的数据库中具有 **ALTER ANY USER** 权限的用户（例如 **db_owner** 和 **db_securityadmin** 固定数据库角色的成员）可以在不告知 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员或者得到其允许的情况下授予该数据库的访问权限。 授予用户对包含数据库的访问权限会增加整个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例受到攻击的可能性。 管理员应了解访问控制的这种委托，而且在为包含数据库中的用户授予 **ALTER ANY USER** 权限时要非常谨慎。 所有数据库所有者都拥有 **ALTER ANY USER** 权限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员应该定期审核包含数据库中的用户。  
  
### <a name="accessing-other-databases-using-the-guest-account"></a>使用 guest 帐户访问其他数据库  
 数据库所有者和拥有 **ALTER ANY USER** 权限的数据库用户可以创建包含数据库用户。 在连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上包含的数据库后，如果其他数据库启用了 [!INCLUDE[ssDE](../../includes/ssde-md.md)]guest **帐户，包含数据库的用户就可以访问** 上的其他数据库。  
  
### <a name="creating-a-duplicate-user-in-another-database"></a>在另一个数据库中创建重复用户  
 某些应用程序可能要求用户可以访问多个数据库。 可以通过在每个数据库中创建相同的包含的数据库来做到这点。 在创建带密码的第二个用户时，使用 SID 选项。 下面的示例在两个数据库中创建两个完全相同的用户。  
  
```  
USE DB1;  
GO  
CREATE USER Carlo WITH PASSWORD = '<strong password>';   
-- Return the SID of the user  
SELECT SID FROM sys.database_principals WHERE name = 'Carlo';  
  
-- Change to the second database  
USE DB2;  
GO  
CREATE USER Carlo WITH PASSWORD = '<same password>', SID = <SID from DB1>;  
GO  
```  
  
 若要执行跨数据库查询，必须在调用数据库上设置 **TRUSTWORTHY** 选项。 例如，如果以上定义的用户 (Carlo) 在 DB1 中，要执行 `SELECT * FROM db2.dbo.Table1;` ，则数据库 DB1 的 **TRUSTWORTHY** 设置必须为 on。 执行以下代码以将 **TRUSTWORTHY** 设置为 on。  
  
```  
ALTER DATABASE DB1 SET TRUSTWORTHY ON;  
```  
  
### <a name="creating-a-user-that-duplicates-a-login"></a>创建复制登录名的用户  
 如果创建了一个有密码的包含数据库用户，所使用的名称与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名相同，而且在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名进行连接时将包含的数据库指定为初始目录，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名将无法连接。 该连接将被判定为包含数据库上的具有密码主体的包含数据库用户发起，而不是基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的用户发起。 这可能导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名遭遇到拒绝服务。  
  
-   最佳做法是， **sysadmin** 固定服务器角色的成员应该始终考虑在连接时不使用初始目录选项。 这样会使登录名连接到 master 数据库，并可避免数据库所有者滥用登录名的可能性。 然后，管理员可以通过使用 USE\<database> 语句更改为包含的数据库。 您也可以将登录操作的默认数据库设置为包含的数据库，这样会先登录到 **master**数据库，然后再转而登录到包含的数据库。  
  
-   最佳做法是，创建有密码的包含数据库用户时，其名称不得与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名相同。  
  
-   如果存在重复的登录名，请连接到 **master** 数据库，但不要指定初始目录，然后执行 **USE** 命令转到包含的数据库。  
  
-   存在包含的数据库时，非包含数据库的用户应连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，但不要使用初始目录，或者将非包含数据库的数据库名称指定为初始目录。 这样就避免了连接到包含的数据库而导致 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 管理员的直接控制减弱。  
  
### <a name="increasing-access-by-changing-the-containment-status-of-a-database"></a>通过更改数据库的包含状态来增加访问  
 具有 **ALTER ANY DATABASE** 权限的登录名（如 **dbcreator** 固定服务器角色的成员）以及非包含数据库中具有 **CONTROL DATABASE** 权限的用户（如 **db_owner** 固定数据库角色的成员）都可以更改数据库的包含设置。 如果数据库的包含设置从 **NONE** 更改为 **PARTIAL** 或 **FULL**，则可以通过创建有密码的包含数据库用户来授予用户访问权限。 这样就可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员不知情或不允许的情况下提供访问。 若要防止将任何数据库更改为包含的数据库，请将 [!INCLUDE[ssDE](../../includes/ssde-md.md)] **contained database authentication** 选项设置为 0。 若要阻止有密码的包含数据库用户连接到选定的包含的数据库，请使用登录触发器取消有密码的包含数据库用户进行的登录尝试。  
  
### <a name="attaching-a-contained-database"></a>附加包含的数据库  
 通过附加包含的数据库，管理员会向用户授予针对 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的不必要的访问权限。 担心这种风险的管理员可以使数据库以 **RESTRICTED_USER** 模式联机，这样会阻止对使用密码的包含数据库用户进行身份验证。 只有通过登录授权的主体才能够访问 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
 用户是使用在其创建时有效的密码要求创建的，并且在附加数据库时不重新检查密码。 通过将一个允许使用弱密码的包含数据库附加到一个具有更严格密码策略的系统上，管理员可能允许在附加 [!INCLUDE[ssDE](../../includes/ssde-md.md)]上使用不满足当前密码策略的密码。 通过要求对附加数据库重置所有密码，管理员可以避免保留弱密码。  
  
### <a name="password-policies"></a>密码策略  
 可以要求数据库中的密码是强密码，但不能通过可靠的密码策略来保护这些密码。 尽可能地使用 Windows 身份验证，以便利用 Windows 提供的更加广泛的密码策略。  
  
### <a name="kerberos-authentication"></a>Kerberos 身份验证  
 有密码的包含数据库用户不能使用 Kerberos 身份验证。 尽可能使用 Windows 身份验证，以便利用 Kerberos 等 Windows 功能。  
  
### <a name="offline-dictionary-attack"></a>脱机字典攻击  
 有密码的包含数据库用户的密码哈希值存储在包含的数据库中。 任何具有数据库文件访问权限的人都可以对未审核系统上有密码的包含数据库用户进行字典攻击。 若要减轻这种威胁，请限制对数据库文件的访问，或者只允许使用 Windows 身份验证连接到包含的数据库。  
  
## <a name="escaping-a-contained-database"></a>避免使用包含的数据库  
 如果某个数据库为部分包含，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员应该定期审核包含的数据库中用户和模块的能力。  
  
## <a name="denial-of-service-through-autoclose"></a>通过 AUTO_CLOSE 拒绝服务  
 不要将包含的数据库配置为自动关闭。 如果关闭，打开数据库对用户进行身份验证会消耗额外的资源，并可能导致拒绝服务攻击。  
  
## <a name="see-also"></a>另请参阅  
 [包含的数据库](../../relational-databases/databases/contained-databases.md)   
 [迁移到部分包含的数据库](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)  
  
  
