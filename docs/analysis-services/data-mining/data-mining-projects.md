---
title: 数据挖掘项目 |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e01ea2027e95d3bb6e2635e48488df6b471bf238
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-projects"></a>数据挖掘项目
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  数据挖掘项目是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 解决方案的一部分。 在设计过程中，在此项目中创建的对象作为工作区数据库的一部分可用于测试和查询。 当您希望用户能够查询或浏览此项目中的对象时，必须将此项目部署到在多维模型中运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
 本主题为您提供了理解和创建数据挖掘项目所需的基本信息。  
  
 [创建数据挖掘项目](#bkmk_Overview)  
  
 [数据挖掘项目中的对象](#bkmk_Objects)  
  
-   [数据源](#bkmk_DataSources)  
  
-   [数据源视图](#bkmk_DSV)  
  
-   [挖掘结构](#bkmk_Structures)  
  
-   [挖掘模型](#bkmk_Models)  
  
 [使用已完成的数据挖掘项目](#bkmk_Complete)  
  
-   [查看和浏览模型](#bkmk_ViewExplore)  
  
-   [测试和验证模型](#bkmk_Validate)  
  
-   [创建预测](#bkmk_Predict)  
  
 [以编程方式访问数据挖掘项目](#bkmk_API)  
  
##  <a name="bkmk_Overview"></a> 创建数据挖掘项目  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，使用模板 **“OLAP 和数据挖掘项目”**生成数据挖掘项目。 还可以使用 AMO 以编程方式创建数据挖掘项目。 可以使用 Analysis Services 脚本语言 (ASSL) 编写单个数据挖掘对象的脚本。 有关详细信息，请参阅[多维模型数据访问（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)。  
  
 如果在现有解决方案中创建数据挖掘项目，则默认情况下，数据挖掘对象将部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，并具有与解决方案文件相同的名称。 您可以使用 **“项目属性”** 对话框更改此名称和目标服务器。 有关详细信息，请参阅[配置 Analysis Services 项目属性 (SSDT)](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)。  
  
> [!WARNING]  
>  若要成功生成和部署您的项目，您必须对运行在 OLAP/数据挖掘模式下的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例具有访问权限。 无法在支持表格模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上开发或部署数据挖掘解决方案，也无法直接使用来自 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿或来自使用内存中数据存储区的表格模型的数据。 若要确定你具有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例是否可支持数据挖掘，请参阅 [确定 Analysis Services 实例的服务器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)。  
  
 在每个创建的数据挖掘项目中，您将执行以下步骤：  
  
1.  选中一个“数据源” （如多维数据集、数据库、甚至 Excel 或文本文件），该数据源包含要用于生成模型的原始数据。  
  
2.  在数据源中定义用于分析的数据子集，并将其保存为“数据源视图” 。  
  
3.  定义一个“挖掘结构”  以支持建模。  
  
4.  通过选中一种“算法”  并指定该算法如何处理数据来将“挖掘模型”  添加到挖掘结构中。  
  
5.  通过使用所选数据或筛选后的数据子集填充结构来定型模型。  
  
6.  浏览、测试和重新生成模型。  
  
 项目完成后，您可以对其进行部署以便用户浏览或查询，或提供对应用程序中挖掘模型的编程访问，以支持预测和分析。  
  
  
##  <a name="bkmk_Objects"></a> 数据挖掘项目中的对象  
 所有数据挖掘项目都包含以下四种对象类型。 您可以具有所有类型的多个对象。  
  
-   数据源  
  
-   数据源视图  
  
-   挖掘结构  
  
-   挖掘模型  
  
 例如，单个数据挖掘项目可包含对多个数据源的引用，每个数据源支持多个数据源视图。 反过来，每个数据源视图可以支持多个挖掘结构，每个挖掘结构具有多个相关的挖掘模型。  
  
 此外，您的项目可能包含插入算法、自定义程序集或自定义存储过程；但此处不介绍这些对象。 有关详细信息，请参阅 [Analysis Services 开发人员文档](../../analysis-services/analysis-services-developer-documentation.md)。  
  
  
###  <a name="bkmk_DataSources"></a> Data Sources  
 数据源定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器连接到此数据源时将使用的连接字符串和身份验证信息。 该数据源可以包含多个表格或视图；它可以如单个 Excel 工作簿或文本文件一样简单，也可以如联机分析处理 (OLAP) 数据库或大型关系数据库一样复杂。  
  
 单个数据挖掘项目可以引用多个数据源。 尽管一个挖掘模型一次只能使用一个数据源，但此项目可能具有多个在不同数据源上绘制的模型。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持来自多个外部提供程序的数据，并且 SQL Server 数据挖掘可以同时使用关系数据和多维数据集数据作为数据源。 但是，如果您开发了这两种项目类型（基于关系数据源的模型和基于 OLAP 多维数据集的模型），则您可能希望在单独的项目中进行开发并管理。  
  
-   通常，基于 OLAP 多维数据集的模型应在 OLAP 设计解决方案中进行开发。 一个原因是基于多维数据集的模型必须对多维数据集进行处理以便更新数据。 通常，仅当这是数据存储和数据访问的主要方法时或者需要多维项目创建的聚合、维度和属性时，才应使用多维数据集数据。  
  
-   如果您的项目仅使用关系数据，则应在单个项目中创建关系模型，否则需要重新处理其他对象。 在许多情况下，用于支持多维数据集创建的临时数据库或数据仓库已包含执行数据挖掘所需的视图，您可以使用这些视图进行数据挖掘，而不是使用多维数据集中的聚合和纬度。  
  
-   不能直接使用内存中数据或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据生成数据挖掘模型。  
  
 该数据源仅标识服务器或提供程序以及数据的一般类型。 如果您需要更改数据格式和聚合，请使用数据源视图对象。  
  
 若要控制处理数据源中的数据的方法，您可以添加派生列或计算、修改聚合或重命名数据源视图的数据中的列。 （还可以通过修改挖掘结构列，或使用挖掘模型列级别的建模标志和筛选器，以处理数据下游。）  
  
 如果需要数据清理，或必须修改数据仓库中的数据以创建其他变量、更改数据类型或创建备用聚合，则可能需要创建其他项目类型以支持数据挖掘。 有关相关项目的详细信息，请参阅 [数据挖掘解决方案的相关项目](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)。  
  
  
###  <a name="bkmk_DSV"></a> Data Source Views  
 定义数据源的此连接之后，可以创建标识与模型相关的特定数据的视图。  
  
 利用数据源视图，还可以自定义向挖掘模型提供数据源中的数据的方式。 您可以修改数据结构，使其与项目的关系更密切，或者仅选择某些种类的数据。  
  
 例如，通过使用数据源视图编辑器，您可以：  
  
-   创建派生列，如日期部分、子字符串等。  
  
-   使用诸如 GROUP BY 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句来聚合值  
  
-   暂时限制数据或示例数据  
  
 有关如何修改数据源视图中数据的详细信息，请参阅 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
> [!WARNING]  
>  如果要筛选数据，则可以在数据源视图中执行此操作，但也可以在挖掘模型级别对数据创建筛选器。 因为筛选器定义存储在挖掘模型中，所以通过使用模型筛选器更便于确定用于对模型进行定型的数据。 此外，使用不同的筛选条件可以创建多个相关模型。 有关详细信息，请参阅[挖掘模型筛选器（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)。  
  
 请注意，您创建的数据源视图可能包含不直接用于分析的其他数据。 例如，您可能添加用于测试、预测或钻取的数据源视图数据。 有关这些用法的详细信息，请参阅[测试和验证（数据挖掘）](../../analysis-services/data-mining/testing-and-validation-data-mining.md)和[钻取](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
  
###  <a name="bkmk_Structures"></a> Mining Structures  
 一旦创建数据源和数据源视图，就必须通过在项目中定义“挖掘结构”  来选择与您的业务问题最相关的数据列。 挖掘结构指示项目实际应使用数据源视图中的哪些数据列来进行建模、定型和测试。  
  
 若要添加新的挖掘结构，请启动数据挖掘向导。 该向导自动定义挖掘结构，引导您完成选择数据的整个过程，并可选择性地将初始挖掘模型添加到该结构中。 在挖掘结构中，从数据源视图中或 OLAP 多维数据集中选择表格和列，并定义表格之间的关系（如果您的数据包含嵌套表）。  
  
 根据您使用的是关系数据源还是联机分析处理 (OLAP) 数据源，在数据挖掘向导中选择的数据将会有很大区别。  
  
-   当您选择关系数据源中的数据时，很容易设置一个挖掘结构：从数据源视图的数据中选择列，然后设置其他自定义项（如别名），或定义列中的值如何分组或分装。 有关详细信息，请参阅 [创建关系挖掘结构](../../analysis-services/data-mining/create-a-relational-mining-structure.md)。  
  
-   当您使用来自 OLAP 多维数据集的数据时，挖掘结构必须与 OLAP 解决方案在同一个数据库中。  若要创建挖掘结构，请从您的 OLAP 解决方案的维度和相关度量中选择属性。 数值通常位于度量中，类别变量位于维度中。 有关详细信息，请参阅 [创建 OLAP 挖掘结构](../../analysis-services/data-mining/create-an-olap-mining-structure.md)。  
  
-   还可以使用 DMX 来定义挖掘结构。 有关详细信息，请参阅[数据挖掘扩展插件 (DMX) 数据定义语句](../../dmx/dmx-statements-data-definition.md)。  
  
 在创建初始挖掘结构之后，可以复制、修改结构列并为其设置别名。  
  
 每个挖掘结构可以包含多个挖掘模型。 因此，在创建挖掘结构之后，您可以再次打开挖掘结构，并使用 [Data Mining Designer](../../analysis-services/data-mining/data-mining-designer.md) 将多个挖掘模型添加到结构中。  
  
 您还具有将数据分为定型数据集以便生成模型的选项，以及一个用来测试或验证挖掘模型的维持数据集。  
  
> [!WARNING]  
>  某些诸如时序模型的模型类型不支持创建维持数据集，因为它们需要连续的数据序列来进行定型。 有关详细信息，请参阅 [Training and Testing Data Sets](../../analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
  
###  <a name="bkmk_Models"></a> Mining Models  
 挖掘模型定义将用于数据的算法或分析方法。 您可以为每个挖掘结构添加一个或多个挖掘模型。  
  
 根据您的需要，可以在单个项目中合并多个模型，或者为每个模型类型或分析任务创建单个项目。  
  
 完成创建结构或模型之后，通过生成数据数学模型的算法来运行数据源视图中的数据“处理”  每个模型。 此过程也称为“对模型定型 ”。 有关详细信息，请参阅[处理要求和注意事项（数据挖掘）](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 处理模型之后，可以用可视化方式浏览挖掘模型，并创建针对该模型的预测查询。 如果已缓存来自定型过程的数据，则可以使用“钻取”  查询返回有关在模型中使用的事例的详细信息。  
  
 如果想要将模型用于生产（如用于进行预测或供一般用户进行浏览），则可将此模型部署到不同服务器。 如果将来需要重新处理该模型，则还必须同时导出基础挖掘结构的定义（如果需要，还须导出数据源定义和数据源视图）。  
  
 在部署模型时，您还必须确保在结构和模型上设置了正确的处理选项，并且潜在用户具有执行查询、查看模型或钻取结构或模型数据所需的权限。 有关详细信息，请参阅[安全性概述（数据挖掘）](../../analysis-services/data-mining/security-overview-data-mining.md)。  
  
  
##  <a name="bkmk_Complete"></a> 使用已完成的数据挖掘项目  
 本节总结可以使用已完成的数据挖掘项目的方法。 您可以创建准确性图表，浏览并验证数据，以及使数据挖掘模式可用于用户。  
  
> [!WARNING]  
>  用于数据挖掘模型的图表、查询和可视化对象不作为数据挖掘项目的一部分保存，并且不能进行部署。 如果您需要保持这些对象，则必须保存显示的内容，或按照针对每个对象的描述对其编写脚本。  
  
  
###  <a name="bkmk_ViewExplore"></a> View and Explore Models  
 创建模型之后，可以使用可视化工具和查询来浏览模型中的模式，并了解有关基础模式和统计数据的详细信息。 在数据挖掘设计器中的 **“挖掘模型查看器”** 选项卡中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 为每个挖掘模型类型提供了查看器，您可以使用这些查看器来浏览挖掘模型。  
  
 这些可视化对象都是临时的，并且在退出与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的会话时关闭这些对象，而无需保存。 因此，如果您需要将这些可视化对象导出到其他应用程序以进行显示或进一步分析，请使用查看器界面的每一个工具栏或窗格中提供的 **“复制”** 命令。  
  
 Excel 数据挖掘外接插件还提供可用于以 Visio 关系图表示模型并使用 Visio 工具对关系图进行批注和修改的 Visio 模板。 有关详细信息，请参阅 [适用于 Microsoft Office 2007 的 Microsoft SQL Server 2008 SP2 数据挖掘外接程序](http://go.microsoft.com/fwlink/?LinkID=123146)。  
  
  
###  <a name="bkmk_Validate"></a> Test and Validate Models  
 创建模型之后，可以调查结果，并确定性能最佳的模型。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供几个图表，使用这些图表可以提供可用于直接比较挖掘模型并选择最准确或最有用的挖掘模型的工具。 这些工具包括提升图、利润图和分类矩阵。 你可以使用数据挖掘设计器的“挖掘准确性图表”  选项卡来生成这些图表。  
  
 您还可以使用交叉验证报表对数据子集进行迭代抽样，进而确定模型是否偏重于某一特定数据集。 报表提供的统计信息可用于客观地比较模型，并评估您的定型数据的质量。  
  
 请注意：这些报表和图表不与项目存储在一起，也不存储在 ssASnoversion 数据库中，因此，如果您需要保留或复制这些结果，则应保存这些结果或使用 DMX 或 AMO 编写这些对象的脚本。 还可以将存储过程用于交叉验证。  
  
 有关详细信息，请参阅[测试和验证（数据挖掘）](../../analysis-services/data-mining/testing-and-validation-data-mining.md)。  
  
  
###  <a name="bkmk_Predict"></a> Create Predictions  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了一种称为数据挖掘扩展插件 (DMX) 的查询语言，该语言是创建预测的基础，并且可方便地编写脚本。 为了帮助您生成 DMX 预测查询， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中提供了查询生成器。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中还有许多用于查询编辑器的 DMX 模板。如果您不熟悉预测查询，建议您使用数据挖掘设计器和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中提供的查询生成器。 有关详细信息，请参阅 [Data Mining Tools](../../analysis-services/data-mining/data-mining-tools.md)。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中创建的预测不会持久化，因此，如果您的查询很复杂，或需要重现这些结果，我们建议您将预测查询保存到 DMX 查询文件中，对其编写脚本，或将这些查询作为 Integration Services 包的一部分嵌入。  
  
  
##  <a name="bkmk_API"></a> 对数据挖掘对象的编程访问  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供了可用于以编程方式处理数据挖掘项目和在其中对象的多个工具。 DMX 提供可用于创建数据源和数据源视图以及创建、定型和使用挖掘结构和模型的语句。 有关详细信息，请参阅[数据挖掘扩展插件 (DMX) 参考](../../dmx/data-mining-extensions-dmx-reference.md)。  
  
 还可以通过使用 Analysis Services 脚本语言 (ASSL) 或使用分析管理对象 (AMO) 来执行这些任务。 有关详细信息，请参阅 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)。  
  
  
## <a name="related-tasks"></a>相关任务  
 下面的主题介绍使用数据挖掘向导来创建数据挖掘项目及关联的对象。  
  
|“任务”|主题|  
|-----------|------------|  
|介绍如何使用挖掘结构列|[创建关系挖掘结构](../../analysis-services/data-mining/create-a-relational-mining-structure.md)|  
|提供有关如何添加新的挖掘模型以及处理结构和模型的详细信息|[将挖掘模型添加到结构 & #40;Analysis Services-数据挖掘 & #41;](../../analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|提供了指向一些资源的链接，这些资源可帮助您自定义生成数据挖掘模型的算法|[自定义挖掘模型和结构](../../analysis-services/data-mining/customize-mining-models-and-structure.md)|  
|提供了指向有关各个挖掘模型查看器的信息的链接|[数据挖掘模型查看器](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|了解如何创建提升图、利润图、分类矩阵或测试挖掘结构|[测试和验证 & #40; 数据挖掘 & #41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)|  
|了解有关处理选项和权限的信息|[处理数据挖掘对象](../../analysis-services/data-mining/processing-data-mining-objects.md)|  
|提供有关 Analysis Services 的详细信息|[多维模型数据库 ](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘设计器](../../analysis-services/data-mining/data-mining-designer.md)   
 [创建使用 SQL Server Data Tools & #40; 多维模型SSDT & #41;](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [工作区数据库](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)  
  
  
