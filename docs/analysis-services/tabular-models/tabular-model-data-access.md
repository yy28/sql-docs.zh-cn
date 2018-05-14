---
title: 表格模型数据访问 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13ce3f601774d5ffee5b19f0d3dec2dca141c8d8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="tabular-model-data-access"></a>表格模型数据访问
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Analysis Services 中的表格模型数据库可由用于检索多维模型中的数据或元数据的大多数相同的客户端、接口和语言访问。 有关详细信息，请参阅[多维模型数据访问（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)。  
  
 本文介绍客户端、 查询语言和适用于表格模型的编程接口。  
  
## <a name="clients"></a>客户端  
 以下 Microsoft 客户端应用程序支持本机连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格模型数据库。  
  
### <a name="power-bi"></a>Power BI
可从 [Power BI](https://powerbi.microsoft.com/)连接到本地 Analysis Services 表格模型数据库。 Power BI 是一套业务分析工具，用于分析数据和共享见解。 

### <a name="excel"></a>Excel  
 您可以从 Excel 连接表格模型数据库，使用 Excel 中的数据可视化和分析功能来处理数据。 若要访问数据，您需要定义 Analysis Services 数据连接，指定以表格服务器模式运行的服务器，然后选择要使用的数据库。 有关详细信息，请参阅 [连接到 SQL Server Analysis Services 或从其中导入数据](http://go.microsoft.com/fwlink/?linkID=215150)。  
  
 Excel 也是推荐用于在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中浏览表格模型的应用程序。 该工具包括一个 **“在 Excel 中分析”** 选项，可用来启动新的 Excel 实例，创建 Excel 工作簿并打开从该工作簿到模型工作区数据库的数据连接。 在 Excel 中浏览表格模型数据时，要注意 Excel 使用 Excel PivotTable 客户端对该模型发出查询。 相应地，Excel 工作簿中的操作会生成将发送到工作区数据库的 MDX 查询而非 DAX 查询。 如果您在使用 SQL Profiler 或其他监视工具来监视查询，则应能在事件探查器跟踪中看到 MDX 而不是 DAX。 有关在 Excel 功能中分析的详细信息，请参阅[在 Excel 中的分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)。  
  
### <a name="power-view"></a>Power View  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 是一个在 SharePoint 2010 环境中运行的 Reporting Services 报表客户端应用程序。 它将数据浏览、查询设计和演示布局融合为集成的特别报表体验。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 可以将表格模型用作数据源，无论该模型是承载于在表格模式下运行的 Analysis Services 实例中，还是使用 DirectQuery 模式从关系数据存储区中检索到的。 若要在 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]中连接到表格模型，您必须创建包含服务器位置和数据库名称的连接文件。 您可以在 SharePoint 中创建 Reporting Services 共享数据源或 BI 语义模型连接文件。 有关 BI 语义模型连接的详细信息，请参阅 [PowerPivot BI 语义模型连接 (bism)](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)。  
  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 客户端通过向指定的数据源发送请求来确定指定模型的结构，这将返回一个架构，客户端可使用此架构来创建针对作为数据源的模型的查询并执行基于数据的操作。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 用户界面中用于筛选数据、执行计算或聚合以及显示关联数据的后续操作由客户端控制且不能以编程方式来执行这些操作。  
  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 客户端向模型发送的查询会作为 DAX 语句发出，您可以在模型上设置跟踪来进行监视。  客户端还向服务器发出了有关初始架构定义的请求，该定义将根据概念性架构定义语言 (CSDL) 呈现。 有关详细信息，请参阅 [用于商业智能的 CSDL 批注 (CSDLBI)](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 管理承载表格模型的实例并查询这些实例中的元数据和数据。 可以处理模型或模型中的对象、创建和管理分区以及设置用于管理数据访问的安全性。 有关详细信息，请参阅以下主题：  
  
-   [确定 Analysis Services 实例的服务器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
-   [连接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
-   [监视 Analysis Services 实例](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
 可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中同时使用 MDX 查询窗口和 XMLA 查询窗口来从表格模型数据库检索数据和元数据。 但是，请注意下列限制：  
  
-   已在 DirectQuery 模式下部署的模型不支持使用 MDX 和 DMX 的语句；因此，如果您需要创建针对 DirectQuery 模式下的表格模型的查询，则应改用 **“XMLA 查询”** 窗口。  
  
-   打开 **“查询”** 窗口后，无法更改 XMLA 查询窗口的数据库上下文。 因此，如果您需要向其他数据库或其他实例发送查询，则必须使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 打开该数据库或实例，并在该上下文中打开新的 **“XMLA 查询”** 窗口。  
  
 可以创建针对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格模型的跟踪，就像对多维解决方案执行此操作一样。 在此版本中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了许多新事件，可用于跟踪内存使用率、查询和处理操作以及文件使用率。 有关详细信息，请参阅 [Analysis Services 跟踪事件](../../analysis-services/trace-events/analysis-services-trace-events.md)。  
  
> [!WARNING]  
>  如果对表格模型数据库进行跟踪，则可能会显示一些归类为 DMX 查询的事件。 但是，表格模型数据不支持数据挖掘，并且数据库上执行的 DMX 查询仅适用于模型元数据的 SELECT 语句。 这些事件仅归类为 DMX，因为 MDX 使用的是相同的分析器框架。  
  
## <a name="query-languages"></a>查询语言  
 Analysis Services 表格模型支持为访问多维模型而提供的大多数相同的查询语言。 已在 DirectQuery 模式下部署的表格模型属于例外情况，该模型不从 Analysis Services 数据存储检索数据，而是直接从 SQL Server 数据源检索数据。 无法使用 MDX 查询这些模型，但必须使用支持从 DAX 表达式到 Transact-SQL 语句的转换的客户端，如 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 客户端。  
  
### <a name="dax"></a>DAX  
 可以使用 DAX 在所有类型的表格模型中创建表达式和公式，无论该模型是作为已启用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]的 Excel 工作簿存储在 SharePoint 上，还是存储在 Analysis Services 实例上。  
  
 此外，您可以在 XMLA EXECUTE 命令语句的上下文中使用 DAX 表达式来向已在 DirectQuery 模式下部署的表格模型发送查询。  
  
 有关使用 DAX 的表格模型查询的示例，请参阅 [DAX 查询语法参考](http://msdn.microsoft.com/en-us/4dd0cf0e-191d-411d-987c-f606813fc39e)。  
  
### <a name="mdx"></a>MDX  
 可以使用 MDX 创建针对将内存中缓存用作首选查询方法的表格模型（即，尚未在 DirectQuery 模式下部署的模型）的查询。 虽然 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 等客户端会使用 DAX 来创建聚合并将模型作为数据源进行查询，但如果熟悉 MDX，则可在 MDX 中快速创建示例查询，请参阅 [在 MDX 中生成度量值](../../analysis-services/multidimensional-models/mdx/mdx-building-measures.md)。  
  
### <a name="csdl"></a>CSDL  
 虽然概念性架构定义语言本身并不是查询语言，但可使用它检索有关模型和模型元数据的信息，然后可使用这些信息来创建报告或创建针对模型的查询。  
  
 有关如何在表格模型中使用 CSDL 的信息，请参阅 [用于商业智能的 CSDL 批注 (CSDLBI)](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)。  
  
## <a name="programmatic-interfaces"></a>编程接口  
 用于与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格模型进行交互的主要接口为架构行集、XMLA 以及由 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]提供的查询客户端和查询工具。  
  
### <a name="data-and-metadata"></a>数据和元数据  
 可以使用 ADOMD.NET 从托管应用程序中的表格模型检索数据和元数据。 
  
-   [使用动态管理视图 & #40; Dmv & #41;监视 Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
 可以在非托管客户端应用程序中使用 Analysis Services 9.0 OLE DB 访问接口以支持对表格模型的 OLE DB 访问。 启用表格模型访问需要更新版本的 Analysis Services OLE DB 访问接口。 有关用于表格模型的提供程序的详细信息，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859) 。  
  
 还可以直接从 Analysis Services 实例以基于 XML 的格式检索数据。 可以使用 DISCOVER_CSDL_METADATA 行集来检索表格模型的架构，也可以将 EXECUTE 或 DISCOVER 命令与现有 ASSL 元素、对象或属性一起使用。 如需詳細資訊，請參閱下列資源：  
  
-   [用于商业智能的 CSDL 批注 (CSDLBI)](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
### <a name="manipulate-analysis-services-objects"></a>操作 Analysis Services 对象  
 可以使用 XMLA 命令或使用 AMO 来创建、修改、删除和处理表格模型及其对象（包括表、列、透视、度量值和分区）。 已同时更新 AMO 和 XMLA 以支持表格模型中用于增强报告和建模的其他属性。  
  
  
### <a name="schema-rowsets"></a>架构行集  
 客户端应用程序可使用架构行集来检查表格模型的元数据并从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器中检索支持和监视信息。 此版本的 SQL Server 中不仅添加了新的架构行集，并且现有架构行集得到了扩展以支持与表格模型相关的功能并增强 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的监视与性能分析。  
  
-   [DISCOVER_CALC_DEPENDENCY 行集](../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)  
  
     用于跟踪表格模型中列和参考之间的依赖关系的新架构行集。  
  
-   [DISCOVER_CSDL_METADATA 行集](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)  
  
     用于获取表格模型的 CSDL 表示形式的新架构行集。  
  
-   [DISCOVER_XEVENT_TRACE_DEFINITION 行集](http://msdn.microsoft.com/library/e1ce2d2d-f994-4318-801a-ee0385aecd84)  
  
     用于监视 SQL Server 扩展事件的新架构行集。 有关详细信息，请参阅 [使用 SQL Server 扩展事件监视 Analysis Services](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)。  
  
-   [DISCOVER_TRACES 行集](../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)  
  
     可使用新 **Type** 列按类别筛选跟踪。 有关详细信息，请参阅[为重播创建事件探查器跟踪 (Analysis Services)](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)。  
  
-   [MDSCHEMA_HIERARCHIES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)  
  
     新的 **STRUCTURE_TYPE** 枚举支持在表格模型中创建的用户定义的层次结构的标识。 有关详细信息，请参阅[层次结构](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)。  
  
 此版本中不包含针对 OLE DB for Data Mining 架构行集的更新。  
  
> [!WARNING]  
>  您无法在已在 DirectQuery 模式下部署的数据库中使用 MDX 或 DMX 查询；因此，如果您需要对使用架构行集的 DirectQuery 模型执行查询，则您应使用 XMLA 而非关联的 DMV。 对于将服务器的结果作为一个整体返回的 DMV（例如，SELECT * from $system.DBSCHEMA_CATALOGS 或 DISCOVER_TRACES），您可以对在缓存模式下部署的数据库内容执行查询。  
  
## <a name="see-also"></a>另请参阅  
 [连接到表格模型数据库 ](../../analysis-services/tabular-models/connect-to-a-tabular-model-database-ssas.md)   
 [Power Pivot 数据访问](../../analysis-services/power-pivot-sharepoint/power-pivot-data-access.md)   
 [连接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
