---
title: 数据挖掘查询 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- prediction queries [Analysis Services]
- queries [DMX], creating
- prediction queries [DMX]
- Prediction Query Builder
- mining models [Analysis Services], querying
ms.assetid: 802806a6-69bb-4c3c-b9aa-d1a1ddfc7fc2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bfce63f3686f06c0289c818daac82f336fb2b17
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084973"
---
# <a name="data-mining-queries"></a>数据挖掘查询
  数据挖掘查询可用于多种目的。 可以：  
  
-   将模型应用于新数据以进行单个或多个预测。 可以将输入值作为参数提供，也可以使用批处理文件提供输入值。  
  
-   获取用于定型的数据的统计摘要。  
  
-   提取模式和规则，或生成表示模型中某种模式的典型事例的配置文件。  
  
-   提取回归公式和其他解释模式的计算。  
  
-   获取适应特定模式的事例。  
  
-   检索有关模型中使用的各个事例的详细信息，包括分析中未使用的数据。  
  
-   通过添加新数据或执行交叉预测重新定型模型。  
  
 本节概述了您开始使用数据挖掘查询时所需的信息。 它说明了可针对数据挖掘对象创建的查询类型，介绍了查询工具和查询语言，并提供了一些链接，这些链接指向可针对使用 SQL Server 数据挖掘中提供的算法生成的模型创建的查询示例。  
  
 [了解数据挖掘查询](#bkmk_Understand)  
  
 [查询工具和接口](#bkmk_Interfaces)  
  
 [不同模型类型的查询](#bkmk_ModelTypes)  
  
 [要求](#bkmk_Reqs)  
  
##  <a name="bkmk_Understand"></a>了解数据挖掘查询  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据挖掘支持以下查询类型：  
  
-   [数据挖掘 &#40;预测查询&#41;](prediction-queries-data-mining.md)  
  
     基于模型中的模式和输入数据进行推断的查询。  
  
-   [内容查询 &#40;数据挖掘&#41;](content-queries-data-mining.md)  
  
     返回元数据、统计信息和有关模型本身的其他信息的查询。  
  
-   [数据挖掘 &#40;钻取查询&#41;](drillthrough-queries-data-mining.md)  
  
     可以检索模型的基础事例数据、甚至结构中未用于模型的数据的查询。  
  
-   [数据定义查询 &#40;数据挖掘&#41;](data-definition-queries-data-mining.md)  
  
     不从模型返回信息，而是用于生成模型和结构或更新模型/结构中的数据的查询。  
  
 在创建查询之前，建议您了解使用 SQL Server 提供的每种数据挖掘算法创建的各个模型之间的差异。  
  
-   可以使用为每种算法类型提供的自定义数据挖掘查看器来浏览和了解各种模型类型。 有关详细信息，请参阅 [挖掘模型查看器任务和操作指南](mining-model-viewer-tasks-and-how-tos.md)。  
  
-   可以使用 **“Microsoft 一般内容树查看器”** 来查看各种模型类型的模型内容。 若要解释此信息，请参阅 [挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。  
  
##  <a name="bkmk_Interfaces"></a>查询工具和接口  
 可以使用 SQL Server 提供的查询工具之一来以交互方式生成数据挖掘查询。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中都提供图形预测查询生成器。 如果您之前未使用过预测查询生成器，建议您按照 [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md) 中的步骤进行操作来了解接口。 有关各步骤的概述，请参阅 [使用预测查询生成器创建预测查询](create-a-prediction-query-using-the-prediction-query-builder.md)。  
  
 对于开始您稍后将自定义的查询，预测查询生成器会很有用。 可以轻松添加数据源并将其映射到列，然后切换到 DMX 视图，并通过添加 WHERE 子句或其他函数来自定义查询。  
  
 在了解数据挖掘模型以及生成查询的方式之后，您还可以使用数据挖掘扩展插件 (DMX) 直接编写查询。 DMX 是一种类似于 Transact-SQL 的查询语言，可以从多种不同的客户端使用它。 DMX 是用来创建自定义预测和复杂查询的理想工具。 有关 DMX 的介绍，请参阅[使用 DMX 创建和查询数据挖掘模型：教程（Analysis Services - 数据挖掘）](../../tutorials/create-query-data-mining-models-dmx-tutorials.md)  
  
 
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中都提供了 DMX 编辑器。 您还可以使用预测查询生成器来开始查询，然后将视图更改为文本编辑器，并将 DMX 语句复制到其他客户端。 有关详细信息，请参阅[数据挖掘查询接口](data-mining-query-tools.md)。  
  
 可以通过编程方式来编写 DMX 语句，然后使用 AMO 或 XMLA 将这些语句从您的客户端发送到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。 但是，DMX 是您在针对挖掘模型创建查询时必须使用的语言。  
  
 您还可以使用基于数据挖掘架构行集的动态管理视图 (DMV) 来查询模型的元数据、统计信息和某些内容。 利用这些 DMV，您可以通过键入 SELECT 语句来轻松检索有关模型的信息；但不能创建预测。 有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持的 DMV 的详细信息，请参阅[使用动态管理视图 (DMV) 监视 Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)。  
  
 最后，您可以使用 [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)或 [Data Mining Query Transformation](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)创建数据挖掘查询以供在 Integration Services 包中使用。 控制流任务支持多种类型的 DMX 查询，而数据流转换只支持使用数据流中的数据的查询，即使用 PREDICTION JOIN 语法的查询。  
  
##  <a name="bkmk_ModelTypes"></a>不同模型类型的查询  
 在创建模型时使用的算法会极大地影响您可以从数据挖掘查询获取的信息类型。 导致出现差异的原因是，每种算法都以不同方式处理数据，并存储不同类型的模式。 例如，一些算法会创建群集；另一些算法会创建树。 因此，您可能需要使用专用的预测和查询函数，具体取决于所使用的模型类型。  
  
 以下列表汇总了可在查询中使用的函数：  
  
-   **一般预测函数：** 此`Predict`函数是多态函数，这意味着它适用于所有模型类型。 该函数将自动检测要使用的模型类型，并提示您输入其他参数。 有关详细信息，请参阅[预测 (DMX)](/sql/dmx/predict-dmx)。  
  
    > [!WARNING]  
    >  并非所有模型都用于进行预测。 例如，可以创建不具有可预测属性的聚类分析模型。 但是，即使模型不具有可预测属性，您也可以创建返回模型中其他类型的有用信息的预测查询。  
  
-   **自定义预测函数：** 每种模型类型都提供一组用于处理该算法所创建的模式的预测函数。  
  
     例如，为时序模型提供了 `Lag` 函数，可使用此函数查看该模型使用的历史数据。 对于聚类分析模型，`ClusterDistance` 函数等函数会更有用。  
  
     有关每种模型类型支持的函数的详细信息，请参阅以下链接：  
  
    |||  
    |-|-|  
    |[关联模型查询示例](association-model-query-examples.md)|[Microsoft Naive Bayes Algorithm](microsoft-naive-bayes-algorithm.md)|  
    |[聚类分析模型查询示例](clustering-model-query-examples.md)|[神经网络模型查询示例](neural-network-model-query-examples.md)|  
    |[决策树模型查询示例](decision-trees-model-query-examples.md)|[顺序分析和聚类分析模型查询示例](sequence-clustering-model-query-examples.md)|  
    |[线性回归模型查询示例](linear-regression-model-query-examples.md)|[时序模型查询示例](time-series-model-query-examples.md)|  
    |[逻辑回归模型查询示例](logistic-regression-model-query-examples.md)||  
  
     您还可以调用 VBA 函数，或创建您自己的函数。 有关详细信息，请参阅[函数 (DMX)](/sql/dmx/functions-dmx)。  
  
-   **常规统计信息：** 几乎所有模型类型都可以使用多个函数，这些函数返回一组标准描述性统计信息，如标准偏差。  
  
     例如，`PredictHistogram` 函数将返回一个表，其中列出了指定列的所有状态。  
  
     有关详细信息，请参阅[通用预测函数 (DMX)](/sql/dmx/general-prediction-functions-dmx)。  
  
-   **自定义统计信息：** 为每种模型类型提供了附加支持函数，以便生成与特定分析任务相关的统计信息。  
  
     例如，在使用聚类分析模型时，您可以使用 `PredictCaseLikelihood` 函数来返回与某个特定事例和分类关联的可能性分数。 但是，如果您创建了线性回归模型，则可能更愿意检索系数和截距，可使用内容查询做到这一点。  
  
-   **模型内容函数：** 所有模型的*内容*都以标准化格式表示，可让你使用简单查询检索信息。 可以使用 DMX 创建针对模型内容的查询。 还可以通过使用数据挖掘架构行集来获取某种类型的模型内容。  
  
     在模型内容中，返回的表中的每个行或节点的含义是不同的，具体取决于用于生成模型的算法的类型以及列的数据类型。 有关详细信息，请参阅 [内容查询（数据挖掘）](content-queries-data-mining.md)。  
  
##  <a name="bkmk_Reqs"></a>要求  
 必须先处理数据挖掘模型，然后才能创建针对模型的查询。 处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象需要特殊权限。 有关处理挖掘模型的详细信息，请参阅[处理要求和注意事项（数据挖掘）](processing-requirements-and-considerations-data-mining.md)。  
  
 执行针对数据挖掘模型的查询需要不同的权限级别，这取决于您运行的查询的类型。 例如，钻取事例或结构数据通常需要可在挖掘结构对象或挖掘模型对象上设置的附加权限。  
  
 但是，如果您的查询使用外部数据并包含 OPENROWSET 或 OPENQUERY 等语句，则您查询的数据库必须启用这些语句，并且您必须具有基础数据库对象的权限。  
  
 有关运行数据挖掘查询所需的安全上下文的详细信息，请参阅[安全性概述（数据挖掘）](security-overview-data-mining.md)。  
  
## <a name="in-this-section"></a>本节内容  
 本节中的各个主题详细地介绍了每种类型的数据挖掘查询，并提供了一些链接，这些链接指向有关如何创建针对数据挖掘模型的查询的详细示例。  
  
 [数据挖掘 &#40;预测查询&#41;](prediction-queries-data-mining.md)  
  
 [内容查询 &#40;数据挖掘&#41;](content-queries-data-mining.md)  
  
 [数据挖掘 &#40;钻取查询&#41;](drillthrough-queries-data-mining.md)  
  
 [数据定义查询 &#40;数据挖掘&#41;](data-definition-queries-data-mining.md)  
  
 [数据挖掘查询接口](data-mining-query-tools.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 使用这些链接了解如何创建和使用数据挖掘查询。  
  
|任务|链接|  
|-----------|-----------|  
|查看有关数据挖掘查询的教程和演练|[第6课：创建和使用预测 &#40;基本数据挖掘教程&#41;](../../tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)<br /><br /> [时序预测 DMX 教程](../../tutorials/time-series-prediction-dmx-tutorial.md)|  
|在 SQL Server Management Studio 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|[在 SQL Server Management Studio 中创建一个 DMX 查询](create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [使用预测查询生成器创建预测查询](create-a-prediction-query-using-the-prediction-query-builder.md)<br /><br /> [将预测函数应用于模型](apply-prediction-functions-to-a-model.md)<br /><br /> [手动编辑预测查询](manually-edit-a-prediction-query.md)|  
|使用预测查询中使用的外部数据|[为预测查询选择和映射输入数据](choose-and-map-input-data-for-a-prediction-query.md)<br /><br /> [为预测查询选择和映射输入数据](choose-and-map-input-data-for-a-prediction-query.md)|  
|使用查询结果|[查看和保存预测查询的结果](view-and-save-the-results-of-a-prediction-query.md)|  
|使用 Management Studio 中提供的 DMX 和 XMLA 查询模板|[通过模板创建单独预测查询](create-a-singleton-prediction-query-from-a-template.md)<br /><br /> [使用 XMLA 创建数据挖掘查询](create-a-data-mining-query-by-using-xmla.md)<br /><br /> [Use Analysis Services Templates in SQL Server Management Studio](../instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|了解有关内容查询的详细信息和参阅示例|[针对挖掘模型创建内容查询](create-a-content-query-on-a-mining-model.md)<br /><br /> [查询用于创建挖掘模型的参数](query-the-parameters-used-to-create-a-mining-model.md)<br /><br /> [内容查询 &#40;数据挖掘&#41;](content-queries-data-mining.md)|  
|设置查询选项和解决查询权限问题|[更改数据挖掘查询的超时值](data-mining-queries.md)|  
|在 Integration Services 中使用数据挖掘组件|[数据挖掘查询任务](../../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [数据挖掘查询转换](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型内容 &#40;Analysis Services 数据挖掘&#41;](mining-model-content-analysis-services-data-mining.md)  
  
  
