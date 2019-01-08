---
title: 从挖掘模型中排除列 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5643f9795d702aeab95ed92d796c93df3ffcd133
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52397430"
---
# <a name="exclude-a-column-from-a-mining-model"></a>从挖掘模型中排除列
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在创建新的挖掘模型时，您可能不希望使用模型基于的挖掘结构中存在的所有列。 例如，你可能已添加钻取，一个客户名称列，但不想要将该列用于建模。 或者，您可能决定为一个列创建具有不同离散化的多个副本，并且在每个模型中仅使用这些副本中的一个，而忽略其余副本。 您还可以有选择地在若干不同模型中添加输入列，看看所添加的变量是如何影响输出列的。  
  
 您不需要为每个列组合都创建新的挖掘结构；相反，您只需将某个列标记为不在特定的模型中使用。  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>从挖掘模型中排除列  
  
1.  在 **中的数据挖掘设计器的** “挖掘模型” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡中，在有关的挖掘模型下，选择与要排除的列相对应的单元。  
  
2.  从下拉列表框中选择“忽略”。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
