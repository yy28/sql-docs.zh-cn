---
title: 比较 Analysis Services 表格和多维模型 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d36c20e0278a90bc5afcbd312afea2cb596e9c51
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072535"
---
# <a name="comparing-tabular-and-multidimensional-solutions"></a>比较表格和多维解决方案
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  SQL Server Analysis Services 提供几种方法来创建商业智能语义模型：表格、 多维和 Power Pivot for SharePoint。
  
 可以使用多种方法来实现针对不同业务和用户需求量身定制的建模体验。 “多维”是建立在开放标准基础之上的成熟技术，已由 BI 软件的众多供应商采用，但难以驾驭。 “表格”提供一种关系建模方法，很多开发人员认为它更加直观。 PowerPivot 更简单，它在 Excel 中提供可视化数据建模，并通过 SharePoint 提供服务器支持。  
  
 所有模型将部署为在 Analysis Services 实例上运行的数据库，可以使用一套数据提供程序通过客户端工具来访问，并通过 Excel、Reporting Services、Power BI 和其他供应商的 BI 工具在交互式静态报告中可视化。  
  
 表格和多维解决方案使用 SSDT 构建，旨在用于上独立运行的公司 BI 项目[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例在本地和表格模型中，对于[Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/)中的服务器云。 这两个解决方案将生成可与 BI 客户端轻松集成的高性能分析数据库。 然而，每个解决方案在创建、使用和部署方式上都存在不同。 本主题的大部分内容比较了这两种类型，以方便你找到适当的方法。  
  
 对于新项目，我们通常建议表格模型。 表格模型是更快地设计、 测试和部署;并将更好地与最新自助式 BI 应用程序和云的 Microsoft 服务。  
  
##  <a name="bkmk_overview"></a> 建模类型概述  
 是 Analysis Services 的新用户？ 下表列举了不同的模型，汇总了方法，并标识了初始发行载体。  
 
 > [!NOTE]  
>  **Azure Analysis Services**支持 1200年及更高版本的兼容性级别的表格模型。 但是，Azure Analysis Services 中支持本主题中所述的不是所有表格建模功能。 尽管创建和部署到 Azure Analysis Services 表格模型是大致相同它与在本地一样，务必了解的差异。 若要了解详细信息，请参阅[Azure Analysis Services 是什么？](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)
  
||||  
|-|-|-|  
|**类型**|**建模说明**|**已发布**|  
|表格|关系建模构造（模型、表、列）。 在内部，元数据继承自 OLAP 建模构造（多维数据集、维度、度量值）。 代码和脚本使用 OLAP 元数据。|SQL Server 2012 和更高版本（兼容级别 1050 - 1103） <sup>1</sup>|  
|SQL Server 2016 中的表格|关系建模构造 （模型、 表、 列） 在表格元数据中的对象定义中清楚表述[表格模型脚本语言 (TMSL)](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)并[表格对象模型 (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)代码。|SQL Server 2016（兼容级别 1200）| 
|SQL Server 2017 中的表格|关系建模构造 （模型、 表、 列） 在表格元数据中的对象定义中清楚表述[表格模型脚本语言 (TMSL)](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)并[表格对象模型 (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)代码。|SQL Server 2017 （兼容性级别 1400年）| 
|多维|OLAP 建模构造（多维数据集、维度、度量值）。|SQL Server 2000 和更高版本|  
|Power Pivot|最初是一个外接程序，但现已完全集成到 Excel。 仅限基于内部表格基础结构的可视建模。 你可以将 Power Pivot 模型导入 SSDT，以创建在 Analysis Services 实例上运行的新表格模型。|通过 Excel 和 Power Pivot BI Desktop|  
  
 <sup>1</sup>兼容性级别非常重要，因为表格元数据引擎以及对方案启用支持的当前版本中仅在更高级别可用的功能。 更高版本支持更低的兼容性级别，但建议创建新的模型或将现有模型升级到的服务器版本支持的最高兼容性级别。
  
##  <a name="bkmk_models"></a> 模型功能  
  下表总结了模型级别的功能可用性。 请查看此列表，以确保你想要使用的功能可在你打算生成的模型类型中使用。  
  
|||| 
|-|-|-|
||多维|表格|
|操作|用户帐户控制|否|
|Aggregations|用户帐户控制|否|
|计算列|否|用户帐户控制|  
|计算度量值|用户帐户控制|用户帐户控制| 
|计算表|否|是<sup>1</sup>|  
|自定义程序集|用户帐户控制|否|
|自定义汇总|用户帐户控制|否| 
|默认成员|用户帐户控制|否|  
|显示文件夹|用户帐户控制|是<sup>1</sup>|  
|Distinct Count|用户帐户控制|是（通过 DAX）|
|钻取|用户帐户控制|是 （取决于客户端应用程序）|
|层次结构|用户帐户控制|用户帐户控制|
|KPI|用户帐户控制|用户帐户控制| 
|链接对象|用户帐户控制|是（链接表）|
|M 表达式|否|是<sup>1</sup>|
|多对多关系|用户帐户控制|否 (但没有[双向交叉筛选器](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)1200年及更高版本的兼容性级别)| 
|命名集|用户帐户控制|否| 
|不规则层次结构|用户帐户控制|是<sup>1</sup>|  
|父子层次结构|用户帐户控制|是（通过 DAX）|
|“度量值组”|用户帐户控制|用户帐户控制| 
|透视|用户帐户控制|用户帐户控制|
|行级安全性|用户帐户控制|用户帐户控制| 
|对象级安全性|用户帐户控制|是<sup>1</sup>|
|半累加性度量值|用户帐户控制|用户帐户控制| 
|翻译|[是](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|用户帐户控制| 
|用户定义的层次结构|用户帐户控制|用户帐户控制|
|写回|用户帐户控制|否| 
  
 <sup>1</sup>请参阅[Analysis Services 中表格的兼容性级别模型](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)有关兼容性级别之间的功能差异的信息。  
  
##  <a name="bkmk_ds"></a> 数据注意事项  
 表格和多维模型使用从外部源导入的数据。 在确定哪种模型类型最适合你的数据时，需要导入的数据量和数据类型是一个主要考虑因素。  
  
 **压缩**  
  
 表格解决方案和多维解决方案都使用数据压缩，从而相对于您要从中导入数据的数据仓库来说，降低了 Analysis Services 数据库的大小。 因为实际压缩将基于基础数据的特性而有所不同，所以，无法精确了解在查询中处理和使用数据后解决方案将获取的磁盘和内存量。  
  
 许多 Analysis Services 开发人员都是这样估计的，多维数据库的主要存储量大约是原始数据大小的三分之一。 表格数据库有时可以获得更高的压缩率，大约是十分之一的大小，尤其在大多数数据都是从事实数据表导入时。  
  
 **模型和资源偏差大小（内存中或磁盘）**  
  
 Analysis Services 数据库的大小仅受可用于运行该数据库的资源的约束。 在数据库可增长到的大小方面，模型类型和存储模式也发挥了重要作用。  
  
 表格数据库在内存中运行，或者在 DirectQuery 模式下运行，这种模式可将查询执行卸载到外部数据库。 对于表格内存中分析，数据库完全在内存中，这意味着你必须拥有足够的内存不仅加载所有数据，但还创建以支持查询的其他数据结构存储。  
  
 DirectQuery，改进了 SQL Server 2016 中具有较少的限制比之前和更好的性能。 为存储和查询执行利用后端关系数据库能比以前更可靠地生成大规模表格模型。  
  
 从历史上看，在生产环境中的最大数据库是多维数据库，与每个针对其各自用途进行了优化的专用硬件上独立运行的处理和查询工作负荷。  表格数据库正在快速发展，DirectQuery 中的新改进功能将进一步弥补差距。  
  
 对于多维卸载数据存储和查询执行，可通过 ROLAP。   在查询服务器上可以缓存行集，过时的行集将被清除。对内存和磁盘资源的有效、平衡使用，使得客户更倾向于多维解决方案。  
  
 如果有一定的负荷压力，针对任一解决方案类型的磁盘和内存要求将随着 Analysis Services 缓存、存储、扫描和查询数据而提高。 有关内存分页选项的详细信息，请参阅 [Memory Properties](../analysis-services/server-properties/memory-properties.md)。 有关可伸缩性的详细信息，请参阅 [High availability and Scalability in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)。  
  
 Power Pivot for Excel 具有自定义的 2 GB 的文件大小限制，之所以施加这个限制是为了保证可以将在 Power Pivot for Excel 中创建的工作簿上载到 SharePoint，因为 SharePoint 针对上载文件大小设置了上限。 在独立 Analysis Services 实例上将 Power Pivot 工作簿迁移到表格解决方案的一个主要原因就是避开这个文件大小限制。 有关配置最大文件上传大小的详细信息，请参阅[配置最大文件上传大小 (PowerPivot for SharePoint)](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)。  
  
 **支持的数据源**  
  
 表格模型可以从关系数据源、数据馈送和某些文档格式导入数据。 此外可以使用 OLE DB for ODBC 与表格模型的提供程序。 在 1400年兼容级别表格模型有了显著提高在多个你可从中导入从数据源。 这是由于引入了新式获取数据查询和数据导入 SSDT 利用 M 公式查询语言中的功能。   

  多维解决方案可以使用 OLE DB 本机和托管访问接口从关系数据源导入数据。  
  
 若要查看可导入到各模型中的外部数据源的列表，请参阅以下主题：  
  
-   [支持的数据源](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  

-   [支持的数据源（SSAS - 多维）](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  

  
##  <a name="bkmk_lang"></a> 查询和脚本语言支持  
 Analysis Services 包括 MDX、DMX、DAX、XML/A、ASSL 和 TMSL。 对这些语言的支持根据模型类型的不同而异。 如果需要考虑查询和脚本语言要求，请查看以下列表。  

-   表格模型数据库支持 DAX 计算、DAX 查询和 MDX 查询。 在所有兼容级别都是如此。 脚本语言为 ASSL （基于 XMLA) 兼容级别 1050年-1103年和 TMSL （基于 XMLA) 兼容级别为 1200年及更高版本。 

-   PowerPivot 工作簿使用 DAX 进行计算，使用 DAX 或 MDX 进行查询。  
  
-   多维模型数据库支持 MDX 计算、 MDX 查询、 DAX 查询和 ASSL。 
  
-   数据挖掘模型支持 DMX 和 ASSL。  
  
-   表格和多维模型及数据库支持 Analysis Services PowerShell。  
  
 所有数据库都支持 XML/A。 有关详细信息，请参阅[查询和表达式语言参考 (Analysis Services)](http://msdn.microsoft.com/library/9597533d-35f4-4742-9d8c-7af392163527) 和 [Analysis Services 开发人员文档](../analysis-services/analysis-services-developer-documentation.md)。  
  
##  <a name="bkmk_sec"></a>安全功能  
 可在数据库级别保护所有 Analysis Services 解决方案。 更精细的安全选项会随模式的不同而不同。 如果解决方案需要精细的安全设置，则请查看以下列表以确保要生成的解决方案类型中支持所需的安全级别：  

  
-   表格模型数据库可使用行级别安全性，使用基于角色的权限。  
  
-   多维模型数据库可以使用维度和单元格级安全性，使用基于角色的权限。  

-   使用 SharePoint 权限在文件级别保护[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿。  
  
 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿可还原到表格模式服务器。 一旦还原文件，它是从 SharePoint，您可以使用所有表格建模功能，包括行级别安全性中分离。  
  
##  <a name="bkmk_designer"></a> 设计工具  
 对于需要生成分析模型的用户，数据建模技能和专业技术可能会大不相同。 如果您的解决方案需要考虑工具熟悉程度或用户专业技术，请比较以下模型创建体验。  
  
|建模工具|使用方法|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|用于创建表格、 多维和数据挖掘解决方案。 此创作环境使用 Visual Studio shell 来提供工作区、属性窗格和对象导航。 已使用 Visual Studio 的专业用户最可能愿意使用此工具生成商业智能应用程序。|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel|用于创建 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿，稍后你会将该工作簿部署到已安装 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 场中。 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel 包含一个在 Excel 上打开的单独应用程序工作区。 它使用与 Excel 相同的视觉表象（选项卡式页面、网格布局和公式栏）。 精通 Excel 的用户更愿意使用这种工具，而不是 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。|  
  
##  <a name="bkmk_client"></a> 客户端应用程序支持  
 在常规、 表格和多维解决方案支持使用一个或多个 Analysis Services 客户端库 （MSOLAP、 AMOMD、 ADOMD） 的客户端应用程序。 例如，Excel、 Power BI Desktop 和自定义应用程序。   
 
 如果您使用的是 Reporting Services，则报表功能的可用性会随版本和服务器模式的不同而不同。 为此，要生成的报表类型可能会影响您选择安装的服务器模式。  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]是在 SharePoint 中运行的一种 Reporting Services 创作工具，可用于在 SharePoint 2010 场中部署的报表服务器。 Analysis Services 表格模型数据库或 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿是能够与此报表一起使用的唯一数据源类型。 这意味着，你必须具有一台表格模式服务器或一台 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 服务器才能承载此类型的报表所用的数据源。 不能将多维模型用作 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 报表的数据源。 你必须创建 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] BI 语义模型连接或 Reporting Services 共享数据源，以便用作 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 报表的数据源。  
  
 报表生成器和报表设计器可以使用任何 Analysis Services 数据库，包括在 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 上承载的 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿。  
  
 所有 Analysis Services 数据库都支持 Excel 数据透视表。 虽然仅多维数据库支持写回，但不管你是使用表格数据库、多维数据库还是 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿，Excel 功能都相同。  
 
  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 实例管理](../analysis-services/instances/analysis-services-instance-management.md)   
 [Analysis Services 中的新增功能](../analysis-services/what-s-new-in-analysis-services.md)     

  
  
