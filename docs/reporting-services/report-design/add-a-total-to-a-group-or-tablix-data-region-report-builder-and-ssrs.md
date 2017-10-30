---
title: "向组或 Tablix 数据区域 （报表生成器和 SSRS） 添加总计 |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf1b96c3-7f0f-4c94-ad08-5239c77ccfe4
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c9547d7950bc594580194ee27dae65b583616a5c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs"></a>向组或 Tablix 数据区域添加总计（报表生成器和 SSRS）
 在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，可以在 Tablix 数据区域中为组或整个数据区域添加总计。 默认情况下，总计是在应用筛选器之后组或数据区域中的非 Null 数值数据之和。 若要为组添加总计，请在“分组”窗格中单击组快捷菜单上的 **“添加总计”** 。 若要为 Tablix 正文区中的各个单元添加总计，请单击单元快捷菜单上的 **“添加总计”** 。 **添加总计**命令是区分上下文的且仅用于数字字段已启用。 根据选择的 Tablix 单元，您可以通过选择 Tablix 正文区中的单元为一个单元添加总计，也可以通过选择 Tablix 行组区或 Tablix 列组区中的单元为整个组添加总计。 有关 Tablix 区域的详细信息，请参阅 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)。  
  
 添加总计之后，可以将默认函数 Sum 更改为内置报表函数列表中的不同聚合函数。 有关详细信息，请参阅[聚合函数引用 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).[!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-total-for-an-individual-value-in-the-tablix-body-area"></a>为 Tablix 正文区中的单个值添加总计  
  
-   在 Tablix 数据区域正文区中，右键单击要在其中添加总计的单元。 该单元必须包含数字字段。 指向 **“添加总计”**，然后单击 **“行”** 或 **“列”**。  
  
     将在数据区域的当前组之外添加一个新行或列，以及已单击单元中的字段的默认总计。  
  
     如果 Tablix 数据区域是一个表，则自动添加一行。  
  
## <a name="to-add-totals-for-a-row-group"></a>添加行组的总计  
  
-   在 tablix 数据区域行组区域中，右键单击单元格在你想总计行组区域中，依次指向**添加总计**，然后单击**之前**或**后**。  
  
     将在数据区域的当前组之外添加一个新行，然后在该行中为每个数字字段添加默认总计。  
  
## <a name="to-add-totals-for-a-column-group"></a>添加列组的总计  
  
-   在 tablix 数据区域行组区域，右键单击对其的汇总值，然后所指向的列组区域中的单元格**添加总计**，然后单击**之前**或**后**。  
  
     将在数据区域的当前组之外添加一个新列，然后在该列中为每个数字字段添加默认总计。  
  
## <a name="see-also"></a>另请参阅  
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)   
 [Tablix 数据区域 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [表、 矩阵和列表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  

