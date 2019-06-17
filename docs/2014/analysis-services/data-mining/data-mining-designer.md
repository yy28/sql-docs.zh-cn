---
title: 数据挖掘设计器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], structure
- mining structures [Analysis Services], modifying
- data mining editor [Analysis Services]
- Data Mining Designer
- data mining [Analysis Services], modifying
ms.assetid: 2540db5b-2bf3-4b6c-87c8-79c48d71acce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b0a54a0ae2bab2c8019b706a51b94f0338dcb3cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085112"
---
# <a name="data-mining-designer"></a>Data Mining Designer
  数据挖掘设计器是在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中使用挖掘模型的主要环境。 您可以通过选择一个现有挖掘结构或使用数据挖掘向导创建一个新的挖掘结构和挖掘模型来访问该设计器。 可以使用数据挖掘设计器执行以下任务：  
  
-   修改最初由数据挖掘向导创建的挖掘结构和挖掘模型。  
  
-   根据现有的挖掘结构创建新模型。  
  
-   定型和浏览挖掘模型。  
  
-   通过使用准确性图表比较模型。  
  
-   根据挖掘模型创建预测查询。  
  
## <a name="mining-structure-tab"></a>“挖掘结构”选项卡  
 使用 **“挖掘结构”** 选项卡添加列和修改现有挖掘结构的属性。 下列任务和主题提供有关使用挖掘结构的详细信息：  
  
 [挖掘结构（Analysis Services - 数据挖掘）](mining-structures-analysis-services-data-mining.md)  
  
 [挖掘结构任务和操作指南](mining-structure-tasks-and-how-tos.md)  
  
## <a name="mining-models-tab"></a>“挖掘模型”选项卡  
 使用 **“挖掘模型”** 选项卡可管理现有的挖掘模型以及创建新模型。 挖掘模型始终基于现有挖掘结构。  
  
 在“挖掘模型”  选项卡中，可以更改算法类型、添加或删除与模型结构关联的列、调整算法特定的列属性、指定挖掘模型列用法以及调整与挖掘模型关联的算法参数。 还可以将挖掘结构与所选模型或所有关联模型一起处理。  
  
 有关使用挖掘模型的详细信息，请参阅下列主题：  
  
 [挖掘模型（Analysis Services - 数据挖掘）](mining-models-analysis-services-data-mining.md)  
  
 [挖掘模型任务和操作指南](mining-model-tasks-and-how-tos.md)  
  
## <a name="mining-model-viewer-tab"></a>“挖掘模型查看器”选项卡  
 使用 **“挖掘模型查看器”** 选项卡以可视化方式浏览挖掘模型。 每个挖掘模型都与显示特定于该模型的内容的一个自定义查看器相关联。 还可以使用内容查看器查看挖掘模型内容。  
  
 有关使用数据挖掘查看器浏览挖掘模型的详细信息，请参阅下列主题：  
  
 [数据挖掘模型查看器](data-mining-model-viewers.md)  
  
 [挖掘模型查看器任务和操作指南](mining-model-viewer-tasks-and-how-tos.md)  
  
## <a name="mining-accuracy-chart-tab"></a>“挖掘准确性图表”选项卡  
 使用 **“挖掘准确性图表”** 选项卡测试单个挖掘模型的预测准确性，或比较挖掘结构中包含的多个挖掘模型的效率。 该选项卡包含用于筛选数据、选择挖掘模型以及在提升图、利润图或分类矩阵中显示结果的工具。  
  
 有关测试和验证挖掘模型的详细信息，请参阅下列主题：  
  
 [测试和验证（数据挖掘）](testing-and-validation-data-mining.md)  
  
 [测试和验证任务和操作指南（数据挖掘）](testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
## <a name="mining-model-prediction-tab"></a>“挖掘模型预测”选项卡  
 “挖掘模型预测”  选项卡包含预测查询生成器，可以使用此生成器创建数据挖掘扩展插件 (DMX) 预测查询。 该选项卡包含用于指定挖掘模型和输入表、将挖掘模型中的列映射到输入表中的列、向查询中添加函数以及为各个列指定条件的工具。  
  
 设计查询后，可以使用该选项卡中的不同视图来显示查询结果并手动修改查询。 还可以将查询结果保存到数据库中的表。  
  
 有关创建数据挖掘查询的详细信息，请参阅下列主题：  
  
 [数据挖掘查询](data-mining-queries.md)  
  
 [数据挖掘查询任务和操作指南](data-mining-query-tasks-and-how-tos.md)  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘解决方案](data-mining-solutions.md)  
  
  
