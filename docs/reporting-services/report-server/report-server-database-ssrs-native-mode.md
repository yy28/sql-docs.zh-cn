---
title: "报表服务器数据库 （SSRS 本机模式） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [Reporting Services]
- report servers [Reporting Services], databases
- temporary databases [Reporting Services]
- report server database
- reportservertempdb
- reportserver database
ms.assetid: 0fc5c033-3fe1-4cea-86c7-66ea5e424d65
caps.latest.revision: 48
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b580d66daa70a5c358a458a6c8f939f5bdabce48
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="report-server-database-ssrs-native-mode"></a>报表服务器数据库（SSRS 本机模式）
  报表服务器是一种无状态服务器，它使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 来存储元数据和对象定义。 为了将永久数据存储与临时存储要求分开，本机模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装使用两个数据库。 这两个数据库一起创建，并按名称绑定。 默认情况下，数据库名称分别为 **reportserver** 和 **reportservertempdb**。  
  
 SharePoint 模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装还将创建数据警报功能的数据库。 SharePoint 模式中的三个数据库与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序关联。 有关详细信息，请参阅 [管理 Reporting Services SharePoint 服务应用程序](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
 数据库可以在本地或远程 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例上运行。 如果您有足够的系统资源或要保留软件许可，则选择本地实例非常有用，但在远程计算机上运行数据库可以提高性能。  
  
 可以从以前的安装或包含其他报表服务器实例的不同实例中导入或重用现有的报表服务器数据库。 报表服务器数据库的架构必须与报表服务器实例兼容。 如果数据库为较早的格式，则系统将提示您将其升级到当前格式。 新版本不能降级为旧版本。 如果您有一个较新的报表服务器数据库，则无法将其与更早版本的报表服务器实例一起使用。 有关如何将报表服务器数据库升级到较新格式的详细信息，请参阅 [升级报表服务器数据库](../../reporting-services/install-windows/upgrade-a-report-server-database.md)。  
  
> [!IMPORTANT]  
>  数据库的表结构已经针对服务器操作进行了优化，因此不应对其进行修改或调整。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 可能会将表结构从一个版本更改为下一个版本。 如果修改或扩展数据库，可能会限制或阻止执行将来执行升级或应用 Service Pack 的能力。 还可能会引入破坏报表服务器操作的更改。 例如，如果在 ReportServer 数据库上启用 READ_COMMITTED_SNAPSHOT，将中断交互式排序功能。  
  
 必须通过报表服务器处理所有对报表服务器数据库的访问。 若要访问报表服务器数据库中的内容，可以使用报表服务器管理工具（例如报表管理器和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]），或者使用编程接口，例如 URL 访问、报表服务器 Web 服务或 Windows Management Instrumentation (WMI) 提供程序。  
  
 与报表服务器数据库的连接通常通过 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器来定义。 但是，如果您选择安装默认配置，则可以在安装过程中进行定义。 有关将报表服务器连接到数据库的详细信息，请参阅[配置报表服务器数据库连接（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
## <a name="report-server-database"></a>报表服务器数据库  
 报表服务器数据库是存储下列内容的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库：  
  
-   报表服务器所管理的项（报表和链接报表、共享数据源、报表模型、文件夹和资源）以及与这些项关联的所有属性和安全设置。  
  
-   订阅和计划定义。  
  
-   报表快照（包括查询结果）和报表历史记录。  
  
-   系统属性和系统级安全设置。  
  
-   报表执行日志数据。  
  
-   报表数据源的对称密钥以及加密连接和凭据。  
  
 因为报表服务器数据库存储应用程序状态和持久性数据，所以您应该为此数据库创建备份计划以防止数据丢失。 有关如何备份数据库的建议和说明，请参阅[将报表服务器数据库移至其他计算机（SSRS 本机模式）](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)。  
  
## <a name="report-server-temporary-database"></a>报表服务器临时数据库  
 每个报表服务器数据库都使用相关的临时数据库来存储报表服务器生成的会话和执行数据、缓存报表以及工作表。 后台服务器进程将定期从临时数据库的表中删除较旧的和未使用的项。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不会重新创建缺少的临时数据库，也不会修复缺少的或经过修改的表。 尽管临时数据库不包含持久性数据，但也应备份该数据库的副本，这样，就无须在故障恢复操作中重新创建该数据库。  
  
 如果在备份临时数据库后执行了恢复操作，则应删除其内容。 通常，在任何时候删除临时数据库的内容都是安全的。 但是，删除内容后必须重新启动报表服务器 Windows 服务。  
  
## <a name="see-also"></a>另请参阅  
 [在 SQL Server 故障转移群集中承载报表服务器数据库](../../reporting-services/install-windows/host-a-report-server-database-in-a-sql-server-failover-cluster.md)   
 [存储加密的 Report Server 数据（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services 报表服务器](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [管理报表服务器数据库（SSRS 本机模式）](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)   
 [创建报表服务器数据库（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
 [Reporting Services 的备份和还原操作](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)  
  
  
