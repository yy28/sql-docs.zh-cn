---
title: SQL server 2014 安装快速入门 |Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- quick start installation [SQL Server]
- installation [SQL Server]
- installing SQL Server, quick start installations
ms.assetid: 672afac9-364d-4946-ad5d-8a2d89cf8d81
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b06f5248152f8a11bf3e46d222df457f5442b6b4
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157243"
---
# <a name="quick-start-installation-of-sql-server-2014"></a>SQL Server 2014 安装快速入门
    
## <a name="introduction"></a>简介  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装向导基于 Windows Installer。 它提供了一个功能树以用来安装以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件：  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]  
  
-   管理工具  
  
-   连接组件  
  
 您可以单独安装每个组件，也可以选择上面列出的组件的组合。 若要作出最佳选择的版本和组件中提供[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]，请参阅[各版本和 SQL Server 2014 的组件](../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 有 32 位和 64 位两种版本可用。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装程序支持以下安装选项：  
  
-   **安装向导**  
  
     请参阅[从安装向导安装 SQL Server 2014&#40;安装程序&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)有关安装的过程信息[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用安装向导。  
  
-   **命令提示符**  
  
     请参阅[从命令提示符安装 SQL Server 2014](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)的示例语法和安装参数，用于运行无人参与的安装。  
  
-   **配置文件**  
  
     请参阅[使用安装 SQL Server 2014 配置文件](../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)的示例语法和安装参数，用于通过配置文件运行安装程序。  
  
-   **SysPrep**  
  
     请参阅[SysPrep 安装 SQL Server 2014 使用](../database-engine/install-windows/install-sql-server-using-sysprep.md)有关安装的过程信息[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 SysPrep。  
  
-   **服务器核心安装**  
  
     请参阅[Server Core 上安装 SQL Server 2014](../database-engine/install-windows/install-sql-server-on-server-core.md)有关安装的过程信息[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Windows Server Core 上。  
  
-   **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] BI 功能安装**  
  
     请参阅[安装 SQL Server 2014 BI 功能](../sql-server/install/install-sql-server-business-intelligence-features.md)有关安装 Microsoft BI 平台一部分的功能的信息，包括[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]， [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]， [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，以及几个用于创建或使用分析数据的客户端应用程序。  
  
-   **故障转移群集安装**  
  
     请参阅[SQL Server 故障转移群集安装](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)有关安装的过程信息[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]故障转移群集。  
  
 默认情况下，不会将示例数据库和示例代码作为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装程序的一部分进行安装。 对于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express Edition 以外的其他 SQL Server 版本，若要安装示例数据库和示例代码，请参阅 [CodePlex 网站](https://go.microsoft.com/fwlink/?LinkId=87843)。 若要了解对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]示例数据库和示例代码的支持，请参阅 [数据库和示例概述](https://go.microsoft.com/fwlink/?LinkId=110391)。  
  
## <a name="includessnoversionincludesssnoversion-mdmd-installation"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装  
 无论使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装向导还是命令提示符安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，安装过程都包括下列一个或多个步骤：  
  
-   查看 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装的安装要求、系统配置检查和安全注意事项。  有关详细信息，请参阅 [Planning a SQL Server Installation](quick-start-installation-of-sql-server-2014.md#BKMK_BeforeYouInstall)。  
  
-   运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装程序，将现有的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本升级到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]。 有关详细信息，请参阅[升级到 SQL Server 2014](#BKMK_Upgrading)。  
  
-   运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装程序，安装 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的新实例。 有关详细信息，请参阅[安装 SQL Server 2014](#BKMK_Install)。  
  
-   在您完成 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装后，下一主要步骤是配置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 及其组件。 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具配置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[配置 SQL Server 2014](#BKMK_Configure)。  
  
 您可以在下一节中找到这些任务的详细说明。  
  
## <a name="related-tasks"></a>Related Tasks  
  
###  <a name="BKMK_BeforeYouInstall"></a> 规划[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]安装  
 在安装 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 前，您必须查看硬件和软件要求、网络和 Internet 注意事项以及用于安装和运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的安全注意事项。 有关详细信息，请参阅[计划 SQL Server 安装](../../2014/sql-server/install/planning-a-sql-server-installation.md)和下列主题：  
  
|任务说明|主题|  
|----------------------|-----------|  
|查看硬件和软件要求、操作系统支持、网络和 Internet 注意事项以及硬盘空间要求。|[安装必备组件](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)|  
|查看安全注意事项[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]安装。|[安全注意事项](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)|  
|查看不同版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 所支持的功能的详细信息。|[功能和版本](features-supported-by-the-editions-of-sql-server-2014.md)|  
|从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所提供的版本和组件中确定最佳选择。|[SQL Server 2014 的版本和组件](../sql-server/editions-and-components-of-sql-server-2016.md)|  
|查看硬件配置并了解如何准备 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 故障转移群集安装。|[安装故障转移群集前的准备工作](../sql-server/failover-clusters/install/before-installing-failover-clustering.md)|  
  
###  <a name="BKMK_Upgrading"></a> 升级到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 您可以将 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 的现有实例升级到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]。 有关详细信息，请参阅[升级到 SQL Server 2014](../database-engine/install-windows/upgrade-sql-server.md)。 在运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装程序以升级到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 之前，请先查看以下有关升级过程的主题：  
  
|Description|主题|  
|-----------------|-----------|  
|介绍 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 支持的升级途径。|[支持的升级](../database-engine/install-windows/supported-version-and-edition-upgrades.md)|  
|介绍升级顾问，这是一种对 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 和 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 实例进行分析以识别已知升级问题的工具。|[使用升级顾问来准备升级](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)|  
|介绍 Distributed Replay 实用工具，这是一种可以使用多台计算机重播跟踪数据并模拟任务关键型工作负荷的工具。 通过在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 升级前和升级后在测试服务器上执行重播，可以测量性能差异，并查找您的应用程序可能与升级版本不兼容的问题。|[使用 Distributed Replay 实用工具准备升级](../../2014/sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md)|  
|列出在升级到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 后可能会影响应用程序的重要更改。|[向后兼容性](backward-compatibility.md)|  
|要将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的独立实例升级到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的过程主题。|[升级到 SQL Server 2014 使用安装向导&#40;安装程序&#41;](../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|  
|用于将某一 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本升级到其他版本的过程主题。 有关支持的版本升级路径的信息，请参阅 [支持的版本升级](../database-engine/install-windows/supported-version-and-edition-upgrades.md)。|[升级到 SQL Server 2014 的另一版本&#40;安装程序&#41;](../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)|  
|在所有故障转移群集节点上，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 都支持 [!INCLUDE[ssDE](../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 分别从 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 升级到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 故障转移群集。 查看此主题的详细信息。|[升级 SQL Server 故障转移群集](../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)|  
  
###  <a name="BKMK_Install"></a> 安装 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 有关针对 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的不同安装方案的信息，请参阅以下主题。  
  
|Description|主题|  
|-----------------|-----------|  
|提供的链接指向用于安装 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的不同组件的主题和用于安装 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的过程主题。|[安装 SQL Server 2014](../database-engine/install-windows/install-sql-server.md)|  
|查看该主题可了解如何在 Windows Server Core 上安装 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 。|[在 Server Core 上安装 SQL Server 2014](../database-engine/install-windows/install-sql-server-on-server-core.md)|  
|查看该主题可向 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的现有实例中添加单独的功能。|[将功能添加到 SQL Server 2014 的实例&#40;安装程序&#41;](../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)|  
|查看此主题以创建新的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 故障转移群集实例。|[创建新的 SQL Server 故障转移群集（安装程序）](../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|使用此主题可管理现有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 故障转移群集实例中的节点。|[在 SQL Server 故障转移群集中添加或删除节点（安装程序）](../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
|使用该主题可在故障转移群集上安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 客户端工具。|[在 SQL Server 故障转移群集上安装客户端工具](../sql-server/failover-clusters/install/install-client-tools-on-a-sql-server-failover-cluster.md)|  
|查看 SQL 发现报告的用法，以便确认 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的版本以及在计算机上安装的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能。|[验证 SQL Server 安装](../database-engine/install-windows/validate-a-sql-server-installation.md)|  
|提供 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的各种安装方法的过程主题链接，这些方法包括使用安装向导、命令提示符、配置文件或 SysPrep。|[安装操作指南主题](../../2014/sql-server/install/installation-how-to-topics.md)|  
  
## <a name="related-content"></a>相关内容  
 本节提供与配置和卸载 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 有关的信息。  
  
###  <a name="BKMK_Configure"></a> 配置 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 安装好 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 后，可以使用图形化实用工具和命令提示符实用工具进一步配置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 请参阅以下主题来首次配置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]：  
  
|Description|主题|  
|-----------------|-----------|  
|使用本主题中的信息可以确定您是否需要在防火墙中取消阻止端口，以便允许对 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 或 PowerPivot for SharePoint 的访问。 可以按照此主题，以配置端口和防火墙设置中提供的步骤。|[配置 Windows 防火墙以允许 Analysis Services 访问](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|  
|本主题概述了防火墙配置并汇总了 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理员所需的信息。|[配置 Windows 防火墙以允许 SQL Server 访问](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|本主题介绍如何在多宿主环境中对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和高级安全 Windows 防火墙进行配置，以便为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例提供多个网络连接。|[将多宿主计算机配置为允许 SQL Server 访问](../../2014/sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|  
  
###  <a name="BKMK_Uninstalling"></a> 卸载 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 下面的主题介绍如何手动卸载 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的独立实例和故障转移群集实例。  
  
|Description|主题|  
|-----------------|-----------|  
|本主题介绍如何手动卸载 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的独立实例。|[卸载 SQL Server 2014](../sql-server/install/uninstall-sql-server.md)|  
|本主题介绍如何卸载 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 故障转移群集实例。|[删除 SQL Server 故障转移群集实例（安装程序）](../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)|  
|本主题介绍在卸载 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 后或者仅卸载 DQS 服务器后如何手动删除 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (DQS) 对象的信息。|[删除数据质量服务器对象](../../2014/sql-server/install/remove-data-quality-server-objects.md)|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 的产品规格](sql-server-2014-product-specifications.md)   
 [开始使用 SQL Server 的产品文档](../2014-toc/books-online-for-sql-server-2014.md)[向后兼容性](backward-compatibility.md)  
  
  
