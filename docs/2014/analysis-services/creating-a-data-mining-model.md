---
title: 创建数据挖掘模型 |Microsoft 文档
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3c08737f07db68bd0e598844325d82172c3b1b44
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126405"
---
# <a name="creating-a-data-mining-model"></a>创建数据挖掘模型
  数据建模是数据挖掘的步骤在其中通过应用中创建模式和趋势*算法*到数据。 之后，可以使用这些模式进行分析或预测。  
  
 Office 数据挖掘外接程序通过向导（使用这些向导可轻松地创建模型）支持数据挖掘。 这些向导对数据进行分析、标识关联、计算所有变量的统计重要性，以及自动选择最佳模型。  
  
 虽然此功能是每个数据挖掘提供的工具一样功能强大的位[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]和[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，向导和熟悉的 Excel 界面的组合，可以轻松地创建、 修改和使用数据挖掘。  
  
## <a name="advanced-data-mining"></a>高级（数据挖掘）  
 高级的向导允许您创建新的数据挖掘模型，基于数据存储在 Excel 中，通过使用中的数据挖掘算法之一[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
### <a name="create-mining-structure"></a>创建挖掘结构  
 创建挖掘结构向导可帮助您生成新的数据挖掘结构并将其用作多个挖掘模型的基础。 通过该向导，可以选择保留要用作测试集的数据部分，因此，您可以按照一致的测试标准来对所有使用相同数据的模型进行评估。  
  
 [创建挖掘结构&#40;SQL Server 数据挖掘外接程序&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
### <a name="add-model-to-structure"></a>将模型添加到结构  
 通过将模型添加到结构向导，可以选择现有的数据挖掘结构，并为该结构创建新的数据挖掘模型。 可以向结构中添加多个挖掘模型、更改参数或选择不同的数据挖掘算法，并自定义输出。  
  
 [将模型添加到结构&#40;数据挖掘的 Excel 外接程序&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)  
  
## <a name="analyze-key-influencers-analyze"></a>分析关键影响因素（分析）  
 您选择感兴趣的列或输出值，然后算法将分析所有输入数据，以便标识对目标影响最大的因素。 或者，您可以创建比较任何两个值的报告，以便可以看到影响因素是如何变化的。  
  
 **分析关键影响因素**工具使用 Microsoft Naïve Bayes 算法。  
  
 [分析关键影响因素&#40;的 Excel 表分析工具&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
  
## <a name="associate-data-mining"></a>关联（数据挖掘）  
 **关联**向导生成的检测到出现在多个事务中的项之间的关联的关联模型： 例如，在市场篮分析。  
  
 [关联向导&#40;for Excel 数据挖掘客户端&#41;](associate-wizard-data-mining-client-for-excel.md)  
  
## <a name="classify-data-mining"></a>分类（数据挖掘）  
 **分类**向导生成分析导致目标结果的因素的分类模型。 您可以将多个算法用于此向导，包括决策树、Naïve Bayes 和神经网络。  
  
 [分类向导&#40;数据挖掘的 Excel 外接程序&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="cluster-data-mining"></a>聚类分析（数据挖掘）  
 **群集**向导生成的聚类分析模型，检测到的具有相似的特征的行组。 群集 (有时称为*分段*) 是尝试了解模式和新数据中的分组时非常有用的一种无监督的学习技术。  
  
 Microsoft 聚类分析算法支持 K-means 聚类分析和期望最大化 (EM) 聚类分析的若干变化形式。  
  
 [群集向导&#40;数据挖掘外接程序 excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)。  
  
## <a name="detect-categories-analyze"></a>检测类别（分析）  
 **检测类别**工具，可以添加任何数据集和应用群集来找出的数据分组。 它用于找到相似之处和创建组以便进一步分析。  
  
 **检测类别**工具使用 Microsoft 聚类分析算法。  
  
 [检测类别&#40;的 Excel 表分析工具&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
## <a name="estimate-data-mining"></a>估计（数据挖掘）  
 估计向导生成一个估计模型，它提取数据模式并使用这些模式来预测连续的数字、日期或时间值。 它使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 决策树算法。  
  
 [估计向导&#40;数据挖掘的 Excel 外接程序&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="fill-from-example-analyze"></a>从示例填充（分析）  
 **从示例填充**工具可帮助您输入缺失值。 您提供缺失值应该是什么的一些示例，该工具将基于表中的所有数据生成模式，然后基于数据中的模式建议新值。  
  
 **从示例填充**工具使用 Microsoft 逻辑回归算法。  
  
 [从示例填充&#40;的 Excel 表分析工具&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-analyze"></a>预测（分析）  
 **预测**工具将数据更改随着时间推移，并预测将来的值。  
  
 **预测**工具使用 Microsoft 时序算法。  
  
 [预测&#40;的 Excel 表分析工具&#41;](forecast-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-data-mining"></a>预测（数据挖掘）  
 **预测**向导生成一个预测模型中一系列单元格，检测模式并然后预测，其他值。  
  
 [预测向导&#40;数据挖掘的 Excel 外接程序&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="highlight-exceptions-analyze"></a>突出显示异常值（分析）  
 **突出显示异常**工具可分析数据的表中的模式并查找行和不符合模式的值。 然后，您可以查看和更正它们并重新运行模型，或者对值进行标记以便以后执行操作。  
  
 **突出显示异常**工具使用 Microsoft 聚类分析算法。  
  
 [突出显示异常&#40;的 Excel 表分析工具&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
  
## <a name="prediction-calculator-analyze"></a>预测计算器（分析）  
 该工具创建对导致目标结果的因素进行分析的模型，然后基于从这些模式导出的条件预测任何新输入的结果。它还生成一个交互式的决策工作表，使您可以轻松地对新输入评分。 您还可以创建评分工作表的打印版本，以供脱机使用。  
  
 **预测计算器**工具使用 Microsoft 逻辑回归算法。  
  
 [预测计算器&#40;的 Excel 表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-goal-seek-analyze"></a>应用场景：目标查找（分析）  
 在**目标查找**工具，你指定一个目标值以及该工具标识必须更改以满足该目标的基础因素。 例如，如果您知道必须将电话满意度增加 20%，则可以要求模型预测应进行变化以便实现该目标的因素。  
  
 **目标查找**工具使用 Microsoft 逻辑回归算法。  
  
 详细信息  
  
 [目标查找方案&#40;的 Excel 表分析工具&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-what-if-scenario-analyze"></a>应用场景：“假设”应用场景（分析）  
 **模拟分析**工具补充**目标查找**工具。 使用此工具，您输入要更改的值，并且模型将预测该更改是否足以实现预期结果。 例如，您可以要求该模型推断再增加一名电话接线员是否可以将客户满意度增加一个百分点。  
  
 **假设**工具使用 Microsoft 逻辑回归算法。  
  
 [假设分析方案&#40;的 Excel 表分析工具&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="shopping-basket-analysis-analyze"></a>购物篮分析（分析）  
 **购物篮分析**工具将创建频繁购买的产品组的组合在一起以识别可在交叉销售的模式或纵向销售。 它还基于相关产品捆绑的价格和成本生成报告，以便帮助进行决策。  
  
 您还可以将该工具用于经常一起发生的事件、导致诊断的因素或者任何其他可能原因和结果组。  
  
 **购物篮分析**工具使用 Microsoft 关联算法。  
  
 [购物篮分析&#40;的 Excel 表 AnalysisTools&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
  
## <a name="see-also"></a>请参阅  
 [浏览和清理数据](exploring-and-cleaning-data.md)   
 [验证模型和使用预测模型&#40;数据挖掘的 Excel 外接程序&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [部署和缩放挖掘模型&#40;数据挖掘的 Excel 外接程序&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  