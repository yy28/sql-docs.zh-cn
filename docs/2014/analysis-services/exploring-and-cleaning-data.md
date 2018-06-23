---
title: 浏览和清理数据 |Microsoft 文档
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0c39eaa58152fd1a75eeaefdc79bae93ccd36b98
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015153"
---
# <a name="exploring-and-cleaning-data"></a>浏览和清除数据
  数据准备不仅在于清理数据。 请牢记，准备数据的方式还会影响最终解释结果的方式。 数据准备涉及以下任务：  
  
-   探索和检查数据的分布。  
  
-   清除有错的记录并选择用于数据挖掘的列。  
  
-   适当地处理 null。  
  
-   按不同的大块时间将值归入统计或聚合值。  
  
-   添加标签以提高结果的可用性。  
  
-   在必要时转换数据类型或将值分类以供分析。  
  
 如果你不熟悉数据建模，我们建议你阅读相关的主题，[清单的准备工作数据挖掘](checklist-of-preparation-for-data-mining.md)。  
  
## <a name="data-preparation-tools"></a>数据准备工具  
 Office 数据挖掘外接包括用于数据清理和准备的以下工具：  
  
### <a name="explore-data"></a>浏览数据  
 使用**浏览数据**向导中为以下数据准备任务：  
  
-   预览数据并且标识在分析前必须修复的错误。  
  
-   收集用于了解数据的平衡性和所需的清理任务的统计信息。  
  
-   标识用于分析的列，并且对数据建模阶段进行计划。  
  
 [浏览数据&#40;SQL Server 数据挖掘外接程序&#41;](explore-data-sql-server-data-mining-add-ins.md)。  
  
### <a name="detect-and-handle-outliers"></a>检测和处理离群值  
 **离群值**向导关系图中的数据值的分布，并帮助你删除极值。 使用**离群值**以下数据准备任务的工具：  
  
-   基于在数据中发现的模式确定单独值是否可靠。  
  
-   检查异常值并且采取删除或替换它们等操作措施。  
  
-   将某一模型的范围划定到特定的值范围。 例如，如果您知道在某一特定商店中具有离群值，则可以删除该值并且获取更好地预测其他商店的模型。  
  
 [离群值&#40;SQL Server 数据挖掘外接程序&#41;](outliers-sql-server-data-mining-add-ins.md)。  
  
### <a name="relabel-and-bin-data"></a>对数据进行重新标记和装箱  
 **重新标记发生**向导按值分组数据，以便你可以更改数据上的标签。 使用重新标记工具可执行以下数据准备任务：  
  
-   将调查结果中使用的数值代码更改为该数值代码所表示的文本说明。  
  
     例如，您可能替换数据条目（如将“性别 = 1”更换为“性别 = 女”）。  
  
-   箱数据，通过创建组来表示数字范围。  
  
     例如，你可能想要替换的数字的收入列标签如**收入 – 中等**和**收入 – 高**。  
  
-   将离散值折叠为类别。  
  
     例如，如果您有很多单个产品要检测购买模式，可能尝试将产品划分为更宽泛的类别。  
  
 [重新标记发生&#40;SQL Server 数据挖掘外接程序&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>清理数据  
 数据清理包括多种活动，其中大多数活动是由外接程序支持的  
  
-   标识 null 并确定它们是应更改为真实值还是作为 `Missing` 值处理。  
  
-   检测缺失值，然后删除它们或归结相应值，例如均值、null 或其他值。  
  
 [浏览数据&#40;SQL Server 数据挖掘外接程序&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [重新标记发生&#40;SQL Server 数据挖掘外接程序&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [从示例填充](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>示例数据  
 示例数据向导为定型模型和测试模型提供了两种创建平衡数据集的方法。  
  
-   **随机采样。** 使用此选项从较大的数据集提取有代表性的一组数据，以便用于定型或测试。 数据挖掘外接程序使用*分层采样*以确保值的平衡的集获得采样每个变量。  
  
-   **过度采样。** 当您具有的数据比目标结果所需的数据少且需要加大该数据权重时，使用此选项。 例如，欺诈可能相对较少，但是您可以对涉及欺诈的事例过度抽样以便获得建模所需的足够数据。  
  
 [示例数据&#40;SQL Server 数据挖掘外接程序&#41;](sample-data-sql-server-data-mining-add-ins.md)。  
  
## <a name="see-also"></a>请参阅  
 [创建数据挖掘模型](creating-a-data-mining-model.md)   
 [验证模型和使用预测模型&#40;数据挖掘的 Excel 外接程序&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [部署和缩放挖掘模型&#40;数据挖掘的 Excel 外接程序&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  