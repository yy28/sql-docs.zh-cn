---
title: 更改挖掘结构的属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], properties
ms.assetid: 03b16897-2e36-42b8-9f7d-db1b9b898401
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c9ca227753b8ebbd80d4de0c672fc8cab5c1b56
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66085855"
---
# <a name="change-the-properties-of-a-mining-structure"></a>更改挖掘结构的属性
  有两种针对挖掘结构的属性，这两种属性均可以修改：  
  
-   影响整个结构的挖掘结构属性  
  
-   针对结构中的单个列的属性  
  
 请注意，有些属性依赖于其他属性设置。 例如，在您将列的数据类型设置为 `Discretized` 之前，不能设置控制绑定行为的属性（例如 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 或 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A>）。  
  
 有关挖掘结构属性的详细信息，请参阅 [挖掘结构列](mining-structure-columns.md)。  
  
### <a name="to-change-the-properties-of-a-mining-structure"></a>更改挖掘结构的属性  
  
1.  在数据挖掘设计器中的“挖掘结构”选项卡上，右键单击挖掘结构或挖掘结构中的一列，然后选择“属性”。  
  
     此时将在屏幕右侧打开 **“属性”** 窗口（如果该窗口尚未可见）。  
  
2.  在 **“属性”** 窗口中，选择与要更改属性相对应的值，然后输入新的值。  
  
     在设计器中选择一个不同的元素后，新值即生效。  
  
## <a name="see-also"></a>请参阅  
 [挖掘结构任务和操作指南](mining-structure-tasks-and-how-tos.md)  
  
  
