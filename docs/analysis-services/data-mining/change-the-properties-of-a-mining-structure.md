---
title: "更改挖掘结构的属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: mining structures [Analysis Services], properties
ms.assetid: 03b16897-2e36-42b8-9f7d-db1b9b898401
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2f97c94a1c594a341c1e03326c975a080d9033cf
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="change-the-properties-of-a-mining-structure"></a>更改挖掘结构的属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]有两种类型的挖掘结构，可以修改这两种属性：  
  
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
  
  
