---
title: 升级 Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
author: Minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b933796b755020f5ffdafb9904ab85a5d2202ba9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48202197"
---
# <a name="upgrade-analysis-services"></a>升级 Analysis Services
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关升级的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 SharePoint 模式下，请参阅[升级 PowerPivot for SharePoint](upgrade-power-pivot-for-sharepoint.md)。 有关升级现有的 SQL Server 实例，请参阅[升级到使用 SQL Server 2014 安装向导&#40;安装程序&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)。  
  
## <a name="known-upgrade-issues"></a>已知升级问题  
 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之前，请先查看以下内容：  
  
-   [SQL Server 2014 发行说明](http://go.microsoft.com/fwlink/?LinkID=296445)。  
  
-   若要了解哪些[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]特性和功能已停止使用，不推荐使用，或更改请参阅[Analysis Services 向后兼容性](../../analysis-services/analysis-services-backward-compatibility.md)。  
  
## <a name="pre-upgrade-checklist"></a>升级准备一览表  
 升级之前，请先查看以下信息：  
  
-   [支持的版本和版本升级](supported-version-and-edition-upgrades.md)  
  
-   [安装 SQL Server 2014 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [系统配置检查器的检查参数](check-parameters-for-the-system-configuration-checker.md)  
  
-   [安装 SQL Server 的安全注意事项](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [备份和还原 Analysis Services 数据库](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
-   [使用升级顾问来准备升级](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
## <a name="upgrading-analysis-services"></a>升级 Analysis Services  
 您可以选择几种方法之一来升级服务器和数据：  
  
-   **就地升级**替换现有的程序文件与[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]程序文件。 数据库保持在相同的位置中。 程序文件夹将更新以反映新名称。  
  
-   一个 **-并行升级**是新安装的[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]具有现有 Analysis Services 实例在同一计算机上。 可以将数据库移动到同一台计算机的新实例上，然后卸载旧版本（如果您不再继续使用这个旧版本）。  
  
-   可以也在新的硬件上安装 Analysis Services，然后将现有数据库迁移到该服务器。  
  
## <a name="in-place-upgrade"></a>就地升级  
 可以将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的现有实例升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] and, as part of the upgrade process, au的现有实例升级到matically migrate existing databases from the old instance 的现有实例升级到 the new instance. 因为元数据和二进制数据在两个版本之间兼容，因此升级之后您可以保留该数据而不必手动迁移该数据。  
  
 若要升级现有实例，请运行安装程序并将现有实例的名称指定为新实例的名称。  
  
## <a name="upgrading-databases"></a>升级数据库  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的之前版本中创建的数据库基于较旧的数据库兼容性级别设置在升级的服务器上运行。 在以下版本中创建的数据库的数据库兼容性级别为 105。 如果您要使用要求较新数据库兼容性级别的功能，则可以更改该兼容性级别。 否则，您可以使用原始设置在升级的服务器上运行数据库。 有关详细信息，请参阅[设置多维数据库的兼容性级别&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)。  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 的版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)   
 [了解 Microsoft OLAP 体系结构](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)   
 [升级 PowerPivot for SharePoint](upgrade-power-pivot-for-sharepoint.md)   
 [在多维和数据挖掘模式下安装 Analysis Services](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [PowerPivot for SharePoint 2010 安装](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
