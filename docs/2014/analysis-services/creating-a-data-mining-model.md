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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086729"
---
# <a name="creating-a-data-mining-model"></a>创建数据挖掘模型
  数据建模是数据挖掘的步骤在其中通过应用中创建的模式和趋势*算法*数据。 之后，可以使用这些模式进行分析或预测。  
  
 Office 数据挖掘外接程序通过向导（使用这些向导可轻松地创建模型）支持数据挖掘。 这些向导对数据进行分析、标识关联、计算所有变量的统计重要性，以及自动选择最佳模型。  
  
 虽然此功能是作为数据挖掘提供的工具同样强大[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]和[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，组合的向导和熟悉的 Excel 界面轻松创建、 修改和使用数据挖掘。  
  
## <a name="advanced-data-mining"></a>高级（数据挖掘）  
 高级的向导可用于创建新的数据挖掘模型，根据数据存储在 Excel 中，通过使用中的数据挖掘算法之一[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
### <a name="create-mining-structure"></a>创建挖掘结构  
 创建挖掘结构向导可帮助您生成新的数据挖掘结构并将其用作多个挖掘模型的基础。 通过该向导，可以选择保留要用作测试集的数据部分，因此，您可以按照一致的测试标准来对所有使用相同数据的模型进行评估。  
  
 [创建挖掘结构&#40;SQL Server 数据挖掘外接程序&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
### <a name="add-model-to-structure"></a>将模型添加到结构  
 通过将模型添加到结构向导，可以选择现有的数据挖掘结构，并为该结构创建新的数据挖掘模型。 可以向结构中添加多个挖掘模型、更改参数或选择不同的数据挖掘算法，并自定义输出。  
  
 [向结构添加模型&#40;Excel 数据挖掘外接程序&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)  
  
## <a name="analyze-key-influencers-analyze"></a>分析关键影响因素（分析）  
 您选择感兴趣的列或输出值，然后算法将分析所有输入数据，以便标识对目标影响最大的因素。 或者，您可以创建比较任何两个值的报告，以便可以看到影响因素是如何变化的。  
  
 **分析关键影响因素**工具使用 Microsoft 朴素贝叶斯算法。  
  
 [分析关键影响因素&#40;Excel 表分析工具&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
  
## <a name="associate-data-mining"></a>关联（数据挖掘）  
 **相关联**向导生成一个关联模型，它检测在多个事务中出现的项之间的关联性： 例如，在市场篮分析。  
  
 [关联向导&#40;Excel 数据挖掘客户端&#41;](associate-wizard-data-mining-client-for-excel.md)  
  
## <a name="classify-data-mining"></a>分类（数据挖掘）  
 **分类**向导生成一个分类模型，用于分析目标结果影响因素。 您可以将多个算法用于此向导，包括决策树、Naïve Bayes 和神经网络。  
  
 [分类向导&#40;Excel 数据挖掘外接程序&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="cluster-data-mining"></a>聚类分析（数据挖掘）  
 **群集**向导生成一个聚类分析模型，它检测各组具有相似特征的行。 聚类分析 (有时称为*分段*) 是一种非监督式的学习技术，是尝试了解模式和新数据中的分组时非常有用。  
  
 Microsoft 聚类分析算法支持 K-means 聚类分析和期望最大化 (EM) 聚类分析的若干变化形式。  
  
 [群集向导&#40;Excel 数据挖掘外接程序&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)。  
  
## <a name="detect-categories-analyze"></a>检测类别（分析）  
 **检测类别**工具，可以添加任何数据集和应用聚类分析来找到数据分组。 它可用于找到相似之处和创建组来进一步分析。  
  
 **检测类别**工具使用 Microsoft 聚类分析算法。  
  
 [检测类别&#40;Excel 表分析工具&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
## <a name="estimate-data-mining"></a>估计（数据挖掘）  
 估计向导生成一个估计模型，它提取数据模式并使用这些模式来预测连续的数字、日期或时间值。 它使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 决策树算法。  
  
 [估计向导&#40;Excel 数据挖掘外接程序&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="fill-from-example-analyze"></a>从示例填充（分析）  
 **从示例填充**工具可帮助您归结缺失值的原因。 您提供缺失值应该是什么的一些示例，该工具将基于表中的所有数据生成模式，然后基于数据中的模式建议新值。  
  
 **从示例填充**工具使用 Microsoft 逻辑回归算法。  
  
 [从示例填充&#40;Excel 表分析工具&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-analyze"></a>预测（分析）  
 **预测**工具使用数据发生变化时，并预测将来值。  
  
 **预测**工具使用 Microsoft 时序算法。  
  
 [预测&#40;Excel 表分析工具&#41;](forecast-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-data-mining"></a>预测（数据挖掘）  
 **预测**向导生成一个预测模型来检测模式中的单元格，一系列，然后预测其他值。  
  
 [预测向导&#40;Excel 数据挖掘外接程序&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="highlight-exceptions-analyze"></a>突出显示异常值（分析）  
 **突出显示异常**工具分析数据的表中的模式，查找不适合该模式的行和值。 然后，您可以查看和更正它们并重新运行模型，或者对值进行标记以便以后执行操作。  
  
 **突出显示异常**工具使用 Microsoft 聚类分析算法。  
  
 [突出显示异常值&#40;Excel 表分析工具&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
  
## <a name="prediction-calculator-analyze"></a>预测计算器（分析）  
 该工具创建对导致目标结果的因素进行分析的模型，然后基于从这些模式导出的条件预测任何新输入的结果。它还生成一个交互式的决策工作表，使您可以轻松地对新输入评分。 您还可以创建评分工作表的打印版本，以供脱机使用。  
  
 **预测计算器**工具使用 Microsoft 逻辑回归算法。  
  
 [预测计算器&#40;Excel 表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-goal-seek-analyze"></a>方案：目标查找 （分析）  
 在中**目标查找**工具，您指定一个目标值，并且该工具标识必须更改才能满足该目标的潜在因素。 例如，如果您知道必须将电话满意度增加 20%，则可以要求模型预测应进行变化以便实现该目标的因素。  
  
 **目标查找**工具使用 Microsoft 逻辑回归算法。  
  
 详细信息  
  
 [目标查找应用场景&#40;Excel 表分析工具&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-what-if-scenario-analyze"></a>方案：假设方案 （分析）  
 **模拟分析**工具补充**目标查找**工具。 使用此工具，您输入要更改的值，并且模型将预测该更改是否足以实现预期结果。 例如，您可以要求该模型推断再增加一名电话接线员是否可以将客户满意度增加一个百分点。  
  
 **假设**工具使用 Microsoft 逻辑回归算法。  
  
 [假设方案&#40;Excel 表分析工具&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="shopping-basket-analysis-analyze"></a>购物篮分析（分析）  
 **购物篮分析**工具创建的经常购买的产品组一起，以识别模式可用于交叉销售或向上销售。 它还基于相关产品捆绑的价格和成本生成报告，以便帮助进行决策。  
  
 您还可以将该工具用于经常一起发生的事件、导致诊断的因素或者任何其他可能原因和结果组。  
  
 **购物篮分析**工具使用 Microsoft 关联算法。  
  
 [购物篮分析&#40;Excel 表分析工具&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
  
## <a name="see-also"></a>请参阅  
 [浏览和清除数据](exploring-and-cleaning-data.md)   
 [验证模型和使用模型进行预测&#40;Excel 数据挖掘外接程序&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [部署和缩放挖掘模型&#40;Excel 数据挖掘外接程序&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
