---
title: "比较表格和多维解决方案 (SSAS) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 49
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 47
---
# 比较表格和多维解决方案 (SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供多种不同的方法来创建商业智能语义模型：多维、表格和 PowerPivot。  
  
 可以使用多种方法来实现针对不同业务和用户需求量身定制的建模体验。 “多维”是建立在开放标准基础之上的成熟技术，已由 BI 软件的众多供应商采用，但难以驾驭。 “表格”提供一种关系建模方法，很多开发人员认为它更加直观。 PowerPivot 更简单，它在 Excel 中提供可视化数据建模，并通过 SharePoint 提供服务器支持。  
  
 所有模型将部署为在 Analysis Services 实例上运行的数据库，可以使用一套数据提供程序通过客户端工具来访问，并通过 Excel、Reporting Services、Power BI 和其他供应商的 BI 工具在交互式静态报告中可视化。  
  
 由于内存体系结构和元数据的差异，模型类型都不可换用，不过，你可以很轻松地从表格 1050-1103 模型升级到表格 1200，并可以导入 Power Pivot，以表格项目的形式创建一个全新的模型。  
  
 表格和多维解决方案是使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 生成的，旨在用于在独立 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例上运行的公司 BI 项目。 这两个解决方案将生成可与 BI 客户端轻松集成的高性能分析数据库。 然而，每个解决方案在创建、使用和部署方式上都存在不同。 本主题的大部分内容比较了这两种类型，以方便你找到适当的方法。  
  
 对于新开发项目，我们通常建议使用表格。 它的设计、测试和部署速度将更快，并且将更好地与来自 Microsoft 的最新自助式 BI 应用程序与云服务一起使用。  
  
##  <a name="a-namebkmkoverviewa-overview-of-modeling-types"></a><a name="bkmk_overview"></a>建模类型概述  
 是 Analysis Services 的新用户？ 下表列举了不同的模型，汇总了方法，并标识了初始发行载体。  
  
||||  
|-|-|-|  
|**类型**|**建模说明**|**已发布**|  
|多维|OLAP 建模构造（多维数据集、维度、度量值）。|SQL Server 2000 和更高版本|  
|表格|关系建模构造（模型、表、列）。<br /><br /> 在内部，元数据继承自 OLAP 建模构造（多维数据集、维度、度量值）。 代码和脚本使用 OLAP 元数据。|SQL Server 2012 和更高版本（兼容级别 1050 - 1103）<sup>1</sup>|  
|SQL Server 2016 中的表格|关系建模构造（模型、表、列），在脚本和代码中的表格元数据对象定义内指定。|SQL Server 2016（兼容级别 1200）|  
|Power Pivot|最初是一个外接程序，但现已完全集成到 Excel。 仅限基于内部表格基础结构的可视建模。 你可以将 Power Pivot 模型导入 SSDT，以创建在 Analysis Services 实例上运行的新表格模型。|通过 Excel 和 Power Pivot BI Desktop|  
  
 <sup>1</sup> SQL Server 2012 中引入的兼容级别非常重要，因为新的表格元数据引擎以及对方案启用功能的支持只在更高级别提供。 值得注意的改进包括 DirectQuery、脚本和可编程性。 有关详细信息，请参阅 [What's New in Analysis Services](../analysis-services/what-s-new-in-analysis-services.md) 。  
  
##  <a name="a-namebkmkmodelsa-model-features"></a><a name="bkmk_models"></a>模型功能  
  下表总结了模型级别的功能可用性。 请查看此列表，以确保你想要使用的功能可在你打算生成的模型类型中使用。  
  
|||||  
|-|-|-|-|  
||多维|表格|Power Pivot|  
|操作|是|是|“否”|  
|Aggregations|是|是|“否”|  
|计算列|“否”|用户帐户控制|是|  
|计算度量值|是|用户帐户控制|是|  
|计算表|是|是<sup>1</sup>|是|  
|自定义程序集|是|是|“否”|  
|自定义汇总|是|是|“否”|  
|默认成员|是|是|“否”|  
|显示文件夹|是|是<sup>1</sup>|是|  
|Distinct Count|是|是（通过 DAX）|是（通过 DAX）|  
|钻取|是|是（在单独的工作表中打开详细信息）|是|  
|层次结构|是|用户帐户控制|是|  
|KPI|是|用户帐户控制|是|  
|链接对象|是|是（链接表）|“否”|  
|多对多关系|是|否（但在 1200 兼容级别提供[双向交叉筛选器](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)）|“否”|  
|命名集|是|是|“否”|  
|父子层次结构|是|是（通过 DAX）|是（通过 DAX）|  
|分区|是|用户帐户控制|是|  
|透视|是|用户帐户控制|是|  
|半累加性度量值|是|用户帐户控制|是|  
|翻译|[是](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|是|[是](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)|  
|用户定义的层次结构|是|用户帐户控制|是|  
|写回|是|是|“否”|  
  
 <sup>1</sup> 有关表格段中功能差异的信息，请参阅 [Analysis Services 中表格模型的兼容级别](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。  
  
##  <a name="a-namebkmkdsa-data-considerations"></a><a name="bkmk_ds"></a>数据注意事项  
 表格和多维模型使用从外部源导入的数据。 在确定哪种模型类型最适合你的数据时，需要导入的数据量和数据类型是一个主要考虑因素。  
  
 **压缩**  
  
 表格解决方案和多维解决方案都使用数据压缩，从而相对于你要从中导入数据的数据仓库来说，降低了 Analysis Services 数据库的大小。 因为实际压缩将基于基础数据的特性而有所不同，所以，无法精确了解在查询中处理和使用数据后解决方案将获取的磁盘和内存量。  
  
 许多 Analysis Services 开发人员都是这样估计的，多维数据库的主要存储量大约是原始数据大小的三分之一。 表格数据库有时可以获得更高的压缩率，大约是十分之一的大小，尤其在大多数数据都是从事实数据表导入时。  
  
 **模型和资源偏差大小（内存中或磁盘）**  
  
 Analysis Services 数据库的大小仅受可用于运行该数据库的资源的约束。 在数据库可增长到的大小方面，模型类型和存储模式也发挥了重要作用。  
  
 表格数据库在内存中运行，或者在 DirectQuery 模式下运行，这种模式可将查询执行卸载到外部数据库。 对于表格内存中分析，数据库完全存储在内存中，这意味着，你必须提供足够的内存，以便不仅能够加载所有数据，而且还能创建更多的数据结构来支持查询。  
  
 DirectQuery 已在此版本中经过改进，其限制比以前更少，并且提高了性能。 为存储和查询执行利用后端关系数据库能比以前更可靠地生成大规模表格模型。  
  
 一直以来，生产环境中的最大 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库是多维数据库，其处理和查询工作负载在专用的硬件上独立运行，并且每个工作负载已针对其各自用途进行优化。  表格数据库正在快速发展，DirectQuery 中的新改进功能将进一步弥补差距。  
  
 对于多维数据库，可通过 ROLAP 来卸载数据存储和查询执行。   在查询服务器上可以缓存行集，过时的行集将被清除。 对内存和磁盘资源的有效、平衡使用，使得客户更倾向于多维解决方案。  
  
 如果有一定的负荷压力，针对任一解决方案类型的磁盘和内存要求将随着 Analysis Services 缓存、存储、扫描和查询数据而提高。 有关内存分页选项的详细信息，请参阅 [Memory Properties](../analysis-services/server-properties/memory-properties.md)。 有关可伸缩性的详细信息，请参阅 [High availability and Scalability in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)。  
  
 Power Pivot for Excel 具有自定义的 2 GB 的文件大小限制，之所以施加这个限制是为了保证可以将在 Power Pivot for Excel 中创建的工作簿上载到 SharePoint，因为 SharePoint 针对上载文件大小设置了上限。 在独立 Analysis Services 实例上将 Power Pivot 工作簿迁移到表格解决方案的一个主要原因就是避开这个文件大小限制。 有关配置最大文件上传大小的详细信息，请参阅[配置最大文件上传大小 (PowerPivot for SharePoint)](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)。  
  
 **支持的数据源**  
  
 多维解决方案可以使用 OLE DB 本机和托管访问接口从关系数据源导入数据。  
  
 表格模型可以从关系数据源、数据馈送和某些文档格式导入数据。 还可以将 OLE DB for ODBC 提供程序用于表格模型。  
  
 若要查看可导入到各模型中的外部数据源的列表，请参阅以下主题：  
  
-   [支持的数据源（SSAS - 多维）](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
-   [支持的数据源（SSAS 表格）](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
##  <a name="a-namebkmklanga-query-and-scripting-language-support"></a><a name="bkmk_lang"></a>查询和脚本语言支持  
 Analysis Services 包括 MDX、DMX、DAX、XML/A、ASSL 和 TMSL。 对这些语言的支持根据模型类型的不同而异。 如果需要考虑查询和脚本语言要求，请查看以下列表。  
  
-   PowerPivot 工作簿使用 DAX 进行计算，使用 DAX 或 MDX 进行查询。  
  
-   表格模型数据库支持 DAX 计算、DAX 查询和 MDX 查询。 在所有兼容级别都是如此。 脚本语言在兼容级别 1050-1103 为 ASSL（基于 XMLA），在兼容级别 1200 为 TMSL（基于 XMLA）。  
  
-   多维模型数据库支持 MDX 计算和 MDX 查询以及 ASSL。  
  
-   数据挖掘模型支持 DMX 和 ASSL。  
  
-   表格和多维模型及数据库支持 Analysis Services PowerShell。  
  
 所有数据库都支持 XML/A。 有关详细信息，请参阅[查询和表达式语言参考 (Analysis Services)](../Topic/Query%20and%20Expression%20Language%20Reference%20\(Analysis%20Services\).md) 和 [Analysis Services 开发人员文档](../analysis-services/analysis-services-developer-documentation.md)。  
  
##  <a name="a-namebkmkseca-security-features"></a><a name="bkmk_sec"></a>安全功能  
 可在数据库级别保护所有 Analysis Services 解决方案。 更精细的安全选项会随模式的不同而不同。 如果解决方案需要精细的安全设置，则请查看以下列表以确保要生成的解决方案类型中支持所需的安全级别。  
  
-   使用 SharePoint 权限在文件级别保护 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿。  
  
-   通过使用 Analysis Services 中基于角色的权限，表格模型数据库可使用行级别安全性。  
  
-   通过使用 Analysis Services 中基于角色的权限，多维模型数据库可使用维度和单元格级别安全性。  
  
 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿可还原到表格模式服务器。 一旦还原文件，它就会从 SharePoint 中分离，从而允许你使用所有表格建模功能（包括行级别安全性）。  
  
##  <a name="a-namebkmkdesignera-design-tools"></a><a name="bkmk_designer"></a>设计工具  
 对于需要生成分析模型的用户，数据建模技能和专业技术可能会大不相同。 如果您的解决方案需要考虑工具熟悉程度或用户专业技术，请比较以下模型创建体验。  
  
|建模工具|使用方法|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|用于创建表格、多维和数据挖掘解决方案。 此创作环境使用 Visual Studio shell 来提供工作区、属性窗格和对象导航。 已使用 Visual Studio 的专业用户最可能愿意使用此工具生成商业智能应用程序。|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel|用于创建 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿，稍后你会将该工作簿部署到已安装 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 场中。 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel 包含一个在 Excel 上打开的单独应用程序工作区。 它使用与 Excel 相同的视觉表象（选项卡式页面、网格布局和公式栏）。 精通 Excel 的用户更愿意使用这种工具，而不是 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。|  
  
##  <a name="a-namebkmkclienta-client-application-support"></a><a name="bkmk_client"></a>客户端应用程序支持  
 如果您使用的是 Reporting Services，则报表功能的可用性会随版本和服务器模式的不同而不同。 为此，要生成的报表类型可能会影响您选择安装的服务器模式。  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 是在 SharePoint 中运行的一种 Reporting Services 创作工具，可用于在 SharePoint 2010 场中部署的报表服务器。 Analysis Services 表格模型数据库或 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿是能够与此报表一起使用的唯一数据源类型。 这意味着，你必须具有一台表格模式服务器或一台 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 服务器才能承载此类型的报表所用的数据源。 不能将多维模型用作 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 报表的数据源。 你必须创建 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] BI 语义模型连接或 Reporting Services 共享数据源，以便用作 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 报表的数据源。  
  
 报表生成器和报表设计器可以使用任何 Analysis Services 数据库，包括在 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 上承载的 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿。  
  
 所有 Analysis Services 数据库都支持 Excel 数据透视表。 虽然仅多维数据库支持写回，但不管你是使用表格数据库、多维数据库还是 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿，Excel 功能都相同。  
  
 PerformancePoint 面板可连接到所有 Analysis Services 数据库（包括 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿）。 有关详细信息，请参阅 [创建数据连接 (PerformancePoint Services)](http://go.microsoft.com/fwlink/?linkdID=218155)。  
  
##  <a name="a-namebkmkdeploymentmodea-server-deployment-modes-for-multidimensional-and-tabular-solutions"></a><a name="bkmk_deploymentmode"></a>针对多维和表格解决方案的服务器部署模式  
 Analysis Services 实例是在用于设置服务器的操作上下文的三种模式中的某种模式下安装的。 安装的服务器模式将确定可部署到该服务器的解决方案的类型。 这三种模式间的主要差异在于存储和内存体系结构，但也存在其他差异。 下表简要描述了三种服务器模式。 有关详细信息，请参阅[确定 Analysis Services 实例的服务器模式](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)。  
  
|部署模式|说明|  
|---------------------|-----------------|  
|0 - 多维和数据挖掘|运行部署到 Analysis Services 的默认实例的多维和数据挖掘解决方案。 部署模式 0 是针对 Analysis Services 安装的默认值。|  
|1 - [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint|对于 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 数据访问，Analysis Services 是 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 安装的一个内部组件。 Analysis Services 安装在部署模式 1 中，并且由 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 服务专用于 SharePoint 环境中。|  
|2 - 表格|在为部署模式 2 配置的 Analysis Services 独立实例上运行表格解决方案。|  
  
 有关详细信息，请参阅[安装 Analysis Services](../analysis-services/instances/install-windows/install-analysis-services.md)。  
  
##  <a name="a-namebkmksharepointa-sharepoint-requirements"></a><a name="bkmk_sharePoint"></a>SharePoint 要求  
 SQL Server 通过添加对 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 数据访问和表格数据访问的支持与 SharePoint 服务器相集成。 在 SharePoint 和 SQL Server 集成中的投资将随着您增加各产品中使用的功能的数目而增长。 如果你具有 SharePoint，则可以安装 SQL Server [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 以便实现 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 数据访问以及获取 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] .bism 连接文件，这些文件用于访问在网络服务器的外部 Analysis Services 实例上运行的表格数据库。  
  
 Power View 报告（使用 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 和表格数据库作为数据源）既是 SQL Server 提供的一项 SharePoint 功能，也是 Excel 的一项内置功能。 尽管表格数据库运行在 SharePoint 之外的 Analysis Services 实例上，但这些数据是由在 SharePoint 中运行的 Power View 报表使用的。  
  
 如果你未使用 SharePoint，仍可以使用 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel 创建 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿，但不会具有整体的数据可视化体验。 使用该工作簿的每个人都必须在 Excel 中使用 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel 外接程序来下载和查看各工作簿，以便使用切片器、筛选器和数据透视表来进行数据交互和浏览。 否则，工作簿可视化将仅限于在您打开工作簿时出现的静态数据。  
  
 表格、多维和数据挖掘解决方案运行在网络中的 Analysis Services 实例上，不依赖于 SharePoint。  
  
##  <a name="a-namebkmkexta-programmability-and-extensibility-support"></a><a name="bkmk_ext"></a>可编程性和扩展性支持  
 尽管对 Power BI 提供开发人员支持，但不对 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿提供开发人员支持。 如果你使用的是 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿，则必须将内置客户端和服务器应用程序用作你解决方案的一部分。 Excel 编程和 SharePoint 编程是唯一的选项。  
  
 有关 Power BI 的信息，请参阅 [Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/)。  
  
 表格解决方案仅支持每个解决方案一个 model.bim 文件，这意味着所有工作都必须在单个文件中完成。 已经习惯于在单个解决方案中使用多个项目的开发团队可能需要在构建共享的表格解决方案时改变其工作的方式。  
  
 位于兼容级别 1200 的表格解决方案将映射到使用表格元数据的新对象模型。 旧版表格模型和所有多维模型使用多维元数据作为描述符。 我们建议将旧版表格模型升级到 1200 兼容级别，以便为自定义代码和脚本使用 AMO 中的表格命名空间。  
  
 有关详细信息，请参阅 [Analysis Services 开发人员文档](https://msdn.microsoft.com/library/bb500153.aspx) 。  
  
##  <a name="a-namebkmknexta-next-step-build-a-solution"></a><a name="bkmk_Next"></a>下一步：构建解决方案  
 现在，您已经基本了解了如何比较解决方案，请试试下面的教程，学习创建各解决方案的步骤。 您可以访问下面的链接，它们链接到用于说明这些步骤的教程。  
  
-   生成 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 模型。 请参阅 [Microsoft Excel 中的 Power Pivot 入门](https://support.office.com/article/Get-started-with-Power-Pivot-in-Microsoft-Excel-fdfcf944-7876-424a-8437-1a6c1043a80b)。  
  
-   生成表格模型。 请参阅[表格建模（Adventure Works 教程）](../analysis-services/tabular-modeling-adventure-works-tutorial.md)。  
  
-   生成多维模型。 请参阅[多维建模（Adventure Works 教程）](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)。  
  
-   生成数据挖掘模型。 请参阅[数据挖掘基础教程](../Topic/Basic%20Data%20Mining%20Tutorial.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 实例管理](../analysis-services/instances/analysis-services-instance-management.md)   
 [Analysis Services 中的新增功能](../analysis-services/what-s-new-in-analysis-services.md)     
 [PowerPivot 中的新增功能](http://go.microsoft.com/fwlink/?LinkId=238141)   
 [PowerPivot BI 语义模型连接 (.bism)](../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [创建和管理共享数据源（SharePoint 集成模式下的 Reporting Services）](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md)  
  
  