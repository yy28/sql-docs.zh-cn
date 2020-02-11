---
title: "\"属性对比\" 选项卡（挖掘模型查看器） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.discrimination.f1
ms.assetid: 68323f23-121e-44fc-be85-6f9915d6d3c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7e8d9593cd45ec5a92ea07051fe424698d8ece6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66063125"
---
# <a name="attribute-discrimination-tab-mining-model-viewer"></a>“属性对比”选项卡（挖掘模型查看器）
  可以使用 **“属性对比”** 选项卡，比较输入属性的状态并查看这些状态与结果属性相关的方式。 两个所选的可预测属性状态之间差别最大的属性值会首先列出。  
  
 **有关详细信息**，请查看[Microsoft Naive Bayes 算法](data-mining/microsoft-naive-bayes-algorithm.md)、[使用 microsoft Naive Bayes 查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 从当前挖掘结构的挖掘模型中选择一个挖掘模型。 该挖掘模型将自动在正确的自定义查看器中打开。  
  
 **查看器**  
 选择用于浏览所选挖掘模型的查看器。 对于每个模型，您可以选择自定义查看器或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 挖掘内容查看器。 还可以使用插件查看器（如果有）。  
  
 **Attribute**  
 选择一个可预测属性。  
  
 **值 1**  
 选择可预测属性的状态以与 **“值 2”** 中所包含状态进行比较。  
  
 **值 2**  
 选择可预测属性的状态以与 **“值 1”** 中所包含状态进行比较。 你还可以选择 "**所有其他状态**"，以将**值 1**中的值与其补数（即除值1之外的所有其他值）进行比较。  
  
 **值1的\<对比分数> 和\<值 2>**  
 图形包含以下列，这些列说明了目标属性与输入属性的特定状态关联的方式。  
  
|值|说明|  
|-----------|-----------------|  
|**属性**|挖掘模型中的输入属性。|  
|**值**|
  **“属性”** 中列出的属性的状态。|  
|**优选\<值 1>**|条形指示当前属性和值是否倾向于“值 1” **** 中所选的目标结果。|  
|**优选\<值 2>**|条形指示当前属性和值是否倾向于 **“值 2”** 中所选的目标结果。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器 &#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
