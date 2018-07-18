---
title: 测试和验证 （数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- testing data mining models
- comparing mining models
- continuous attribute charts
- data mining [Analysis Services], models
- charts [Analysis Services]
- predictive modeling [Analysis Services]
- mining models [Analysis Services], validating
- validating data mining models
- viewing mining accuracy
- confidence scores [data mining]
- displaying mining accuracy
- predictions [Analysis Services], comparing mining models
- scoring [data mining]
- lift charts [Analysis Services]
- classification matrix [Analysis Services]
- CRISP-DM
- accuracy testing [data mining]
ms.assetid: 197144f5-21ed-4009-b448-fe412fb3916c
caps.latest.revision: 60
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d3fb68f21136da8236c653aaae71c9a9e461b432
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230143"
---
# <a name="testing-and-validation-data-mining"></a>测试和验证（数据挖掘）
  验证是评估挖掘模型对实际数据执行情况的过程。 在将挖掘模型部署到生产环境之前，务必通过了解其质量和特征来对其进行验证。  
  
 本节将介绍与模型质量有关的一些基本概念，还将介绍 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中提供的模型验证的策略。 有关模型验证如何适合更大数据挖掘过程的概述，请参阅 [数据挖掘解决方案](data-mining-solutions.md)。  
  
## <a name="methods-for-testing-and-validation-of-data-mining-models"></a>测试和验证数据挖掘模型的方法  
 可以使用多种方法评估数据挖掘模型的质量和特征。  
  
-   使用统计信息有效性的各种度量值来确定数据或模型中是否存在问题。  
  
-   将数据划分为定型集和测试集，以测试预测的准确性。  
  
-   请求商业专家查看数据挖掘模型的结果，以确定发现的模式在目标商业方案中是否有意义。  
  
 所有这些方法在数据挖掘方法中都非常有用，在创建、测试和优化模型来解决特定问题时可以反复使用这些方法。 没有一个全面的规则可以说明什么时候模型已足够好，或者什么时候具有足够的数据。  
  
## <a name="definition-of-criteria-for-validating-data-mining-models"></a>验证数据挖掘模型的条件的定义  
 数据挖掘的度量通常分为以下三类：准确性、可靠性和有用性。  
  
  “准确性”是模型与所提供数据中的属性的结果相关联程度的度量值。 准确性有各种度量值，但准确性的所有度量值都依赖于所使用的数据。 事实上，值可能缺少或近似，数据可能已被多个进程更改。 特别是在探索和开发阶段，您可能决定允许数据中存在一定数量的错误，尤其是在数据的特征非常统一时。 例如，基于过去的销售额来预测特定商店的销售额的模型可能非常相关，并且非常准确，即使该商店一直使用错误的会计方法。 所以，准确性的度量值必须通过评估可靠性来平衡。  
  
  “可靠性”评估数据挖掘模型处理不同数据集的方法。 如果无论提供哪些测试数据，数据挖掘模型都生成相同类型的预测，或者发现相同常规类型的模式，则该数据挖掘模型是可靠的。 例如，为使用错误会计方法的商店生成预测的模型将不适用于其他商店，因此该模型是不可靠的。  
  
  “有用性”包括说明模型是否提供了有用信息的各种指标。 例如，将商店位置与销售额相关联的数据挖掘模型可能既是准确的，也是可靠的，但可能是无用的，因为不能通过在同一位置增加更多商店来推广该结果。 而且，它没有回答为什么某些位置销售额较高这一基本商业问题。 您可能还会发现，如果模型基于数据中的交叉关联，它看起来是成功，但实际上没有意义。  
  
## <a name="tools-for-testing-and-validation-of-mining-models"></a>用于测试和验证挖掘模型的的工具  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持多种验证方法。  
  
-   将数据分区为测试集和定型集  
  
-   筛选模型以便定型和测试同一源数据的不同组合。  
  
-   测量“提升”  和“增长” 。 “提升图”  是将使用数据挖掘模型获得的改进与随机推测进行对比时，可视化所获得改进的方法。  
  
-   执行数据集的交叉验证  
  
-   生成“分类矩阵” 。 这些图在表中对准确和不准确的推测进行排序，以便可以快速方便地衡量模型预测目标值的准确程度。  
  
-   创建“散点图”  以评估回归公式的拟合度。  
  
-   创建将财务收益或成本与使用挖掘模型相关联的“利润图”  ，以便评估建议的值。  
  
 这些度量不能准确回答数据挖掘模型是否能解决商业问题等之类的问题；但它们提供了可用于评估预测性分析的可靠性的目标度量值，并指导您是否在开发流程中使用特定遍历的决策。  
  
 本节中的主题提供了每个方法的概述，并引导您使用 SQL Server 数据挖掘完成度量您生成的模型准确性的过程。  
  
### <a name="related-topics"></a>相关主题  
  
|主题|链接|  
|------------|-----------|  
|了解如何使用向导或 DMX 命令设置测试数据集|[定型数据集和测试数据集](training-and-testing-data-sets.md)|  
|了解如何测试挖掘结构中的数据分布和代表性|[交叉验证&#40;Analysis Services-数据挖掘&#41;](cross-validation-analysis-services-data-mining.md)|  
|了解有关 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]中提供的图标类型的准确性。|[提升图&#40;Analysis Services-数据挖掘&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [利润图&#40;Analysis Services-数据挖掘&#41;](profit-chart-analysis-services-data-mining.md)<br /><br /> [散点图&#40;Analysis Services-数据挖掘&#41;](scatter-plot-analysis-services-data-mining.md)|  
|了解如何创建分类矩阵（有时也称为混淆矩阵），以评估真正、假正、真负和假负的次数。|[分类矩阵&#40;Analysis Services-数据挖掘&#41;](classification-matrix-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘工具](data-mining-tools.md)   
 [数据挖掘解决方案](data-mining-solutions.md)   
 [测试和验证任务和操作指南&#40;数据挖掘&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  
