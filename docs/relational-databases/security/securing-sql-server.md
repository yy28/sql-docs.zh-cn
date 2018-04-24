---
title: 保护 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- database objects [SQL Server], security
- SQL Server, security
- operating systems [SQL Server], security
- security [SQL Server], planning
- applications [SQL Server], security
ms.assetid: 4d93489e-e9bb-45b3-8354-21f58209965d
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 07ab7d7c420d1b0c9809f58476d2bf8f6b4b0260
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="securing-sql-server"></a>保护 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可将保护 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 视为一系列步骤，它涉及四个方面：平台、身份验证、对象（包括数据）以及访问系统的应用程序。 下列主题将指导您完成创建和实现有效安全计划的过程。  
  
 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Server [网站上找到有关](http://go.microsoft.com/fwlink/?LinkID=31629) 安全性的详细信息。 此类信息包括最佳实践指南和安全清单。 此网站还包含最新的 Service Pack 信息和下载。  
  
## <a name="platform-and-network-security"></a>平台与网络安全性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的平台包括物理硬件和将客户端连接到数据库服务器的联网系统，以及用于处理数据库请求的二进制文件。  
  
### <a name="physical-security"></a>物理安全性  
 物理安全性的最佳实践是严格限制对物理服务器和硬件组件的接触。 例如，将数据库服务器硬件和联网设备放在限制进入的上锁房间。 此外，还可通过将备份介质存储在安全的现场外位置，限制对其接触。  
  
 实现物理网络安全首先要防止未经授权的用户访问网络。 下表包含有关联网安全信息的详细信息。  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)] 和对其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的网络访问|[!INCLUDE[ssEW](../../includes/ssew-md.md)] 联机丛书中的“配置和保护服务器环境的安全性”|  
  
### <a name="operating-system-security"></a>操作系统安全性  
 操作系统 Service Pack 和升级包含重要的安全性增强功能。 通过数据库应用程序对所有更新和升级进行测试后，再将它们应用到操作系统。  
  
 防火墙也提供了实现安全性的有效方式。 从逻辑上讲，防火墙是网络通信的隔离者或限制者，可配置为执行您组织的数据安全性策略。 如果使用防火墙，则可通过提供一个检查点（在此可着重关注安全措施）来增强操作系统级别的安全性。 下表包含有关如何将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与防火墙一起使用的详细信息。  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|为使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)|  
|为使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[Integration Services 服务（SSIS 服务）](../../integration-services/service/integration-services-service-ssis-service.md)|  
|为使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[将 Windows 防火墙配置为允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|  
|打开防火墙上的特定端口以便启用对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[配置 Windows 防火墙以允许 SQL Server 访问](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|通过使用渠道绑定和服务绑定，配置对针对验证的扩展保护的支持|[使用扩展保护连接到数据库引擎](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)|  
  
 减少外围应用是一项安全措施，它涉及停止或禁用未使用的组件。 减少外围应用后，对系统带来潜在攻击的途径也会减少，从而有助于提高安全性。 限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外围应用的关键在于通过仅向服务和用户授予适当的权限来运行具有“最小权限”的所需服务。 下表包含有关服务和系统访问的详细信息。  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|所需的服务 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)|  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统使用了 Internet Information Services (IIS)，则还需要采用其他步骤来帮助确保平台外围的安全。 下表包含有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Internet 信息服务的信息。  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|的 IIS 安全性 [!INCLUDE[ssEW](../../includes/ssew-md.md)]|[!INCLUDE[ssEW](../../includes/ssew-md.md)] 联机丛书中的“IIS 安全性”|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 身份验证|[Reporting Services 中的身份验证](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md)|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)] 和 IIS 访问|[!INCLUDE[ssEW](../../includes/ssew-md.md)] 联机丛书中的“Internet Information Services 安全性流程图”|  
  
### <a name="sql-server-operating-system-files-security"></a>SQL Server 操作系统文件安全性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用操作系统文件进行操作和数据存储。 文件安全性的最佳实践要求您限制对这些文件的访问。 下表包含有关这些文件的信息。  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程序文件|[SQL Server 的默认实例和命名实例的文件位置](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升级提供了增强的安全性。 若要确定可用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的最新 Service Pack，请访问 [SQL Server](http://go.microsoft.com/fwlink/?LinkID=31629) 网站。  
  
 您可以使用以下脚本来确定系统上安装的 Service Pack。  
  
```  
SELECT CONVERT(char(20), SERVERPROPERTY('productlevel'));  
GO  
```  
  
## <a name="principals-and-database-object-security"></a>主体与数据库对象安全性  
 主体是获得了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]访问权限的个体、组和进程。 “安全对象”是服务器、数据库和数据库包含的对象。 每个安全对象都拥有一组权限，可对这些权限进行配置以减少 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外围应用。 下表包含有关主体和安全对象的信息。  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|服务器和数据库用户、角色与进程|[主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)|  
|服务器和数据库对象安全性|[安全对象](../../relational-databases/security/securables.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性层次结构|[权限层次结构（数据库引擎）](../../relational-databases/security/permissions-hierarchy-database-engine.md)|  
  
### <a name="encryption-and-certificates"></a>加密和证书  
 加密并不解决访问控制问题。 不过，它可以通过限制数据丢失来增强安全性，即使在访问控制失效的罕见情况下也能如此。 例如，在数据库主机配置有误且恶意用户获取了敏感数据（如信用卡号）的情况下，如果被盗信息已加密，则此信息将毫无用处。 下表包含有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的加密的详细信息。  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|中的加密层次结构 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)|  
|实现安全连接|[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)|  
|加密函数|[加密函数 (Transact-SQL)](../../t-sql/functions/cryptographic-functions-transact-sql.md)|  
  
 证书是在两个服务器之间共享的软件“密钥”，使用证书后，可以通过严格的身份验证实现安全通信。 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建和使用证书，以增强对象和连接的安全性。 下表包含有关如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用证书的信息。  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|创建由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)|  
|为数据库镜像使用证书|[使用数据库镜像终结点证书 (Transact-SQL)](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|  
  
## <a name="application-security"></a>应用程序安全性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性最佳实践包括编写安全客户端应用程序。  
  
 有关如何在网络层保护客户端应用程序安全的详细信息，请参阅 [Client Network Configuration](../../database-engine/configure-windows/client-network-configuration.md)。  
  
## <a name="sql-server-security-tools-utilities-views-and-functions"></a>SQL Server 安全性工具、实用工具、视图和函数  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了可用来配置和管理安全性的工具、实用工具、视图和函数。  
  
### <a name="sql-server-security-tools-and-utilities"></a>SQL Server 安全性工具和实用工具  
 下表包含有关可用来配置和管理安全的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具与实用工具的信息。  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|连接、配置和控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[使用 SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)|  
|连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并在命令提示符下运行查询|[sqlcmd 实用工具](../../tools/sqlcmd-utility.md)|  
|网络配置和控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)|  
|使用基于策略的管理启用和禁用功能|[使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)|  
|操作报表服务器的对称密钥|[rskeymgmt 实用工具 (SSRS)](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)|  
  
### <a name="sql-server-security-catalog-views-and-functions"></a>SQL Server 安全性目录视图和函数  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在若干视图和函数（已为性能和效用进行了优化）中显示安全信息。 下表包含有关安全性视图和函数的信息。  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性目录视图，可返回有关数据库级别和服务器级别权限、主体、角色等的信息。 此外，还有提供加密密钥、证书和凭据相关信息的目录视图。|[安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全函数。|[安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性动态管理视图。|[与安全性相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)|  
  
## <a name="related-content"></a>相关内容  
 [安装 SQL Server 的安全注意事项](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 [SQL Server 数据库引擎和 Azure SQL Database 的安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[SQL Server 2012 安全最佳做法 - 操作和管理任务。](http://download.microsoft.com/download/8/F/A/8FABACD7-803E-40FC-ADF8-355E7D218F4C/SQL_Server_2012_Security_Best_Practice_Whitepaper_Apr2012.docx)   
[SQL Server 安全博客](https://blogs.msdn.microsoft.com/sqlsecurity/)  
[安全最佳做法和标签安全白皮书](https://blogs.msdn.microsoft.com/sqlsecurity/2012/03/06/security-best-practice-and-label-security-whitepapers/)  
[行级安全性](../../relational-databases/security/row-level-security.md)   
[保护 SQL Server 知识产权](../../relational-databases/security/protecting-your-sql-server-intellectual-property.md)   
  
