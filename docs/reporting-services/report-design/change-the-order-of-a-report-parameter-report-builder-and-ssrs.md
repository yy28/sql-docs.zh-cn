---
title: 更改报表参数的顺序（报表生成器）| Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d905dd50fd9001ed3c5b3ad5eaf3016f8f63094f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "77078869"
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>更改报表参数的顺序（报表生成器和 SSRS）
  当依赖参数位于它所依赖的参数之前时，需要更改报表参数的顺序。 当您有级联参数或希望在用户选择其他参数值之前向他们显示参数的默认值时，参数顺序非常重要。 依赖报表参数在其默认值查询或有效值查询中包含对一个查询参数的引用，该查询参数指向  “报表数据”窗格的参数列表中该依赖报表参数之后的报表参数。  
  
 运行报表时，你所看到的报表查看器工具栏上显示参数的顺序由“报表数据”  窗格中参数的顺序以及参数在自定义参数窗格中的位置决定。 有关详细信息，请参阅[自定义报表中的参数窗格（报表生成器）](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-order-of-report-parameters"></a>更改报表参数的顺序  
  
可以通过执行下列其中一项操作，更改报表参数的顺序：  
  
-   单击  “报表数据”窗格中的参数，然后使用向上和向下箭头按钮在列表中上下移动该参数，如下图所示。  更改参数在  “报表数据”窗格中的顺序时，参数窗格中的参数位置也会发生变化。  
  
     ![更改“报表数据”窗格中的参数顺序](../../reporting-services/report-design/media/ssrs-changeorderofparameters-reportdata.png "更改“报表数据”窗格中的参数顺序")  
  
-   在参数窗格中，将参数拖到窗格中的新列或新行。 更改参数在窗格中的位置时，  “报表数据”窗格中的参数顺序也会发生变化。 有关移动窗格中的参数的详细信息，请参阅[自定义报表中的参数窗格（报表生成器）](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)。  
  
## <a name="see-also"></a>另请参阅  
 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [向报表添加级联参数（报表生成器和 SSRS）](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教程：向报表添加参数（报表生成器）](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Parameters 集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
