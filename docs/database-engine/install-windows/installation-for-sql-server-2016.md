---
title: "安装 SQL Server 2016 | Microsoft Docs"
ms.custom: ""
ms.date: "04/13/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.portal.Installation.f1"
helpviewer_keywords: 
  - "安装 SQL Server, 初始安装"
  - "安装 [SQL Server]"
  - "初始安装 [SQL Server]"
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 34
---
# 安装 SQL Server 2016
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导提供一个功能树以用来安装所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
  
-   连接组件  
  
 从 SQL Server 2016 开始，SQL Server 管理工具不再从主功能树安装 SQL Server 管理工具；有关详细信息，请参阅[安装带有 SSMS 的 SQL Server 管理工具](Install%20SQL%20Server%20Management%20Tools%20\(SSMS\).md)  
  
 您可以单独安装每个组件，也可以选择上面列出的组件的组合。 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的不同版本和可用组件中做出最佳选择，请参阅 [SQL Server 2016 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)和 [SQL Server 2016 各个版本支持的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)。  
  
## 本节内容  
 无论使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导还是命令提示符安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，安装都包括下列步骤：  
  
 [计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)  
 说明如何为安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而准备计算机：  
  
-   硬件和软件要求。  
  
-   系统配置检查器的要求和妨碍性问题。  
  
-   安全注意事项。  
  
 [安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md)  
 说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安装选项。  
  
 [SQL Server 安装程序的用户界面参考](../Topic/SQL%20Server%20Setup%20User%20Interface%20Reference.md)  
 说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导提供的安装选项。  
  
 [升级到 SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)  
 介绍用于升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的选项。  
  
 [卸载 SQL Server 2016](../../sql-server/install/uninstall-sql-server-2016.md)  
 说明卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 的过程。  
  
 [SQL Server 故障转移群集安装](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装文档中的本节介绍了如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集。  
  
 [安装 SQL Server 2016 商业智能功能](../../sql-server/install/install-sql-server-2016-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft BI 平台的部分功能包括：[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，以及用于创建或使用分析数据的若干客户端应用程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装文档中的本节说明如何安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
## 详细信息  
 [使用 SharePoint 安装 SQL Server BI 功能（Power Pivot 和 Reporting Services）](../Topic/Install%20SQL%20Server%20BI%20Features%20with%20SharePoint%20\(Power%20Pivot%20and%20Reporting%20Services\).md)  
 本节介绍如何在 SharePoint 环境中安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 它标识对于特定版本的 SharePoint，提供了哪些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 本节还包含在 SharePoint 模式下安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 和 Reporting Services 的过程。  
  
 ![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) 安装新的示例数据库 [Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)。 
  
 [其他 SQL Server 示例和示例数据库](http://sqlserversamples.codeplex.com/)  
 说明如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 示例和示例数据库。  
  
有关所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 受支持版本的链接和信息，请参阅 [SQL Server 更新中心](https://msdn.microsoft.com/library/ff803383.aspx)。  
  
## 另请参阅  
 [SQL Server 安装中的新增功能](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
 [安装 SQL Server 2016 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)  
  
  