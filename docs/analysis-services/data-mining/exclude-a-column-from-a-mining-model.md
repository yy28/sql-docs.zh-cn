---
title: "从挖掘模型中排除列 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d9e175dde4ca78636c909b20e3898ee582f1adb9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="exclude-a-column-from-a-mining-model"></a>从挖掘模型中排除列
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]当你创建新的挖掘模型时，你可能不想要使用模型所基于的挖掘结构中存在的所有列。 例如，您可能添加了一个客户名称列来用于钻取，但不想将该列用于建模。 或者，您可能决定为一个列创建具有不同离散化的多个副本，并且在每个模型中仅使用这些副本中的一个，而忽略其余副本。 您还可以有选择地在若干不同模型中添加输入列，看看所添加的变量是如何影响输出列的。  
  
 您不需要为每个列组合都创建新的挖掘结构；相反，您只需将某个列标记为不在特定的模型中使用。  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>从挖掘模型中排除列  
  
1.  在 **中的数据挖掘设计器的** “挖掘模型” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡中，在有关的挖掘模型下，选择与要排除的列相对应的单元。  
  
2.  从下拉列表框中选择“忽略”。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
