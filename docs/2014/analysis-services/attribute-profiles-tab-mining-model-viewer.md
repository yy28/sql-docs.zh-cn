---
title: 属性配置文件选项卡 （挖掘模型查看器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.profiles.f1
ms.assetid: 17c7e7ae-273c-4a6b-9a35-e8b9b8e65999
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b2bb75ec06d9b5c14ce5c2dcc85561412b362b40
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063173"
---
# <a name="attribute-profiles-tab-mining-model-viewer"></a>“属性配置文件”选项卡（挖掘模型查看器）
  可以使用 **“属性配置文件”** 选项卡，来查看 Naive Bayes 模型状态中输入值的分布如何生成结果属性的每个状态。 值的分布会显示为一个彩色直方图且所有分布都以表格格式显示，以便能更轻松地比较值。  
  
 **有关详细信息：**[Microsoft Naive Bayes 算法](data-mining/microsoft-naive-bayes-algorithm.md)，[使用 Microsoft Naive Bayes 查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 从当前挖掘结构的挖掘模型中选择一个挖掘模型以进行查看。 挖掘模型将在其关联的查看器中打开。  
  
 **Viewer**  
 选择用于浏览所选挖掘模型的查看器。 可以选择为每个挖掘模型提供的自定义查看器或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 挖掘内容查看器。 还可以使用插件查看器（如果有）。  
  
 **显示图例**  
 选择此选项可显示一个键，该键将“状态”中的每个值与分布图表中使用的一种颜色匹配。  
  
 **直方图条数**  
 选择要在直方图中包含多少个图条。 如果存在的图条数多于您选择显示的图条数，则会保留重要性最高的那些图条，其余图条则组合到 **“其他”** 中。  
  
 **可预测**  
 从挖掘模型中选择可预测列。  
  
 **属性配置文件**  
 该表包含以下列：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**属性**|列出挖掘模型中包含的挖掘模型列。|  
|**状态**|一个说明相应属性行中的颜色所表示的状态的可选列。 通过使用 **“显示图例”** 复选框进行添加或删除。|  
|**人口数**|显示属性在整个数据集中的分布情况。|  
|**可预测属性的状态列**|为可预测列的每个状态显示一列，其中每一行对应于模型中的一个输入属性。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器（数据挖掘模型设计器）](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
