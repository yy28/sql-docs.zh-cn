---
title: 比较表格和多维解决方案 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 498cba5d7ccb4e97de13d9cb46e58351547d9b75
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680817"
---
# <a name="comparing-tabular-and-multidimensional-solutions-ssas"></a>比较表格和多维解决方案 (SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 为数据建模提供两种不同方法：表格和多维。 虽然它们之间有明显的重叠现象，但也有重要的差异，你可以通过差异决定如何继续。 在本主题中，我们提供功能比较，并解释每种方法如何满足常见项目要求。 例如，如果对特定数据源的支持是最重要的因素，则有关数据源的部分有助于指导您决定采用哪种建模方法。  
  
 本主题包含以下各节：  
  
-   [Analysis Services 中的建模概述](#bkmk_overview)  
  
-   [支持的解决方案类型的数据源](#bkmk_ds)  
  
-   [模型功能](#bkmk_models)  
  
-   [模型大小](#bkmk_modelsize)  
  
-   [可编程性和开发人员体验](#bkmk_ext)  
  
-   [查询和脚本语言支持](#bkmk_lang)  
  
-   [安全功能支持](#bkmk_sec)  
  
-   [设计工具](#bkmk_designer)  
  
-   [客户端和报告应用程序](#bkmk_client)  
  
-   [承载平台](#bkmk_sharePoint)  
  
-   [针对多维和表格解决方案的服务器部署模式](#bkmk_deploymentmode)  
  
-   [下一步：构建解决方案](#bkmk_Next)  
  
 可以在 MSDN 上的此技术文章中找到更多信息：[在 SQL Server 2012 Analysis Services 中选择表格或多维建模体验](https://go.microsoft.com/fwlink/?LinkId=251588)。  
  
##  <a name="bkmk_overview"></a> Analysis Services 中的建模概述  
 Analysis Services 通过在 Analysis Services 实例上承载的数据库提供模型的开发体验以及模型部署。 模型类型包括表格和多维。 正如你所料，数据库承载支持你所创建的表格和多维解决方案，但数据库承载还包括 PowerPivot for SharePoint。  
  
 PowerPivot for SharePoint 是 *在 SharePoint 模式下的 Analysis Services*，其中 Analysis Services 作为 SharePoint 的辅助服务运行，帮助承载和管理以前在 Excel 中创建并随后保存到 SharePoint 的 Excel 数据模型。 在此上下文中，Analysis Services 的作用是将数据模型加载到内存，刷新来自外部数据源的数据并执行针对模型的查询。 在此配置中，Analysis Services 在后台进行操作。 所有连接和对 Analysis Services 的请求都是通过 SharePoint 完成的，并且仅在 Excel 工作簿包含数据模型（数据模型在 Excel 工作簿中为可选）时。 如果生成数据模型在 Excel 中，并将其托管在 SharePoint 中，符合你的项目要求，请参阅[Power Pivot:功能强大的数据分析和在 Excel 中的数据建模](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b)并[PowerPivot for SharePoint &#40;SSAS&#41; ](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)有关详细信息。  
  
> [!NOTE]  
>  Excel 数据模型和表格模型在体系结构上类似。 如果需要支持更大量的数据或使用在 Excel 中不可用的其他模型功能，则可以将 Excel 数据模型导入到表格模型。  
  
 表格和多维解决方案是使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 生成的，旨在用于在独立 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例上运行的公司 BI 项目。 这两种解决方案都生成高性能的分析数据库，这些分析数据库可轻松地与 Excel、Reporting Services 报表以及来自 Microsoft 的其他 BI 应用程序和第三方应用程序相集成。 这两种解决方案都会产生可供支持 Analysis Services 的任何客户端应用程序使用的独立数据库。  
  
 在高级别中，表格和多维模型之间的差异具有如下特征：  
  
-   多维和数据挖掘解决方案使用 OLAP 建模构造（多维数据集和维度），而 MOLAP、ROLAP 或 HOLAP 存储则使用磁盘作为预聚合数据的主数据存储。  
  
-   表格解决方案使用关系建模构造（如表和关系）来对数据进行建模，并且使用内存中分析引擎来存储和计算数据。 大多数（如果不是全部）模型都会存储在 RAM 中，并且通常速度比与之对应的多维更快。  
  
 对于新项目，请首先考虑表格方法。 它的设计、测试和部署速度将更快，并且将更好地与来自 Microsoft 的最新自助式 BI 应用程序一起使用。  
  
##  <a name="bkmk_ds"></a> 支持的解决方案类型的数据源  
 多维和表格模型使用从外部源导入的数据。 大多数开发人员使用数据仓库（旨在支持报告数据结构）作为模型背后的主数据源。 数据仓库通常基于星型或雪花型架构，SSIS 用于将数据从 OLTP 解决方案加载到数据仓库。 使用数据仓库作为后端数据源时，建模会更简单。  
  
|**链接**|**支持的选项的摘要**|  
|--------------|--------------------------------------|  
|[支持的数据源&#40;SSAS 多维&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)|多维模型使用来自关系数据源的数据。|  
|[支持的数据源（SSAS 表格）](tabular-models/data-sources-supported-ssas-tabular.md)|表格模型支持更广泛的数据源，包括平面文件、数据馈送和通过 ODBC 数据提供程序访问的数据源。|  
  
 这两种建模方法都可以使用来自同一模型中的多个数据源的数据。  
  
 如果你的解决方案需要在关系数据库（尤其是要求大型数据时使用的技术）中的模型之外存储模型数据，则数据源类型必须是 SQL Server 关系数据库。 多维模型的两种 ROLAP 存储和表格模型的 DirectQuery 都有此要求。  
  
 **数据大小**  
  
 表格解决方案和多维解决方案都使用数据压缩，从而相对于您要从中导入数据的数据仓库来说，降低了 Analysis Services 数据库的大小。 因为实际压缩将基于基础数据的特性而有所不同，所以，无法精确了解在查询中处理和使用数据后解决方案将获取的磁盘和内存量。 许多 Analysis Services 开发人员都是这样估计的，多维数据库的主要存储量大约是原始数据大小的三分之一。  
  
 表格数据库有时可以获得更高的压缩率，大约是十分之一的大小，尤其在大多数数据都是从事实数据表导入时。 对于表格数据库，由于将表格数据库加载到内存时创建的附加数据结构，内存需求通常将大于磁盘上的数据大小。 如果有一定的负荷压力，针对任一解决方案类型的磁盘和内存要求将随着 Analysis Services 缓存、存储、扫描和查询数据而提高。  
  
 对于某些项目，数据要求可能会比较高，从而成为选择模型类型时要考虑的一个因素。 如果您需要加载的数据大小会高达 TB 级，则在可用缓存无法容纳这些数据的情况下，表格解决方案可能无法满足您的要求。 尽管存在将内存中数据交换到磁盘上的分页选项，但非常大量的数据更适合用于多维解决方案中。 当今生产中使用的最大的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库是多维数据库。 有关针对表格解决方案的内存分页选项的详细信息，请参阅 [Memory Properties](server-properties/memory-properties.md)。 有关扩展多维解决方案的详细信息，请参阅 [针对具有只读数据库的 Analysis Services 的扩展查询](https://go.microsoft.com/fwlink/?LinkId=251711)。  
  
##  <a name="bkmk_models"></a> 模型功能  
 下表总结了模型级别的功能可用性。 如果您已安装 Analysis Services，则可通过此信息来了解您安装的服务器模式的功能。 如果您已熟悉 Analysis Services 中的模型功能并且您的业务需求包含其中的一个或多个功能，则可查看此列表以确保要使用的功能在计划生成的模型类型中可用。  
  
 有关如何按建模方法来比较功能的详细信息，请参阅 MSDN 上的技术文章 [在 SQL Server 2012 Analysis Services 中选择表格或多维建模的经验](https://go.microsoft.com/fwlink/?LinkId=251588) 。  
  
> [!NOTE]  
>  在特定版本的 SQL Server 中支持表格建模。 有关详细信息，请参阅 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
||||  
|-|-|-|  
||**多维**|**表格**|  
|操作|[是](multidimensional-models/actions-in-multidimensional-models.md)|否|  
|Aggregation 对象|[是](multidimensional-models/designing-aggregations-analysis-services-multidimensional.md)|否|  
|计算度量值|[是](multidimensional-models/create-calculated-members.md)|是|  
|自定义程序集|[是](multidimensional-models/multidimensional-model-assemblies-management.md)|否|  
|自定义汇总|是|否|  
|Distinct Count|[是](multidimensional-models/use-aggregate-functions.md)|是 （通过 DAX) *|  
|钻取|[是](multidimensional-models/actions-in-multidimensional-models.md)|是|  
|层次结构|[是](multidimensional-models/user-defined-hierarchies-create.md)|是|  
|KPI|[是](multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|是|  
|链接度量值组|[是](multidimensional-models/linked-measure-groups.md)|否|  
|多对多关系|[是](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)|否|  
|父子层次结构|[是](multidimensional-models/parent-child-dimension.md)|是（通过 DAX）|  
|“度量值组”|[是](tabular-models/partitions-ssas-tabular.md)|  
|透视|[是](multidimensional-models/perspectives-in-multidimensional-models.md)|[是](tabular-models/partitions-ssas-tabular.md)|  
|半累加性度量值|[是](multidimensional-models/define-semiadditive-behavior.md)|是（通过 DAX）|  
|翻译|[是](multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|否|  
|用户定义的层次结构|[是](multidimensional-models/user-defined-hierarchies-create.md)|是|  
|写回|[是](multidimensional-models/set-partition-writeback.md)|否|  
  
 * 如果你的解决方案必须支持非常大量的非重复计数 （例如，数以百万计的客户 Id），请首先考虑表格。 表格在此方案中往往具有更高的性能。 请参阅有关在白皮书中，非重复计数部分[Analysis Services 案例研究：在大型商业解决方案中使用表格模型](https://msdn.microsoft.com/library/dn751533.aspx)。  
  
##  <a name="bkmk_modelsize"></a> 模型大小  
 就对象的总数而言，模型大小不依解决方案类型而定。 但是，用来生成各解决方案的设计工具在其适应处理大量对象的程度上有所不同。 更大的模型有时候在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中构建会更容易，因为它提供更多的功能以便在对象资源管理器和解决方案资源管理器中按类型描绘和列出对象。  
  
 由数以百计的表格或维度构成的非常大的模型往往在 Visual Studio 中（而不是在设计工具中）以编程方式生成。 最大数量的模型中的对象的详细信息，请参阅[最大容量规范&#40;Analysis Services&#41;](multidimensional-models/olap-physical/maximum-capacity-specifications-analysis-services.md)。  
  
##  <a name="bkmk_ext"></a> 可编程性和开发人员体验  
 对于表格和多维模型，将为这两种模式共享一个对象模型。 AMO 和 ADOMD.NET 都支持这两种模式。 没有针对表格构造修正客户端库，因此，您将需要理解多维和表格构造以及命名约定彼此之间的关系。 作为第一步，查看 AMO 到表格编程示例，了解针对表格模型的 AMO 编程。 有关详细信息，请从 [codeplex 网站](https://go.microsoft.com/fwlink/?LinkID=221036)下载示例。  
  
 表格解决方案仅支持每个解决方案一个 model.bim 文件，这意味着所有工作都必须在单个文件中完成。 已经习惯于在单个解决方案中使用多个项目的开发团队可能需要在构建共享的表格解决方案时改变其工作的方式。  
  
##  <a name="bkmk_lang"></a> 查询和脚本语言支持  
 Analysis Services 包括 MDX、DMX、DAX、XML/A 和 ASSL。 对这些语言的支持会随模型类型的不同而略微不同。 如果需要考虑查询和脚本语言要求，请查看以下列表。  
  
-   表格模型数据库支持 DAX 计算、DAX 查询和 MDX 查询。  
  
-   多维模型数据库支持 MDX 计算和 MDX 查询以及 ASSL。  
  
-   数据挖掘模型支持 DMX 和 ASSL。  
  
-   Analysis Services PowerShell 支持服务器和数据库管理。 模型类型（或服务器模式）不是使用 PowerShell cmdlet 的一个因素。  
  
 所有数据库都支持 XML/A。  
  
##  <a name="bkmk_sec"></a> 安全功能支持  
 可在数据库级别保护所有 Analysis Services 解决方案。 更精细的安全选项会随模式的不同而不同。 如果解决方案需要精细的安全设置，则请查看以下列表以确保要生成的解决方案类型中支持所需的安全级别：  
  
-   通过使用 Analysis Services 中基于角色的权限，表格模型数据库可使用行级别安全性。  
  
-   通过使用 Analysis Services 中基于角色的权限，多维模型数据库可使用维度和单元格级别安全性。  
  
 Excel 数据模型可以还原到表格模式服务器。 一旦还原文件，它就会从 SharePoint（假设你从 SharePoint 位置还原）中分离，从而允许你使用几乎所有表格建模功能（包括行级别安全性）。 您不能对已还原工作簿使用的一个表格建模功能是链接表。  
  
##  <a name="bkmk_designer"></a> 设计工具  
 对于需要生成分析模型的用户，数据建模技能和专业技术可能会大不相同。 如果您的解决方案需要考虑工具熟悉程度或用户专业技术，请比较以下模型创建体验。  
  
|**建模工具**|**如何使用**|  
|-----------------------|------------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|用于创建表格、多维和数据挖掘解决方案。 此创作环境使用 Visual Studio shell 来提供工作区、属性窗格和对象导航。 已使用 Visual Studio 的专业用户最可能愿意使用此工具生成商业智能应用程序。 有关详细信息，请参阅 [Tools and applications used in Analysis Services](tools-and-applications-used-in-analysis-services.md) 。|  
|Excel 2013 和更高版本，带 Power Pivot for Excel 外接程序|Power Pivot for Excel 是用于编辑和增强 Excel 数据模型的工具。 它有一个单独的应用程序工作区，可通过 Excel 打开，但使用与 Excel 相同的视觉表象（选项卡式的页面、网格布局和公式栏）。 精通 Excel 的用户更愿意使用这种工具，而不是 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。 请参阅[Power Pivot:功能强大的数据分析和在 Excel 中的数据建模](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b)。|  
  
##  <a name="bkmk_client"></a> 客户端和报告应用程序  
 在早期版本中，你选择的模型类型将影响你可以使用的客户端应用程序，但随着时间的推移，这些区别已经消失。 对于连接到 Analysis Services 数据的客户端应用程序，表格和多维提供同样的支持。 下表是可与 Analysis Services 数据模型一起使用的 Microsoft 客户端应用程序的列表。  
  
|**应用程序**|**说明**|  
|---------------------|---------------------|  
|Excel 数据透视表|虽然仅多维支持写回功能（一种 Excel 实现的 Analysis Services 功能），但对于表格和多维模型而言，Excel 功能都是相同的。|  
|Reporting Services RDL 报表|在报表生成器或报表设计器中创建的 RDL 报表，可以使用任何 Analysis Services 模型以及在 PowerPivot for SharePoint 上承载的 Excel 数据模型。|  
|PerformancePoint 面板|在 SharePoint 中，PerformancePoint 仪表板可以连接到所有 Analysis Services 数据库，包括 Excel 数据模型。 有关详细信息，请参阅 [创建数据连接 (PerformancePoint Services)](https://go.microsoft.com/fwlink/?linkdID=218155)。|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 在 Office 365 或 Power BI 网站中|仅限表格模型。|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 在本地 SharePoint 中|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]，作为来自 SharePoint 的 ClickOnce 应用程序，可以使用 Analysis Services 多维数据集或表格模型。|  
  
##  <a name="bkmk_deploymentmode"></a> 针对多维和表格解决方案的服务器部署模式  
 Analysis Services 实例是在用于设置服务器的操作上下文的三种模式中的某种模式下安装的。 安装的服务器模式将确定可部署到该服务器的解决方案的类型。 这三种模式间的主要差异在于存储和内存体系结构，但也存在其他差异。 下表简要描述了三种服务器模式。 有关详细信息，请参阅[确定 Analysis Services 实例的服务器模式](instances/determine-the-server-mode-of-an-analysis-services-instance.md)。  
  
|部署模式|Description|  
|---------------------|-----------------|  
|0 - 多维和数据挖掘|运行部署到 Analysis Services 的默认实例的多维和数据挖掘解决方案。 部署模式 0 是针对 Analysis Services 安装的默认值。 有关详细信息，请参阅 [Install Analysis Services in Multidimensional and Data Mining Mode](../../2014/sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)。|  
|1 - PowerPivot for SharePoint|对于 Excel 数据模型访问，Analysis Services 是 SharePoint 的一个内部组件。 Analysis Services 安装在部署模式 1 中，并且只接受来自 SharePoint 环境中 Excel Services 的请求。 有关详细信息，请参阅 [PowerPivot for SharePoint 2010 Installation](../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)。|  
|2 - 表格|在为部署模式 2 配置的 Analysis Services 独立实例上运行表格解决方案。 有关详细信息，请参阅 [Install Analysis Services in Tabular Mode](instances/install-windows/install-analysis-services.md)。|  
  
 请注意，服务器模型不能互换。 安装时，需要为服务器操作选择一个模式。 应安装多个实例（每个对应一个服务器模式），以支持所有的工作负载。  
  
##  <a name="bkmk_sharePoint"></a> 承载平台  
 Microsoft 提供多种用于承载数据、应用程序、报表和协作的方法。 在此部分中，我们将介绍 Analysis Services 针对每个承载平台的互操作性。  
  
|**平台**|**说明**|  
|------------------|---------------------|  
|Microsoft Azure|你可以在 Azure 虚拟机上运行任何 Analysis Services 支持的版本。 对比 Azure SQL 数据库（Azure 中一种提供许多与本地关系数据库引擎相同功能的服务），Azure 上没有任何等效的 Analysis Services。 在 Azure VM 中安装、配置和运行是我们唯一基于 Azure 的选项。|  
|Office 365|Office 365 中 Excel 联机支持在本地运行的对表格和多维模型的远程连接。|  
|Office 365 中的 Power BI 网站|在 Power BI 网站中，Power View 报表可以连接到在本地运行的表格数据模型。|  
|本地服务器（SharePoint 和 SQL Server 实例）|本地数据库服务器（即已安装了 Analysis Services 的 SQL Server 实例）仍然是使 Analysis Services 数据对报表和客户端应用程序可用的主要方式。 表格、多维和数据挖掘解决方案运行在网络中的 Analysis Services 实例上，不依赖于 SharePoint。<br /><br /> SQL Server 通过添加对 PowerPivot 数据访问和表格数据访问的支持与 SharePoint 服务器相集成。 在 SharePoint 和 SQL Server 集成中的投资将随着您增加各产品中使用的功能的数目而增长。 如果您具有 SharePoint，则可以安装 SQL Server PowerPivot for SharePoint 以便实现 PowerPivot 数据访问以及获取 PowerPivot .bism 连接文件，这些文件用于访问在网络服务器的外部 Analysis Services 实例上运行的表格数据库。<br /><br /> 如果你同时具有 SharePoint 和 SQL Server，则可以支持以下服务和应用程序的组合：<br /><br /> Analysis Services 模型（表格或多维）<br /><br /> 中间层 SharePoint 服务（Excel Services、SharePoint 中的 Reporting Services 或 PerformancePoint services）<br /><br /> 用于深入数据分析和探索的浏览器客户端或富客户端 (Excel)。|  
  
##  <a name="bkmk_Next"></a> 下一步：构建解决方案  
 现在，您已经基本了解了如何比较解决方案，请试试下面的教程，学习创建各解决方案的步骤。 您可以访问下面的链接，它们链接到用于说明这些步骤的教程。  
  
-   使用[表格建模（Adventure Works 教程）](tabular-modeling-adventure-works-tutorial.md)生成表格模型。  
  
-   使用[多维建模（Adventure Works 教程）](multidimensional-modeling-adventure-works-tutorial.md)生成多维模型。  
  
-   使用 [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md)构建数据挖掘模型。  
  
-   使用 [PowerPivot for Excel 教程](https://go.microsoft.com/fwlink/?LinkId=251135)构建 PowerPivot 模型。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 实例管理](instances/analysis-services-instance-management.md)   
 [什么是 Analysis Services 和 Business Intelligence 中的新增功能](what-s-new-in-analysis-services.md)   
 [新增功能&#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)   
 [什么是 PowerPivot 中的新增功能](https://go.microsoft.com/fwlink/?LinkId=238141)   
 [SQL Server 2012 的 PowerPivot 帮助](https://go.microsoft.com/fwlink/?LinkID=220946)   
 [PowerPivot BI 语义模型连接&#40;.bism&#41;](power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [创建和管理共享数据源（SharePoint 集成模式下的 Reporting Services）](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
  
