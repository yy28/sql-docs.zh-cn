---
title: "安装 SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "AdventureWorks 示例数据库"
  - "安装 SQL Server, 准备安装"
  - "安装 [SQL Server]"
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 59
ms.author: "mikeray"
manager: "jhubbard"
---
# 安装 SQL Server 2016
  SQL Server 2016 是 64 位应用程序。 以下是有关如何获取 SQL Server 以及如何安装 SQL Server 的重要详细信息。

## <a name="installation-details"></a>安装详细信息
  
*  **选项**：通过安装向导、命令提示符或 sysprep 进行安装
 
*  **要求**：安装之前，请先查看[计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)中的安装要求、系统配置检查和安全注意事项 

* **过程**：有关安装过程的完整说明，请参阅[安装 SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md)

* **示例数据库和示例代码**： 
    * 默认情况下，它们不作为 SQL Server 安装程序的一部分安装 
    * 若要为 SQL Server 的非 Express 版本安装它们，请参阅 [CodePlex 网站](http://go.microsoft.com/fwlink/?LinkId=87843)
    * 若要了解对 SQL Server Express 的 SQL Server 示例数据库和示例代码的支持，请参阅[数据库和示例概述](http://go.microsoft.com/fwlink/?LinkId=110391)
    

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的下载位置由版本决定：

- “SQL Server Enterprise、Standard 和 Express Edition”已获授权，可供生产之用。 对于企业版和标准版，请联系软件供应商获取安装媒体。 你可以在 [Microsoft 采购网站](https://www.microsoft.com/en-us/server-cloud/products/sql-server/overview.aspx)上找到采购信息和 Microsoft 合作伙伴目录。 

- 以下链接提供有“免费版本”：

| 版本 | Description
|---------|--------
|[开发人员版](http://myprodscussu1.app.vssubscriptions.visualstudio.com/Downloads?q=SQL%20Server%20Developer) | 免费的功能齐全的 SQL Server 2016 企业版软件让开发人员可以在非生产环境中构建、测试和演示应用程序。 
|[速成版](http://www.microsoft.com/download/details.aspx?id=52679)|  入门级的免费数据库，是在生产环境中部署小型数据库的理想选择。 生成最多 10 GB 磁盘大小的桌面、小型服务器和数据驱动应用程序。 
| [评估版](http://technet.microsoft.com/evalcenter/mt130694) | 功能齐全的 SQL Server 企业版软件，可提供 180 天评估期。
   
 
  

## <a name="how-to-install-sql-server"></a>如何安装 SQL Server
 
|标题|Description|  
|-----------|-----------------|  
|[在 Server Core 上安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-on-server-core.md)|查看该主题可了解如何在 Windows Server Core 上安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|[系统配置检查器的检查参数](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|讨论系统配置检查器 (SCC) 的功能。|  
|[使用安装向导安装 SQL Server 2016（安装程序）](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)|介绍如何通过使用安装向导进行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 典型安装的过程主题。|  
|[从命令提示符安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|提供运行无人参与安装的示例语法和安装参数的过程主题。|  
|[使用配置文件安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|提供通过配置文件运行安装程序的示例语法和安装参数的过程主题。|  
|[使用 SysPrep 安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-using-sysprep.md)|提供通过 SysPrep 运行安装程序的示例语法和安装参数的过程主题。|  
|[向 SQL Server 2016 的实例添加功能（安装程序）](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|介绍如何更新现有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例的组件的过程主题。|  
|[修复失败的 SQL Server 2016 安装](../../database-engine/install-windows/repair-a-failed-sql-server-2016-installation.md)|介绍如何修复损坏的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装的过程主题。|  
|[重命名托管 SQL Server 独立实例的计算机](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|介绍如何更新存储在 sys.servers 中的系统元数据的过程主题。|  
|[安装 SQL Server 2016 服务更新](../../database-engine/install-windows/install-sql-server-2016-servicing-updates.md)|为 SQL Server 2016 安装更新的过程主题。|  
|[查看和读取 SQL Server 安装程序日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|介绍如何在安装日志文件中检查错误的过程主题。|  
|[验证 SQL Server 安装](../../database-engine/install-windows/validate-a-sql-server-installation.md)|查看 SQL 发现报告的用法，以便确认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本以及在计算机上安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。|  
  
  
## <a name="how-to-install-individual-components"></a>如何安装各个组件  
  
|主题|Description|  
|-----------|-----------------|  
|[安装 SQL Server 数据库引擎](../../database-engine/install-windows/install-sql-server-database-engine.md)|说明如何安装和配置 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。|  
|[安装 SQL Server 复制](../../database-engine/install-windows/install-sql-server-replication.md)|说明如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制。|  
|[安装 Distributed Replay - 概述](../../tools/distributed-replay/install-distributed-replay-overview.md)|列出了有关安装 Distributed Replay 功能的主题。|  
|[安装带有 SSMS 的 SQL Server 管理工具](Install%20SQL%20Server%20Management%20Tools%20\(SSMS\).md)|说明如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具。|  
|[安装 SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|介绍安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 组件的注意事项。|  
  

## <a name="how-to-configure-sql-server"></a>如何配置 SQL Server  
  
|主题|Description|  
|-----------|-----------------|  
|[配置 Windows 防火墙以允许 SQL Server 访问](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|本主题概述了防火墙配置和 Windows 防火墙配置方法。|  
|[将多宿主计算机配置为允许 SQL Server 访问](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|本主题介绍如何在多宿主环境中对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和高级安全 Windows 防火墙进行配置，以便为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例提供多个网络连接。|  
|[配置 Windows 防火墙以允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|可以按照本主题中提供的步骤配置端口和防火墙设置，以允许访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或用于 SharePoint 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 。|  
  
## <a name="related-sections"></a>相关章节  
[SQL Server 2016 各个版本支持的功能](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
[安装 SQL Server 2016 商业智能功能](../../sql-server/install/install-sql-server-2016-business-intelligence-features.md)  
  [SQL Server 故障转移群集安装](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>另请参阅  

[计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)   
 [升级到 SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)   
 [卸载 SQL Server 2016](../../sql-server/install/uninstall-sql-server-2016.md)   
 [高可用性解决方案 (SQL Server)](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  