---
title: 升级 Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9c3543f3-3eb9-455d-a9bf-f17e9506ad21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: da78f21c6346281dc23332f40e8e6f46ff07aa06
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774651"
---
# <a name="upgrade-master-data-services"></a>升级 Master Data Services
  有四种升级到 Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 的方案。 请选择适用于您情况的方案。  
  
-   [升级（不升级数据库引擎）](#noengine)  
  
-   [升级（升级数据库引擎）](#engine)  
  
-   [在两台计算机的方案中升级](#twocomputer)  
  
-   [升级并从备份还原数据库](#restore)  
  
> [!IMPORTANT]
>  -   不支持从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP1 版升级到 CTP2 版。  
> -   在执行任何升级之前备份您的数据库。  
> -   升级过程将重新创建存储过程并对 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]所使用的表进行升级。 您对这些组件中的任何一个所做的任何自定义内容可能会丢失。  
> -   模型部署包只能在创建它们的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中使用。 不能将在中创建的模型[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]部署[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]包部署到中。  
> -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 在将 Master Data Services 和 Data Quality Services 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 后，您可以使用用于 Excel 的 Master Data Services 外接程序的  SP1 版本继续进行。 但是，在升级到 SQL Server 2014 CTP2 后，用于 Excel 的 Master Data Services 外接程序的任何早期版本都无法使用。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 您可以从 [此处](https://go.microsoft.com/fwlink/?LinkId=328664)下载用于 Excel 的 Master Data Services 外接程序的  SP1 版本。  
  
##  <a name="upgrade-without-database-engine-upgrade"></a><a name="noengine"></a>升级但不数据库引擎升级  
 此方案可被视为[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]并行安装，因为和[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]均并行安装在同一台计算机或不同的计算机上。  
  
 在此方案中，您继续使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 承载 MDS 数据库。 但是，必须升级 MDS 数据库的架构，然后创建 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 应用程序来访问 MDS 数据库。 MDS 数据库不再可以由 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Web 应用程序访问。  
  
 如果选择在同一台[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]计算机上安装和早期版本的[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]/[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SQL Server （），则可以这样做，因为文件安装在不同的位置。  
  
-   在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，默认情况下这些文件安装在驱动器**:\Program Files\Microsoft SQL Server\120\Master Data Services 中。  
  
-   在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，默认情况下这些文件安装在驱动器**:\Program Files\Microsoft SQL Server\110\Master Data Services 中。  
  
-   在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 中，默认情况下这些文件安装在驱动器**:\Program Files\Microsoft SQL Server\Master Data Services 中。  
  
 若要执行此任务，请完成以下步骤：  
  
1.  安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 和所需的任何其他功能。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导。  
  
    2.  在左窗格中，单击 **“安装”**。  
  
    3.  在右窗格中，单击“全新 SQL Server 独立安装或向现有安装添加功能”****。  
  
    4.  在 **“功能选择”** 页上，选择 **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** 和要安装的任何其他功能。  
  
    5.  完成向导。  
  
2.  安装完成后，升级 MDS 数据库架构。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
        > [!IMPORTANT]  
        >  若要升级 MDS 数据库架构，您必须以在创建 MDS 数据库时指定的管理员帐户登录。 在 MDS 数据库的 mdm.tblUser 中，此用户的 **ID** 值为 **1**。 有关更改此用户的信息，请参阅[更改系统管理员帐户 &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)。  
  
    2.  在左窗格中单击 **“数据库配置”** 。  
  
    3.  在右侧窗格中，单击 "**选择数据库**" 并指定[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]数据库实例的信息。  
  
    4.  单击 **“升级数据库”** 以启动 **“升级数据库向导”** 。 有关详细信息，请参阅[升级数据库向导（Master Data Services 配置管理器）](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)。  
  
3.  升级完成时，创建一个 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 应用程序。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
    2.  在左窗格中单击 **“Web 配置”** 。  
  
    3.  在右窗格中，从 **“网站”** 列表选择以下选项之一：  
  
        -   **“默认网站”** ，然后单击 **“创建应用程序”** 。  
  
        -   **“创建新站点”** 。 创建网站时，将自动创建新的 Web 应用程序。  
  
        > [!IMPORTANT]  
        >  在 SQL Server 2014 版 Master Data Services 配置管理器中，您可以选择 SQL Server 早期版本（[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]）的现有 MDS Web 应用程序。 您不能选择现有 Web 应用程序，而是必须为 MDS 创建一个 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 应用程序。 否则，在您尝试将 Web 应用程序与升级的 MDS 数据库关联时，您会收到错误，指出无法访问请求的页面，因为该页的相关配置数据无效。  
        >   
        >  如果您要为 MDS Web 应用程序使用与现有（[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]）Web 应用程序相同的名字（别名），您必须首先从 IIS 中删除该 Web 应用程序和关联的应用程序池，然后使用 SQL Server 2014 版 Master Data Services 配置管理器创建同名的 Web 应用程序。 有关从 IIS 删除 Web 应用程序和应用程序池的信息，请参阅 [删除应用程序 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) 和 [删除应用程序池 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538)。  
  
4.  现在将新 Web 应用程序与已升级的 MDS 数据库关联。  
  
    1.  在 **“将应用程序与数据库相关联”** 部分中，单击 **“选择”** 。  
  
    2.  选择 MDS 数据库。  
  
    3.  单击“应用”  。  
  
##  <a name="upgrade-with-database-engine-upgrade"></a><a name="engine"></a> 升级（升级数据库引擎）  
 在此方案中，您同时将数据库引擎和 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 应用程序从 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 SQL Server 2012 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 若要执行此任务，请完成以下步骤：  
  
1.  **仅适用于 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** ：打开“控制面板” **“程序和功能”，然后卸载 Microsoft**  >   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]。  
  
2.  将数据引擎升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导。  
  
    2.  在左窗格中，单击 **“安装”**。  
  
    3.  在右侧窗格中，单击 "**从 SQL Server 2005 升级，SQL Server 2008"，SQL Server 2008 R2 或 SQL Server 2012**。  
  
    4.  完成向导。  
  
3.  **仅[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]适用于**：升级完成时，添加**[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** 功能。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导。  
  
    2.  在左窗格中，单击 **“安装”**。  
  
    3.  在右窗格中，单击“全新 SQL Server 独立安装或向现有安装添加功能”****。  
  
    4.  在向导的 "**安装类型**" 页上，选择 "向**现有实例中添加功能**" 选项，然后选择安装 MDS 数据库的实例。  
  
    5.  在 "**功能选择**" 页上的 "**共享功能**" 下，选择**[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]**。  
  
    6.  完成向导。  
  
4.  升级 MDS 数据库架构。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
        > [!IMPORTANT]  
        >  若要升级 MDS 数据库架构，您必须以在创建 MDS 数据库时指定的管理员帐户登录。 在 MDS 数据库的 mdm.tblUser 中，此用户的 **ID** 值为 **1**。 有关更改此用户的信息，请参阅[更改系统管理员帐户 &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)。  
  
    2.  在左窗格中单击 **“数据库配置”**。  
  
    3.  在右侧窗格中，单击 "**选择数据库**" 并指定数据库实例的信息。  
  
    4.  单击 **“升级数据库”** 以启动 **“升级数据库向导”**。 有关详细信息，请参阅[升级数据库向导（Master Data Services 配置管理器）](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)。  
  
    5.  单击“应用”  。  
  
5.  升级完成时，创建一个 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 应用程序。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
    2.  在左窗格中单击 **“Web 配置”**。  
  
    3.  在右窗格中，从 **“网站”** 列表选择以下选项之一：  
  
        -   **“默认网站”**，然后单击 **“创建应用程序”**。  
  
        -   **“创建新站点”**。 创建网站时，将自动创建新的 Web 应用程序。  
  
        > [!IMPORTANT]  
        >  在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版 Master Data Services 配置管理器中，您可以选择 SQL Server 早期版本（[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）的现有 MDS Web 应用程序。 您不能选择现有 Web 应用程序，而是必须为 MDS 创建一个 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 应用程序。 否则，在您尝试将 Web 应用程序与升级的 MDS 数据库关联时，您会收到错误，指出无法访问请求的页面，因为该页的相关配置数据无效。  
        >   
        >  如果您要为 MDS Web 应用程序使用与现有（[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]）Web 应用程序相同的名字（别名），您必须首先从 IIS 中删除该 Web 应用程序和关联的应用程序池，然后使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版 Master Data Services 配置管理器创建同名的 Web 应用程序。 有关从 IIS 删除 Web 应用程序和应用程序池的信息，请参阅 [删除应用程序 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) 和 [删除应用程序池 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538)。  
  
6.  现在将新 Web 应用程序与已升级的 MDS 数据库关联。  
  
    1.  在 **“将应用程序与数据库相关联”** 部分中，单击 **“选择”**。  
  
    2.  选择 MDS 数据库。  
  
    3.  单击“应用”  。  
  
##  <a name="upgrade-in-two-computer-scenario"></a><a name="twocomputer"></a> 在两台计算机上执行升级的方案  
 此方案涉及升级在两台计算机上安装 SQL Server 的系统：一台计算机安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，另一台计算机安装 SQL Server 2008 R2 或 SQL Server 2012。  
  
 如果安装 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，您将继续分别使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 在一台计算机上承载 MDS 数据库。 但是，必须升级 MDS 数据库的架构，然后使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 应用程序来访问 MDS 数据库。 MDS 数据库不再可以由 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Web 应用程序访问。  
  
-   在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，默认情况下这些文件安装在驱动器**:\Program Files\Microsoft SQL Server\120\Master Data Services 中。  
  
-   在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，默认情况下这些文件安装在驱动器**:\Program Files\Microsoft SQL Server\110\Master Data Services 中。  
  
-   在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 中，默认情况下这些文件安装在驱动器**:\Program Files\Microsoft SQL Server\Master Data Services 中。  
  
 若要执行此任务，请完成以下步骤：  
  
1.  安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 和所需的任何其他功能。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导。  
  
    2.  在左窗格中，单击 **“安装”**。  
  
    3.  在右窗格中，单击“全新 SQL Server 独立安装或向现有安装添加功能”****。  
  
    4.  在 **“功能选择”** 页上，选择 **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** 和要安装的任何其他功能。  
  
    5.  完成向导。  
  
2.  安装完成后，升级 MDS 数据库架构。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
        > [!IMPORTANT]  
        >  若要升级 MDS 数据库架构，您必须以在创建 MDS 数据库时指定的管理员帐户登录。 在 MDS 数据库的 mdm.tblUser 中，此用户的 **ID** 值为 **1**。 有关更改此用户的信息，请参阅[更改系统管理员帐户 &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)。  
  
    2.  在左窗格中单击 **“数据库配置”**。  
  
    3.  在右侧窗格中，单击 **"选择数据库**"，然后在另[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]一[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]台计算机上安装或数据库实例的[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]信息[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] （如果在其他计算机上安装了或）。  
  
    4.  单击 **“升级数据库”** 以启动 **“升级数据库向导”**。 有关详细信息，请参阅[升级数据库向导（Master Data Services 配置管理器）](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)。  
  
3.  升级完成时，创建一个 SQL Server 2014 Web 应用程序。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
    2.  在左窗格中单击 **“Web 配置”**。  
  
    3.  在右窗格中，从 **“网站”** 列表选择以下选项之一：  
  
        -   **“默认网站”**，然后单击 **“创建应用程序”**。  
  
        -   **“创建新站点”**。 创建网站时，将自动创建新的 Web 应用程序。  
  
        > [!IMPORTANT]  
        >  在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版 Master Data Services 配置管理器中，您可以选择 SQL Server 早期版本（[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）的现有 MDS Web 应用程序。 您不能选择现有 Web 应用程序，而是必须为 MDS 创建一个 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 应用程序。 否则，在您尝试将 Web 应用程序与升级的 MDS 数据库关联时，您会收到错误，指出无法访问请求的页面，因为该页的相关配置数据无效。  
        >   
        >  如果您要为 MDS Web 应用程序使用与现有（[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]）Web 应用程序相同的名字（别名），您必须首先从 IIS 中删除该 Web 应用程序和关联的应用程序池，然后使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版 Master Data Services 配置管理器创建同名的 Web 应用程序。 有关从 IIS 删除 Web 应用程序和应用程序池的信息，请参阅 [删除应用程序 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) 和 [删除应用程序池 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538)。  
  
4.  现在将 Web 应用程序与已升级的 MDS 数据库关联。  
  
    1.  在 **“将应用程序与数据库相关联”** 部分中，单击 **“选择”**。  
  
    2.  选择 MDS 数据库。  
  
    3.  单击“应用”  。  
  
##  <a name="upgrade-with-restoring-a-database-from-backup"></a><a name="restore"></a> 通过从备份还原数据库升级  
 在此方案中，[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 与 SQL Server 2008 R2 或 SQL Server 2012 安装在同一台或两台不同的计算机上。 另外，在升级前，在低于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 的版本上备份数据库，必须还原该数据库。  
  
-   在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，默认情况下这些文件安装在驱动器**:\Program Files\Microsoft SQL Server\120\Master Data Services 中。  
  
-   在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，默认情况下这些文件安装在驱动器**:\Program Files\Microsoft SQL Server\110\Master Data Services 中。  
  
-   在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 中，默认情况下这些文件安装在驱动器**:\Program Files\Microsoft SQL Server\Master Data Services 中。  
  
 若要执行此任务，请完成以下步骤：  
  
1.  安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 和所需的任何其他功能。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导。  
  
    2.  在左窗格中，单击 **“安装”**。  
  
    3.  在右窗格中，单击“全新 SQL Server 独立安装或向现有安装添加功能”****。  
  
    4.  在 **“功能选择”** 页上，选择 **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** 和要安装的任何其他功能。  
  
    5.  完成向导。  
  
2.  还原已备份的数据库。  
  
3.  安装完成后，升级 MDS 数据库架构。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
        > [!IMPORTANT]  
        >  若要升级 MDS 数据库架构，您必须以在创建 MDS 数据库时指定的管理员帐户登录。 在 MDS 数据库的 mdm.tblUser 中，此用户的 **ID** 值为 **1**。 有关更改此用户的信息，请参阅[更改系统管理员帐户 &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)。  
  
    2.  在左窗格中单击 **“数据库配置”**。  
  
    3.  在右侧窗格中，单击 "**选择数据库**" 并指定[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]数据库实例的信息。  
  
    4.  单击 **“升级数据库”** 以启动 **“升级数据库向导”**。 有关详细信息，请参阅[升级数据库向导（Master Data Services 配置管理器）](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)。  
  
4.  升级完成时，创建一个 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 应用程序。  
  
    1.  打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
    2.  在左窗格中单击 **“Web 配置”**。  
  
    3.  在右窗格中，从 **“网站”** 列表选择以下选项之一：  
  
        -   **“默认网站”**，然后单击 **“创建应用程序”**。  
  
        -   **“创建新站点”**。 创建网站时，将自动创建新的 Web 应用程序。  
  
        > [!IMPORTANT]  
        >  在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版 Master Data Services 配置管理器中，您可以选择 SQL Server 早期版本（[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）的现有 MDS Web 应用程序。 您不能选择现有 Web 应用程序，而是必须为 MDS 创建一个 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 应用程序。 否则，在您尝试将 Web 应用程序与升级的 MDS 数据库关联时，您会收到错误，指出无法访问请求的页面，因为该页的相关配置数据无效。  
        >   
        >  如果您要为 MDS Web 应用程序使用与现有（[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]）Web 应用程序相同的名字（别名），您必须首先从 IIS 中删除该 Web 应用程序和关联的应用程序池，然后使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版 Master Data Services 配置管理器创建同名的 Web 应用程序。 有关从 IIS 删除 Web 应用程序和应用程序池的信息，请参阅 [删除应用程序 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) 和 [删除应用程序池 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538)。  
  
5.  现在将新 Web 应用程序与已升级的 MDS 数据库关联。  
  
    1.  在 **“将应用程序与数据库相关联”** 部分中，单击 **“选择”**。  
  
    2.  选择 MDS 数据库。  
  
    3.  单击“应用”  。  
  
## <a name="troubleshooting"></a>故障排除  
 **问题：** 打开[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web 应用程序时，将显示 "客户端版本与数据库版本不兼容" 错误消息。  
  
 **解决方案：** 当[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]主数据管理器 web 应用程序尝试访问已升级到[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Master Data Services 的数据库时，会出现此问题。 您必须改用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 应用程序。  
  
 如果您在升级 MDS 数据库架构时没有在 IIS 中停止并重新启动 **“MDS 应用程序池”** ，则也可能出现此问题。 重新启动 **“MDS 应用程序池”** 可解决此问题。  
  
## <a name="see-also"></a>另请参阅  
 [安装 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
