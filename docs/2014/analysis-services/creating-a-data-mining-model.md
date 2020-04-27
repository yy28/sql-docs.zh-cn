---
title: 创建数据挖掘模型 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining models, creating
- forecasting [data mining]
- mining models, creating
- clustering [data mining]
- association [data mining]
- data modeling [data mining]
- estimation
- classification [data mining]
ms.assetid: 804b7db3-1f6a-4f73-a81d-bbe02520d7c6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a8893960b5177563ccf98dbd21cb528ce399ea3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086729"
---
# <a name="creating-a-data-mining-model"></a>创建数据挖掘模型
  数据建模是数据挖掘的一个步骤，通过将*算法*应用于数据来构建模式和趋势。 之后，可以使用这些模式进行分析或预测。  
  
 Office 数据挖掘外接程序通过向导（使用这些向导可轻松地创建模型）支持数据挖掘。 这些向导对数据进行分析、标识关联、计算所有变量的统计重要性，以及自动选择最佳模型。  
  
 尽管此功能的功能与[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]和[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]提供的数据挖掘工具一样强大，但向导和熟悉的 Excel 界面的组合使你可以轻松地创建、修改和使用数据挖掘。  
  
## <a name="advanced-data-mining"></a>高级（数据挖掘）  
 使用高级向导，您可以通过使用中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的数据挖掘算法之一，基于在 Excel 中存储的数据创建新的数据挖掘模型。  
  
### <a name="create-mining-structure"></a>创建挖掘结构  
 创建挖掘结构向导可帮助您生成新的数据挖掘结构并将其用作多个挖掘模型的基础。 通过该向导，可以选择保留要用作测试集的数据部分，因此，您可以按照一致的测试标准来对所有使用相同数据的模型进行评估。  
  
 [SQL Server 数据挖掘外接程序创建挖掘结构 &#40;&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
### <a name="add-model-to-structure"></a>将模型添加到结构  
 通过将模型添加到结构向导，可以选择现有的数据挖掘结构，并为该结构创建新的数据挖掘模型。 可以向结构中添加多个挖掘模型、更改参数或选择不同的数据挖掘算法，并自定义输出。  
  
 [将模型添加到用于 Excel 的数据挖掘外接 &#40;&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)  
  
## <a name="analyze-key-influencers-analyze"></a>分析关键影响因素（分析）  
 您选择感兴趣的列或输出值，然后算法将分析所有输入数据，以便标识对目标影响最大的因素。 或者，您可以创建比较任何两个值的报告，以便可以看到影响因素是如何变化的。  
  
 "**分析关键影响因素**" 工具使用 Microsoft Bayes 算法。  
  
 [分析&#41;Excel &#40;表分析工具的关键影响因素](analyze-key-influencers-table-analysis-tools-for-excel.md)  
  
## <a name="associate-data-mining"></a>关联（数据挖掘）  
 **关联**向导生成一个关联模型，用于检测在多个事务中出现的项之间的关联：例如，在市场篮分析中。  
  
 [用于 Excel 的数据挖掘客户端的关联向导 &#40;&#41;](associate-wizard-data-mining-client-for-excel.md)  
  
## <a name="classify-data-mining"></a>分类（数据挖掘）  
 **分类**向导生成一个分类模型，该模型分析提供给目标结果的因素。 您可以将多个算法用于此向导，包括决策树、Naïve Bayes 和神经网络。  
  
 [用于 Excel 的数据挖掘外接程序 &#40;分类向导&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="cluster-data-mining"></a>聚类分析（数据挖掘）  
 **聚**类分析向导生成一个聚类分析模型，用于检测具有相似特征的行组。 "聚类分析*segmentation*" 是一种无人监督学习技术，在尝试理解新数据中的模式和分组时非常有用。  
  
 Microsoft 聚类分析算法支持 K-means 聚类分析和期望最大化 (EM) 聚类分析的若干变化形式。  
  
 [群集向导 &#40;Excel 的数据挖掘外接程序&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)。  
  
## <a name="detect-categories-analyze"></a>检测类别（分析）  
 使用 "**检测类别**" 工具，可以添加任何数据集，并可以应用群集来查找数据分组。 这对于查找相似点以及创建组以进行进一步分析非常有用。  
  
 "**检测类别**" 工具使用 Microsoft 聚类分析算法。  
  
 [检测类别 &#40;Excel&#41;的表分析工具](detect-categories-table-analysis-tools-for-excel.md)  
  
## <a name="estimate-data-mining"></a>估计（数据挖掘）  
 估计向导生成一个估计模型，它提取数据模式并使用这些模式来预测连续的数字、日期或时间值。 它使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 决策树算法。  
  
 [估计向导 &#40;Excel 数据挖掘外接程序&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="fill-from-example-analyze"></a>从示例填充（分析）  
 "**从示例填充**" 工具可帮助您归结缺失值。 您提供缺失值应该是什么的一些示例，该工具将基于表中的所有数据生成模式，然后基于数据中的模式建议新值。  
  
 "**从示例填充**" 工具使用 Microsoft 逻辑回归算法。  
  
 [Excel&#41;&#40;的填充示例表分析工具](fill-from-example-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-analyze"></a>预测（分析）  
 **预测**工具获取随时间变化的数据，并预测将来的值。  
  
 **预测**工具使用 Microsoft 时序算法。  
  
 [用于 Excel&#41;的预测 &#40;表分析工具](forecast-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-data-mining"></a>预测（数据挖掘）  
 **预测**向导生成一个预测模型，该模型检测一系列单元中的模式，然后预测其他值。  
  
 [预测向导 &#40;Excel 数据挖掘外接程序&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="highlight-exceptions-analyze"></a>突出显示异常值（分析）  
 **突出显示异常**值工具可分析数据表中的模式，并查找不适合该模式的行和值。 然后，您可以查看和更正它们并重新运行模型，或者对值进行标记以便以后执行操作。  
  
 **突出显示异常**工具使用 Microsoft 聚类分析算法。  
  
 [突出显示 Excel &#40;表分析工具的异常&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
  
## <a name="prediction-calculator-analyze"></a>预测计算器（分析）  
 该工具创建对导致目标结果的因素进行分析的模型，然后基于从这些模式导出的条件预测任何新输入的结果。它还生成一个交互式的决策工作表，使您可以轻松地对新输入评分。 您还可以创建评分工作表的打印版本，以供脱机使用。  
  
 **预测计算器**工具使用 Microsoft 逻辑回归算法。  
  
 [用于 Excel&#41;的预测计算器 &#40;表分析工具](prediction-calculator-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-goal-seek-analyze"></a>应用场景：目标查找（分析）  
 在 "**目标查找**" 工具中，您可以指定一个目标值，该工具将标识为了满足目标而必须更改的基本因素。 例如，如果您知道必须将电话满意度增加 20%，则可以要求模型预测应进行变化以便实现该目标的因素。  
  
 **目标查找**工具使用 Microsoft 逻辑回归算法。  
  
 详细信息  
  
 [用于 Excel&#41;&#40;表分析工具的目标查找方案](goal-seek-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-what-if-scenario-analyze"></a>应用场景：“假设”应用场景（分析）  
 **假设分析工具是**对**目标查找**工具的补充。 使用此工具，您输入要更改的值，并且模型将预测该更改是否足以实现预期结果。 例如，您可以要求该模型推断再增加一名电话接线员是否可以将客户满意度增加一个百分点。  
  
 **假设**工具使用 Microsoft 逻辑回归算法。  
  
 [假设方案 &#40;Excel&#41;的表分析工具](what-if-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="shopping-basket-analysis-analyze"></a>购物篮分析（分析）  
 **购物篮分析**工具可创建经常一起购买的产品组，以确定可用于交叉销售或向上销售的模式。 它还基于相关产品捆绑的价格和成本生成报告，以便帮助进行决策。  
  
 您还可以将该工具用于经常一起发生的事件、导致诊断的因素或者任何其他可能原因和结果组。  
  
 **购物篮分析**工具使用 Microsoft 关联算法。  
  
 [用于 Excel&#41;&#40;表 AnalysisTools 的购物篮分析](shopping-basket-analysis-table-analysistools-for-excel.md)  
  
## <a name="see-also"></a>另请参阅  
 [浏览和清理数据](exploring-and-cleaning-data.md)   
 [验证模型和使用模型进行预测 &#40;Excel 数据挖掘外接程序&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [&#40;Excel 数据挖掘外接程序部署和缩放挖掘模型&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
