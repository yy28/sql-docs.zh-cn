---
title: 验证模型和使用模型进行预测（Excel 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- mining models, charting
- validation [data mining]
- mining models, testing
ms.assetid: e245ac1f-1230-48e9-9091-e70b131aa2a8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 00048ea3c5f344a90e93799a92b4d48c07325482
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938158"
---
# <a name="validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel"></a>验证模型和使用模型进行预测（Excel 数据挖掘外接程序）
  测试和验证模型是数据挖掘过程中很重要的一步。 将挖掘模型部署到生产环境中之前，必须了解挖掘模型对于实际数据的执行情况。  
  
 数据挖掘外接程序包含的工具可帮助您对生成的模型进行测试，以及使用模型创建预测和建议。  
  
## <a name="accuracy-chart"></a>准确性图表  
 **准确性图表**向导可帮助您创建预测查询，并通过创建提升图或散点图来评估数据挖掘模型的性能。 提升图有助于区分同一结构中几乎相同的两个模型，从而帮助您确定哪个模型能够提供最佳的预测。  
  
 [SQL Server 数据挖掘外接程序的准确性图表 &#40;&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
## <a name="classification-matrix"></a>分类矩阵  
 **分类矩阵**向导可帮助您创建预测查询，以评估分类模型的性能。 其输出是一张图表，汇总了模型所做出的准确预测及不准确预测。 该矩阵是一个重要的工具，因为它不仅可显示模型正确预测某一值的频率，而且还显示模型最经常预测错的值。  
  
 [SQL Server 数据挖掘外接程序的分类矩阵 &#40;&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
## <a name="profit-chart"></a>利润图  
 **利润图**向导可帮助您权衡使用数据挖掘模型的好处，并评估误报和漏报的成本  
  
 此图表类型衡量模型的预测精确性并且纳入您指定的单位和整体成本。  
  
 [利润图 &#40;SQL Server 数据挖掘外接程序&#41;](profit-chart-sql-server-data-mining-add-ins.md)。  
  
## <a name="cross-validation"></a>交叉验证  
 交叉验证是数据挖掘社区中的一种既有技术，用于评估某一数据集的有效性以及该数据集上挖掘模型的精确性。 它会将一个数据集划分为多个子集，然后在每个子集上反复创建、定型和测试模型。  
  
 使用**交叉验证**向导可以指定要将数据划分成多少个折叠，然后提供一份交叉验证报表，该报表以统计方式描述这些交叉部分之间的差异。 从该报表中，您可以确定模型是在所有定型数据上都正常运行，还是可能只对特定子集倾斜。  
  
 [SQL Server 数据挖掘外接程序的交叉验证 &#40;&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
  
## <a name="query-wizard"></a>查询向导  
 **查询**向导是一种可帮助您生成预测查询的交互式工具。 查询是您生成建议、将来的预测等的方式。  
  
 在**查询**向导中，您可以选择一个模型，然后以单个值或从表或范围提供输入数据，向导将帮助您选择要输出的列。 您还可以向查询中添加函数，以便生成概率分数和其他有用的统计信息。  
  
 [查询 &#40;SQL Server 数据挖掘外接程序&#41;](query-sql-server-data-mining-add-ins.md)  
  
## <a name="advanced-query-editor"></a>高级查询编辑器  
 **高级查询编辑器**是一组交互式对话框，可帮助您生成所有类型的 DMX 语句、运行自定义查询来创建和定型新模型、删除模型或创建新数据集。  
  
 [高级数据挖掘查询编辑器](advanced-data-mining-query-editor.md)  
  
## <a name="see-also"></a>另请参阅  
 [浏览和清理数据](exploring-and-cleaning-data.md)   
 [创建数据挖掘模型](creating-a-data-mining-model.md)   
 [&#40;Excel 数据挖掘外接程序部署和缩放挖掘模型&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
