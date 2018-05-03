---
title: 更改挖掘结构的属性 |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6aabe9c70442843797d3d27dd8415c2b2b040691
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="change-the-properties-of-a-mining-structure"></a>更改挖掘结构的属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  有两种针对挖掘结构的属性，这两种属性均可以修改：  
  
-   影响整个结构的挖掘结构属性  
  
-   针对结构中的单个列的属性  
  
 请注意，有些属性依赖于其他属性设置。 例如，在将列的数据类型设置为 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 之前，不能设置控制绑定行为的属性（例如 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A>或 **DiscretizationBucketCount**）。  
  
 有关挖掘结构属性的详细信息，请参阅 [挖掘结构列](../../analysis-services/data-mining/mining-structure-columns.md)。  
  
### <a name="to-change-the-properties-of-a-mining-structure"></a>更改挖掘结构的属性  
  
1.  在数据挖掘设计器中的“挖掘结构”选项卡上，右键单击挖掘结构或挖掘结构中的一列，然后选择“属性”。  
  
     此时将在屏幕右侧打开 **“属性”** 窗口（如果该窗口尚未可见）。  
  
2.  在 **“属性”** 窗口中，选择与要更改属性相对应的值，然后输入新的值。  
  
     在设计器中选择一个不同的元素后，新值即生效。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘结构任务和操作指南](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
