---
title: 创建多维模型使用 SQL Server Data Tools (SSDT) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, environments
- Analysis Services, development
- SQL Server Analysis Services, environments
- projects [Analysis Services]
- solutions [Analysis Services]
ms.assetid: 132ed779-3ec8-4734-9698-802116d1b017
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 915ce0ebc6ff9ecd68647deb1653bfab0e1c956d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076171"
---
# <a name="creating-multidimensional-models-using-sql-server-data-tools-ssdt"></a>使用 SQL Server Data Tools 创建多维模型 (SSDT)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了两个不同的环境以生成、部署和管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 解决方案： [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 这两个环境都可实现项目系统。 有关 Visual Studio 项目的详细信息，请参阅 MSDN Library 中的 [作为容器的项目](https://go.microsoft.com/fwlink/?LinkId=63960) 。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 是一种基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2010 的开发环境，用于创建和修改商业智能解决方案。 使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，可以创建包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象（多维数据集、维度等）定义的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，这些定义存储在包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 元素的 XML 文件内。 这些项目包含在还可含有来自其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件（包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]）的项目的解决方案中。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，可以开发 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，作为独立于任意特定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的解决方案的一部分。 您可以向测试服务器的实例部署对象，以便在开发期间进行测试，然后再使用同一个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，向一个或多个临时服务器或生产服务器实例部署对象。 包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的解决方案中的项目和项可以与源代码管理（如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual SourceSafe）集成。 有关使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目的详细信息，请参阅 [创建 Analysis Services 项目 (SSDT)](create-an-analysis-services-project-ssdt.md)。 您还可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 直接连接到现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例以创建和修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象，而无需使用项目，也无需在 XML 文件中存储对象定义。 有关详细信息，请参阅 [多维模型数据库 (SSAS)](multidimensional-model-databases-ssas.md)和 [在联机模式下连接到 Analysis Services 数据库](connect-in-online-mode-to-an-analysis-services-database.md)。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 是一个管理环境，主要用于管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的实例。 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，可以管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象（执行备份、处理等），还可以使用 XMLA 脚本直接在现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上创建新对象。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了 Analysis Server 脚本项目，在该项目中可开发和保存以多维表达式 (MDX)、数据挖掘扩展插件 (DMX) 和 XML for Analysis (XMLA) 编写的脚本。 通常，Analysis Server 脚本项目可用于在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上执行管理任务或重新创建对象（例如数据库和多维数据集）。 这些项目可作为解决方案的一部分进行保存，并可与源代码管理控件相集成。 有关使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中创建 Analysis Server 脚本项目的详细信息，请参阅 [SQL Server Management Studio 中的 Analysis Services 脚本项目](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md)。  
  
## <a name="introducing-solutions-projects-and-items"></a>解决方案、项目和项简介  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 均提供了项目，并且这些项目都纳入了各自的解决方案。 一个解决方案可以包含多个项目，而一个项目通常又包含多个项。 创建项目时会自动生成一个新的解决方案，您可以根据需要向现有解决方案中添加其他项目。 项目包含的对象取决于项目类型。 每个项目容器中的项保存为文件系统中的项目文件夹中的文件。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 包含以下商业智能项目。  
  
|项目|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目|包含单个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的对象定义。 有关如何创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的详细信息，请参阅 [创建 Analysis Services 项目 (SSDT)](create-an-analysis-services-project-ssdt.md)。|  
|导入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 2008 数据库|提供一个向导，您可以使用该向导，通过从现有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库导入对象定义，来创建一个新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目|包含一组 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的对象定义。 有关详细信息，请参阅 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)。|  
|报表项目向导|提供一个向导，引导您完成使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]创建报表项目的过程。 有关详细信息，请参阅 [Reporting Services (SSRS)](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)。|  
|报表模型项目|包含 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表模型的对象定义。 有关详细信息，请参阅 [Reporting Services (SSRS)](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)。|  
|报表服务器项目|包含一个或多个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表的对象定义。 有关详细信息，请参阅 [Reporting Services (SSRS)](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)。|  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 还包含多个侧重于各种查询或脚本的项目类型，如下表所示。  
  
|项目|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的 DMX、MDX 和 XMLA 脚本，以及与可执行这些脚本的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例之间的连接。 有关详细信息，请参阅 [SQL Server Management Studio 中的 Analysis Services 脚本项目](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md)。|  
|SQL Server Compact 脚本|包含 SQL Server Compact 的 SQL 脚本，以及与对其执行这些脚本的 SQL Server Compact 实例之间的连接。|  
|SQL Server 脚本|包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 实例的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 XQuery 脚本，以及与对其执行这些脚本的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例之间的连接。 有关详细信息，请参阅 [SQL Server Database Engine](../../database-engine/sql-server-database-engine-overview.md)。|  
  
 有关解决方案和项目的详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .NET 文档或 MSDN Library 中的“管理解决方案、项目和文件”。  
  
## <a name="choosing-between-sql-server-management-studio-and-sql-server-data-tools"></a>在 SQL Server Management Studio 和 SQL Server Data Tools 之间进行选择  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 是为管理和配置 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的现有对象而设计的。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 是为开发商业智能解决方案（包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的功能）而设计的。  
  
 下面是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]之间的一些差异。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一个集成环境，用于连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的实例，以配置和管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例中的对象。 通过使用脚本，还可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建或修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象本身，但是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 没有提供用于对象设计和定义的图形界面。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供了一个集成开发环境，用于开发商业智能解决方案。 你可以在项目模式下使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，它使用项目和解决方案中包含的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 对象的基于 XML 的定义。 在项目模式下使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 意味着在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中对 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 对象的更改即为对这些基于 XML 的对象定义的更改，并且在部署解决方案之前，不会直接应用到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上的对象。 还可以在联机模式下使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，这意味着直接连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例并使用现有数据库中的对象。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 增强了商业智能应用程序的开发，因为你可以在源代码管理的多用户环境中处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，而不需要与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例建立活动连接。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供对用于查询和测试的现有对象的直接访问，并可用于更快速地实现以前已编写脚本的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。 但是，将项目部署到生产环境后，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]数据库及其对象时必须谨慎。 避免覆盖以下更改：直接对现有数据库中的对象所做的更改，以及对最初生成部署解决方案的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目所做的更改。 有关详细信息，请参阅 [在开发阶段使用 Analysis Services 项目和数据库](work-with-analysis-services-projects-and-databases-in-development.md)和 [在生产环境中使用 Analysis Services 项目和数据库](work-with-analysis-services-projects-and-databases-in-production.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [创建 Analysis Services 项目 (SSDT)](create-an-analysis-services-project-ssdt.md)  
  
-   [配置 Analysis Services 项目属性 (SSDT)](configure-analysis-services-project-properties-ssdt.md)  
  
-   [生成 Analysis Services 项目 (SSDT)](build-analysis-services-projects-ssdt.md)  
  
-   [部署 Analysis Services 项目 (SSDT)](deploy-analysis-services-projects-ssdt.md)  
  
-   [在开发阶段使用 Analysis Services 项目和数据库](work-with-analysis-services-projects-and-databases-in-development.md)  
  
-   [在生产环境中使用 Analysis Services 项目和数据库](work-with-analysis-services-projects-and-databases-in-production.md)  
  
## <a name="see-also"></a>请参阅  
 [创建 Analysis Services 项目 (SSDT)](create-an-analysis-services-project-ssdt.md)   
 [SQL Server Management Studio 中的 Analysis Services 脚本项目](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md)   
 [多维模型数据库 (SSAS)](multidimensional-model-databases-ssas.md)  
  
  
