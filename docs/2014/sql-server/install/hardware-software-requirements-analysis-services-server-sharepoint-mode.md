---
title: SharePoint 模式下 Analysis Services 服务器的硬件和软件要求（SQL Server 2014） |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 8f645ca9bdb6176505a6277af0f0482be5b62f09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245614"
---
# <a name="hardware-and-software-requirements-for-analysis-services-server-in-sharepoint-mode-sql-server-2014"></a>SharePoint 模式下的 Analysis Services 服务器的硬件和软件要求 (SQL Server 2014)


  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 支持 SharePoint 2010 和 SharePoint 2013。 尽管 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 可以在 SharePoint 服务器上安装，但是它在 SharePoint 场外部运行。 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 在 SharePoint 2010 场中的应用程序服务器上运行，并且使用 SharePoint 功能和基础结构来支持服务器操作。 要安装用于任一版本的 SharePoint 的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，请使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导。 安装后完成以下操作：  
  
- 运行该 SharePoint 版本的合适 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 配置工具版本。  
  
- 对于 SharePoint 2013，请安装[&#40;SharePoint 2013&#41;上的 "安装" 或 "卸载 PowerPivot for SharePoint 外接程序](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)"。  

##  <a name="bkmk_sqleditions"></a>SQL Server 版要求  
 并不是所有的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本中都提供了商业智能功能。 有关详细信息，请参阅[SQL Server 2014 的版本支持的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)和[SQL Server 2014 的版本和组件](../editions-and-components-of-sql-server-2016.md)。  
  
 [Microsoft SQL Server 2014 发行说明](https://go.microsoft.com/fwlink/?LinkID=296445)中可找到当前发行说明。  
  

  
##  <a name="bkmk_sqllicense"></a>SQL Server 许可  
 有关 SQL Server 许可的详细信息，请参阅以下内容：  
  
-   [SQL Server 2014 许可数据表](https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf)（https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf)。  
  
-   [如何购买： SQL Server 许可模式支持](https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2)（https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2)。  
  
##  <a name="bkmk_ssas__sharepoint_2013"></a>在 SharePoint 2013 上安装 Analysis Services  
 如果您在单独服务器上在 SharePoint 模式下安装 Analysis Services 服务器，则最低系统要求将基于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，而不是 SharePoint Server 要求。  
  
 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 最好运行在提供更高 RAM 阈值和更强处理能力的新一代商业服务器上。 使用大量 RAM 在内存中存储 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据。 该 RAM 支持根据结构变化进行调整的能力。 额外的处理器支持对原始未聚合的数据进行长时间运行的扫描。 数据假定其结构处于动态环境中，以便响应通过 Excel 客户端或前端接口启动的用户驱动的数据分析。  
  
> [!TIP]  
>  
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 使用 L2 和 L3 缓存。 若要改进性能，请考虑使用包含更大的 L2 和 L3 缓存的处理器。  
  
 下表介绍独立 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 服务器（不是 SharePoint 场的一部分）的最低硬件配置和建议的硬件配置：  
  
|组件|最小值|建议|  
|---------------|-------------|-----------------|  
|处理器|64 位双核处理器，3 千兆赫 (GHz)。|16 内核|  
|RAM|8 GB RAM|64 GB RAM|  
|存储|80 GB 存储空间|80 GB 或更大|  
  
 如果您在 SharePoint 场服务器上在 SharePoint 模式下安装 Analysis Services 服务器，则请查看以下链接中针对 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 SharePoint Server 的最低系统要求：  
  
-   [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [SharePoint 2013 的硬件和软件要求](https://technet.microsoft.com/library/cc262485\(office.15\).aspx)。  
  
 标准 SharePoint 2013 硬件和软件建议针对的是用于工作组或团队的基于 Web 的文档管理解决方案。 因为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 处理涉及大量数据，所以，仅当整个工作负荷较小（例如小于 100 个用户或工作簿）时该标准建议才足够。 更大的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 部署将要求更高的计算能力。  
  
##  <a name="bkmk_ssas__sharepoint_2010"></a>Analysis Services 安装在 SharePoint 2010 服务器上  
 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 在 SharePoint 2010 场中的应用程序服务器上运行，并且使用 SharePoint 功能和基础结构来支持服务器操作。 下表汇总了与 SharePoint 2010 部署有关的要求：  
  
|组件|要求|  
|---------------|-----------------|  
|SharePoint 版本|在同一个服务器场中配置的 SharePoint 2010 Enterprise 以及 Excel Services、安全存储区服务和 Claims to Windows Token Service。<br /><br /> 必须使用 SharePoint 安装程序中的“服务器场”选项安装 SharePoint（不支持 SharePoint 的“独立安装”选项）。 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 需要服务器场基础结构以便支持管理访问和数据访问。 独立安装不提供这些服务。<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务器安装不支持在 windows 7 或 windows Vista 上运行的 developer edition。|  
|Service Pack|要求使用 SharePoint Server 2010 Service Pack 1 (SP1)。<br /><br /> 必须有 SharePoint 2010 Service Pack 1 才能使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 功能。<br /><br /> 从 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 的以前版本升级到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 时，需要 SharePoint 2010 的 2010 年 8 月累积更新或更高版本。 在安装 SharePoint Service Pack 1 后，应安装 2010 年 8 月累积更新或更高版本。 的新安装[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]不需要累积更新。 有关详细信息，请参阅[8 月2010版 SharePoint 累积更新已发布](https://blogs.technet.com/b/stefan_gossner/archive/2010/09/02/august-2010-cumulative-update-for-sharepoint-has-been-released.aspx)。|  
|SharePoint Web 应用程序|
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2010 仅支持为经典模式身份验证配置的 SharePoint Web 应用程序。 如果您在向现有场中添加 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，则请确保您计划与其一起使用的 Web 应用程序是为经典模式身份验证配置的。 有关如何检查身份验证模式的说明，请参阅将[PowerPivot 解决方案部署到 SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)中的 "验证 Web 应用程序是否使用经典模式身份验证" 部分。|  
|
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器端数据刷新所需的数据访问接口|服务器端数据刷新重复用于最初导入数据的相同数据检索步骤。 这意味着，用于导入客户端工作站上的数据的数据访问接口还必须在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 服务器上存在。<br /><br /> 此外，使用 SharePoint 服务器上的数据馈送要求您具有 ADO.NET Data Services。 SharePoint Prerequisite Installer 程序不为您安装此软件。 必须手动安装以下软件。<br /><br /> ADO.NET Data Services 3.5 SP1 运行时程序集，用于将 SharePoint 列表导出为数据馈送。 下载并安装与您的操作系统匹配的版本：<br /><br /> 对于 Windows Server 2008 R2，使用适用[于 windows 7 和 Windows server 2008 R2 .NET Framework 3.5 SP1 的 ADO.NET Data Services 更新](https://www.microsoft.com/download/details.aspx?id=2343)。 Windows Server 2008 R2 **SP1**已经包含更新的提供程序。<br /><br /> 对于 Windows Server 2008，使用适用[于 windows 2000、Windows server 2003、WINDOWS XP、Windows Vista 和 Windows server 2008https://go.microsoft.com/fwlink/?LinkId=158125).NET Framework 3.5 SP1 的 ADO.NET Data Services 更新](https://www.microsoft.com/download/details.aspx?id=22734)。|  
  
 [确定硬件和软件要求（SharePoint 2010）（https://go.microsoft.com/fwlink/?LinkId=169734)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
## <a name="additional-information"></a>其他信息  

