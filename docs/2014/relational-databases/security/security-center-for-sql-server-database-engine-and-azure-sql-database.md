---
title: SQL Server 数据库引擎和 Azure SQL Database 的安全中心 | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- SQL Server, security
- security [SQL Server]
- database security [SQL Server]
- databases [SQL Server], security
ms.assetid: dfb39d16-722a-4734-94bb-98e61e014ee7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 1fffca14e9c30c5fd01cff88b7bb90608eb9d30d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63185340"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server 数据库引擎和 Azure SQL Database 的安全中心
  本页提供的链接可帮助你找到有关 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]和 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]中的安全性和保护的必要信息。  
  
> [!NOTE]  
>  [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 的功能将继续改进。 有关 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]的最新信息，请参阅本主题的最新版本。  
  
|身份验证：你是谁？|授权：您可以做什么？|加密：存储机密数据|连接安全：限制和保护|审核：记录访问|  
|----------------------------------|-------------------------------------|-------------------------------------|---------------------------------------------------|--------------------------------|  
|**谁进行身份验证？**<br /><br /> [![安全中心映射 Windows 身份验证](../../database-engine/media/security-center-map-windows-authenticaion.png "安全中心映射 Windows 身份验证")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> <br /><br /> [![安全中心映射 SQL Server 身份验证](../../database-engine/media/security-center-map-sql-authenticaion.png "安全中心映射 SQL Server 身份验证")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> **在哪里进行身份验证？**<br /><br /> [![安全中心映射登录名和用户](../../database-engine/media/security-center-map-logins-users.png "安全中心映射登录名和用户")](https://msdn.microsoft.com/library/aa337562.aspx)<br /><br /> <br /><br /> [![安全中心映射包含的数据库用户](../../database-engine/media/security-center-map-contained-users.png "安全中心映射包含的数据库用户")](https://msdn.microsoft.com/library/ff929188.aspx)<br /><br /> **使用其他标识**<br /><br /> [![安全中心映射凭据](../../database-engine/media/security-center-map-credentials.png "安全中心映射凭据")](https://msdn.microsoft.com/library/ms161950.aspx)<br /><br /> [![安全中心映射作为登录名执行](../../database-engine/media/security-center-map-exec-as-login.png "安全中心映射作为登录名执行")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> [![安全中心映射作为用户执行](../../database-engine/media/security-center-map-exec-as-user.png "安全中心映射作为用户执行")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")|**授予、撤消和拒绝权限**<br /><br /> [![安全中心映射安全对象类](../../database-engine/media/security-center-map-securable-classes.png "安全中心映射安全对象类")](https://msdn.microsoft.com/library/ms190401.aspx)<br /><br /> [![安全中心映射服务器权限](../../database-engine/media/security-center-map-srv-perms.png "安全中心映射服务器权限")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> [![安全中心映射数据库权限](../../database-engine/media/security-center-map-db-perms.png "安全中心映射数据库权限")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> **按角色分类的安全性**<br /><br /> [![安全中心映射服务器角色](../../database-engine/media/security-center-map-srv-roles.png "安全中心映射服务器角色")](https://msdn.microsoft.com/library/ms188659.aspx)<br /><br /> [![安全中心映射数据库角色](../../database-engine/media/security-center-map-db-roles.png "安全中心映射数据库角色")](https://msdn.microsoft.com/library/ms189121.aspx)<br /><br /> `Restricting Data Access to Selected Data Elements`<br /><br /> [![安全中心映射视图和过程](../../database-engine/media/security-center-map-view-procs.png "安全中心映射视图和过程")](https://msdn.microsoft.com/library/ms175503.aspx)<br /><br /> [![安全中心映射行级安全性](../../database-engine/media/security-center-map-row-level-sec.png "安全中心映射行级安全性")](https://msdn.microsoft.com/library/dn765131.aspx)<br /><br /> [![安全中心映射动态数据屏蔽](../../database-engine/media/security-center-map-data-masking.png "安全中心映射动态数据屏蔽")](http://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [![安全中心映射签名的对象](../../database-engine/media/security-center-map-signed-objects.png "安全中心映射签名的对象")](https://msdn.microsoft.com/library/ms181700.aspx)<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")|**加密文件**<br /><br /> [![安全中心映射 BitLocker](../../database-engine/media/security-center-map-bitlocker.png "安全中心映射 BitLocker")](https://support.microsoft.com/en-us/kb/2855131)<br /><br /> [![安全中心映射 NTFS 加密](../../database-engine/media/security-center-map-ntfs-encryp.png "安全中心映射 NTFS 加密")](https://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [![安全中心映射 TDE](../../database-engine/media/security-center-map-tde.png "安全中心映射 TDE")](https://msdn.microsoft.com/library/bb934049.aspx)<br /><br /> [![安全中心映射备份加密](../../database-engine/media/security-center-map-backup-encryp.png "安全中心映射备份加密")](https://msdn.microsoft.com/library/dn449489.aspx)<br /><br /> **加密源**<br /><br /> [![安全中心映射 EKM](../../database-engine/media/security-center-map-ekm.png "安全中心映射 EKM")](https://msdn.microsoft.com/library/bb895340.aspx)<br /><br /> [![安全中心映射 Azure 密钥保管库](../../database-engine/media/security-center-map-key-vault.png "安全中心映射 Azure 密钥保管库")](http://azure.microsoft.com/documentation/articles/key-vault-get-started/)<br /><br /> **列、 数据和密钥加密**<br /><br /> [![使用证书进行安全中心映射加密](../../database-engine/media/security-center-map-cert.png "证书进行安全中心映射加密")](https://msdn.microsoft.com/library/ms188061.aspx)<br /><br /> [![对称密钥进行安全中心映射加密](../../database-engine/media/security-center-map-sym-key.png "对称密钥进行安全中心映射加密")](https://msdn.microsoft.com/library/ms174361.aspx)<br /><br /> [![非对称密钥进行安全中心映射加密](../../database-engine/media/security-center-map-asym-key.png "非对称密钥进行安全中心映射加密")](https://msdn.microsoft.com/library/ms186950.aspx)<br /><br /> [![使用密码进行安全中心映射加密](../../database-engine/media/security-center-map-passphrase.png "通行短语进行安全中心映射加密")](https://msdn.microsoft.com/library/ms190357.aspx)|**防火墙保护**<br /><br /> [![安全中心映射 Windows 防火墙](../../database-engine/media/security-center-map-windows-firewall.png "安全中心映射 Windows 防火墙")](https://msdn.microsoft.com/library/ms175043.aspx)<br /><br /> [![安全中心映射服务防火墙](../../database-engine/media/security-center-map-service-firewall.png "安全中心映射服务防火墙")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> [![安全中心映射数据库防火墙](../../database-engine/media/security-center-map-db-firewall.png "安全中心映射数据库防火墙")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> **在传输过程中加密数据**<br /><br /> [![安全中心映射强制 SSL](../../database-engine/media/security-center-map-forced-ssl.png "安全中心映射强制 SSL")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> [![安全中心映射可选的 SSL](../../database-engine/media/security-center-map-opt-ssl.png "安全中心映射可选的 SSL")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")|**自动审核**<br /><br /> [![安全中心映射 SQL Server 审核](../../database-engine/media/security-center-map-sql-audit.png "安全中心映射 SQL Server 审核")](https://msdn.microsoft.com/library/cc280386.aspx)<br /><br /> [![安全中心映射 SQL 数据库审核](../../database-engine/media/security-center-map-sqldb-audit.png "安全中心映射 SQL 数据库审核")](http://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> **自定义审核**<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> [![安全中心映射触发器](../../database-engine/media/security-center-map-triggers.png "安全中心映射触发器")](https://msdn.microsoft.com/library/ms175941.aspx)<br /><br /> **遵从性**<br /><br /> [![SecCtrCompliance](../../database-engine/media/secctrcompliance.png "SecCtrCompliance")](http://azure.microsoft.com/support/trust-center/services/)<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![占位符](../../database-engine/media/security-center-map-blankplaceholder.png "占位符")<br /><br /> ![安全中心图例](../../database-engine/media/security-center-map-legend.png "安全中心图例")|  
  
## <a name="links-to-specific-related-topics"></a>指向特定相关主题的链接  
 ![小文件文件夹图标](../../integration-services/media/filefolder-small.gif "小文件文件夹图标")**身份验证：你是谁？**  
 **谁进行身份验证？(Windows 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
  
-   [选择身份验证模式](choose-an-authentication-mode.md)  
  
 **在 master 数据库进行身份验证** （登录名和数据库用户）  
  
-   [创建 SQL Server 登录名](authentication-access/create-a-login.md)  
  
-   [在 Azure SQL 数据库中管理数据库和登录名](https://msdn.microsoft.com/library/ee336235.aspx)  
  
-   [创建数据库用户](authentication-access/create-a-database-user.md)  
  
 **在用户数据库进行身份验证**  
  
-   [包含的数据库用户 - 使你的数据库可移植](contained-database-users-making-your-database-portable.md)  
  
 **使用其他标识**  
  
-   [凭据（数据库引擎）](authentication-access/credentials-database-engine.md)  
  
-   [作为另一个登录名执行](/sql/t-sql/statements/execute-as-transact-sql)  
  
-   [作为另一个数据库用户执行](/sql/t-sql/statements/execute-as-transact-sql)  
  
 ![小文件文件夹图标](../../integration-services/media/filefolder-small.gif "小文件文件夹图标")**加密：存储机密数据**  
 **加密文件**  
  
-   [BitLocker（驱动器级别）](https://support.microsoft.com/kb/2855131)  
  
-   [NTFS 加密（文件夹级别）](https://msdn.microsoft.com/library/dd163562.aspx)  
  
-   [透明数据加密（文件级别）](encryption/transparent-data-encryption.md)  
  
-   [备份加密（文件级别）](../backup-restore/backup-encryption.md)  
  
 **加密源**  
  
-   [可扩展密钥管理模块](encryption/extensible-key-management-ekm.md)  
  
-   [Azure 密钥保管库中存储的密钥](encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 **列、 数据和密钥加密**  
  
-   [使用证书进行加密](/sql/t-sql/functions/encryptbycert-transact-sql)  
  
-   [使用非对称密钥进行加密](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
  
-   [使用对称密钥进行加密](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [使用密码进行加密](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
  
 ![小文件文件夹图标](../../integration-services/media/filefolder-small.gif "小文件文件夹图标")**授权：您可以做什么？**  
 **授予、撤消和拒绝权限**  
  
-   [权限层次结构（数据库引擎）](permissions-hierarchy-database-engine.md)  
  
-   [权限](permissions-database-engine.md)  
  
-   [安全对象](securables.md)  
  
 **按角色分类的安全性**  
  
-   [服务器级别角色](authentication-access/server-level-roles.md)  
  
-   [数据库级别的角色](authentication-access/database-level-roles.md)  
  
 `Restricting Data Access to Selected Data Elements`  
  
-   使用 [视图](../views/views.md) 和 [过程](../stored-procedures/stored-procedures-database-engine.md)限制数据访问  
  
-   [行级安全性](https://msdn.microsoft.com/library/azure/dn765131.aspx)  
  
-   [动态数据屏蔽](http://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)  
  
-   [签名的对象](/sql/t-sql/statements/add-signature-transact-sql)  
  
 ![小文件文件夹图标](../../integration-services/media/filefolder-small.gif "小文件文件夹图标")**连接安全：限制和保护**  
 **防火墙保护**  
  
-   [为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Azure SQL 数据库防火墙设置](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
-   [Azure 服务防火墙设置](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
 **在传输过程中加密数据**  
  
-   [用于数据库引擎的安全套接字层](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
-   [用于 SQL 数据库的安全套接字层](https://msdn.microsoft.com/library/azure/ff394108.aspx)  
  
 ![小文件文件夹图标](../../integration-services/media/filefolder-small.gif "小文件文件夹图标")**审核：记录访问**  
 **自动审核**  
  
-   [SQL Server Audit（数据库引擎）](auditing/sql-server-audit-database-engine.md)  
  
-   [SQL 数据库审核](http://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)  
  
 **自定义审核实现**  
  
-   创建 [DDL Triggers](../triggers/ddl-triggers.md) 和 [DML Triggers](../triggers/dml-triggers.md)  
  
 ![小文件文件夹图标](../../integration-services/media/filefolder-small.gif "小文件文件夹图标")**法规遵从性**  
 **SQL Server**  
  
-   [通用准则](https://go.microsoft.com/fwlink/?LinkId=616319)  
  
 **SQL 数据库**  
  
-   [Microsoft Azure 信任中心：按功能的符合性](http://azure.microsoft.com/support/trust-center/services/)  
  
## <a name="see-also"></a>请参阅  
 [保护 SQL Server](securing-sql-server.md)   
 [主体（数据库引擎）](authentication-access/principals-database-engine.md)   
 [SQL Server 证书和非对称密钥](sql-server-certificates-and-asymmetric-keys.md)   
 [SQL Server 加密](encryption/sql-server-encryption.md)   
 [外围应用配置器](surface-area-configuration.md)   
 [强密码](strong-passwords.md)   
 [TRUSTWORTHY 数据库属性](trustworthy-database-property.md)   
 [数据库引擎功能和任务](../../database-engine/database-engine-features-and-tasks.md)  
  
  
