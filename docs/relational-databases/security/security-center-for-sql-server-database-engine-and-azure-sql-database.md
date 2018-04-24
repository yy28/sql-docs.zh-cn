---
title: SQL Server 数据库引擎和 Azure SQL Database 的安全中心 | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: ''
ms.component: security
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- SQL Server, security
- security [SQL Server]
- database security [SQL Server]
- databases [SQL Server], security
ms.assetid: dfb39d16-722a-4734-94bb-98e61e014ee7
caps.latest.revision: 55
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 09c051ece663a046a9286b27ddfd5356ab534e7a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server 数据库引擎和 Azure SQL Database 的安全中心
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本页提供的链接可帮助你找到有关 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]中的安全性和保护的必要信息。  
  
 **图例**  
  
 ![security-center-legend](../../relational-databases/performance/media/security-center-legend.PNG "security-center-legend")  
  
##  <a name="Who"></a> 身份验证：你是谁？  
  
|||  
|-|-|  
|**谁进行身份验证？**<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") Windows 身份验证<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") Azure Active Directory|谁进行身份验证？ （Windows 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）<br /><br /> [选择身份验证模式](../../relational-databases/security/choose-an-authentication-mode.md)<br /><br /> [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)|  
|**在哪里进行身份验证？**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 在 master 数据库：登录名和 DB 用户<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 在用户数据库：包含的 DB 用户|在 master 数据库进行身份验证（登录名和数据库用户）<br /><br /> [创建 SQL Server 登录名](../../relational-databases/security/authentication-access/create-a-login.md)<br /><br /> [在 Azure SQL 数据库中管理数据库和登录名](http://msdn.microsoft.com/library/ee336235.aspx)<br /><br /> [创建数据库用户](../../relational-databases/security/authentication-access/create-a-database-user.md)<br /><br /> <br /><br /> 在用户数据库进行身份验证<br /><br /> [包含的数据库用户 - 使你的数据库可移植](../../relational-databases/security/contained-database-users-making-your-database-portable.md)|  
|**使用其他标识**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 凭据<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") 以另一个登录名的身份执行<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 以另一个数据库用户的身份执行|[凭据（数据库引擎）](../../relational-databases/security/authentication-access/credentials-database-engine.md)<br /><br /> [作为另一个登录名执行](../../t-sql/statements/execute-as-transact-sql.md)<br /><br /> [作为另一个数据库用户执行](../../t-sql/statements/execute-as-transact-sql.md)|  
  
##  <a name="What"></a> 授权：你可以做什么？  
  
|||  
|-|-|  
|**授予、撤消和拒绝权限**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 安全对象类<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") 具体服务器权限<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 具体数据库权限|[权限层次结构（数据库引擎）](../../relational-databases/security/permissions-hierarchy-database-engine.md)<br /><br /> [权限](../../relational-databases/security/permissions-database-engine.md)<br /><br /> [安全对象](../../relational-databases/security/securables.md)<br /><br /> [数据库引擎权限入门](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)|  
|**按角色分类的安全性**<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") 服务器级别角色<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 数据库级别角色|[服务器级角色](../../relational-databases/security/authentication-access/server-level-roles.md)<br /><br /> [数据库级别的角色](../../relational-databases/security/authentication-access/database-level-roles.md)|  
|**限制对所选数据元素的数据访问**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 使用视图/过程限制数据访问<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 行级别安全性<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 动态数据掩码<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 已签名的对象|使用 [视图](../../relational-databases/views/views.md) 和 [过程](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)限制数据访问<br /><br /> [行级别安全性 (SQL Server)](../../relational-databases/security/row-level-security.md)<br /><br /> [行级别安全性 (Azure SQL Database)](http://msdn.microsoft.com/library/azure/dn765131.aspx)<br /><br /> [动态数据掩码 (SQL Server)](../../relational-databases/security/dynamic-data-masking.md)<br /><br /> [动态数据掩码 (Azure SQL Database)](http://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [签名的对象](../../t-sql/statements/add-signature-transact-sql.md)|  
  
##  <a name="Encrypt"></a> 加密：存储机密数据  
  
|||  
|-|-|  
|**加密文件**<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") BitLocker 加密（驱动器级别）<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") NTFS 加密（文件夹级别）<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 透明数据加密（文件级别）<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 备份加密（文件级别）|[BitLocker（驱动器级别）](http://support.microsoft.com/kb/2855131)<br /><br /> [NTFS 加密（文件夹级别）](http://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [透明数据加密（文件级别）](../../relational-databases/security/encryption/transparent-data-encryption.md)<br /><br /> [备份加密（文件级别）](../../relational-databases/backup-restore/backup-encryption.md)|  
|**加密源**<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") 可扩展密钥管理模块<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") Azure Key Vault 中存储的密钥<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") Always Encrypted|[可扩展密钥管理模块](../../relational-databases/security/encryption/extensible-key-management-ekm.md)<br /><br /> [Azure 密钥保管库中存储的密钥](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)<br /><br /> [始终加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md)|  
|**列、数据和密钥加密**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 使用证书进行加密<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 使用对称密钥进行加密<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 使用非对称密钥进行加密<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 使用密码进行加密|[使用证书进行加密](../../t-sql/functions/encryptbycert-transact-sql.md)<br /><br /> [使用非对称密钥进行加密](../../t-sql/functions/encryptbyasymkey-transact-sql.md)<br /><br /> [使用对称密钥进行加密](../../t-sql/functions/encryptbykey-transact-sql.md)<br /><br /> [使用密码进行加密](../../t-sql/functions/encryptbypassphrase-transact-sql.md)<br /><br /> [加密数据列](../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
##  <a name="Connect"></a> 连接安全：限制和保护  
  
|||  
|-|-|  
|**防火墙保护**<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") Windows 防火墙设置<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") Azure 服务防火墙设置<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") 数据库防火墙设置|[为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)<br /><br /> [Azure SQL 数据库防火墙设置](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)<br /><br /> [Azure 服务防火墙设置](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)|  
|**在传输过程中加密数据**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 强制的 SSL 连接<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") 可选的 SSL 连接|[用于数据库引擎的安全套接字层](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)<br /><br /> [用于 SQL 数据库的安全套接字层](https://msdn.microsoft.com/library/azure/ff394108.aspx)<br /><br /> [针对 Microsoft SQL Server 的 TLS 1.2 支持](https://support.microsoft.com/kb/3135244)|  
  
##  <a name="Audit"></a> 审核：记录访问  
  
|||  
|-|-|  
|**自动审核**<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 审核（服务器和 DB 级别）<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 审核（数据库级别）<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") 威胁检测| <br /><br /> [SQL Server Audit（数据库引擎）](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)<br /><br /> [SQL 数据库审核](http://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> [SQL 数据库威胁检测入门](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/) <br /><br /> [SQL 数据库漏洞评估](https://docs.microsoft.com/en-us/azure/sql-database/sql-vulnerability-assessment) |  
|**自定义审核**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 触发器|自定义审核实现：创建 [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md) 和 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)|  
|**遵从性**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 符合性|SQL Server：<br />                        [通用准则](http://go.microsoft.com/fwlink/?LinkId=616319)<br /><br /> SQL 数据库：<br />                        [Microsoft Azure 信任中心：合规性（按功能）](http://azure.microsoft.com/support/trust-center/services/)|  
  
##  <a name="SQLInjection"></a> SQL 注入  
 SQL 注入是一种攻击方式，可将恶意代码插入字符串中，稍后这些字符串会传递到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 进行分析和执行。 任何构成 SQL 语句的过程都应进行注入漏洞检查，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将执行其接收到的所有语法有效的查询。 所有的数据库系统都会面临一些受到 SQL 注入攻击的风险，并会受到正在查询 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的应用程序中引入的许多安全漏洞的威胁。 你可以防止受到 SQL 注入攻击，具体方法为使用存储过程和参数化命令，避免使用动态 SQL，并限制所有用户的权限。  有关详细信息，请参阅 [SQL Injection](../../relational-databases/security/sql-injection.md)。  
  
 向应用程序程序员提供的其他链接：  
  
-   [SQL Server 中的应用程序安全方案](https://msdn.microsoft.com/library/bb669057.aspx)  
  
-   [在 SQL Server 中编写安全动态 SQL](https://msdn.microsoft.com/library/bb669091.aspx)  
  
-   [如何在 ASP.NET 内避免 SQL 注入](https://msdn.microsoft.com/library/ff648339.aspx)  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎权限入门](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [保护 SQL Server](../../relational-databases/security/securing-sql-server.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [SQL Server 证书和非对称密钥](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)   
 [SQL Server 加密](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [外围应用配置器](../../relational-databases/security/surface-area-configuration.md)   
 [强密码](../../relational-databases/security/strong-passwords.md)   
 [TRUSTWORTHY 数据库属性](../../relational-databases/security/trustworthy-database-property.md)   
 [数据库引擎功能和任务](http://msdn.microsoft.com/library/d9efe145-3306-4d61-bd77-e2af43e19c34)  
 [保护 SQL Server 知识产权](../../relational-databases/security/protecting-your-sql-server-intellectual-property.md)   
  
