---
title: "更改报表参数 （报表生成器和 SSRS） 的顺序 |Microsoft 文档"
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
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3377e943ddf7d8c7bd06aeab52ee263a754af25c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>更改报表参数的顺序（报表生成器和 SSRS）
  当依赖参数位于它所依赖的参数之前时，需要更改报表参数的顺序。 当您有级联参数或希望在用户选择其他参数值之前向他们显示参数的默认值时，参数顺序非常重要。 依赖报表参数在其默认值查询或有效值查询中包含对一个查询参数的引用，该查询参数指向  “报表数据”窗格的参数列表中该依赖报表参数之后的报表参数。  
  
 运行报表时，你所看到的报表查看器工具栏上显示参数的顺序由“报表数据”  窗格中参数的顺序以及参数在自定义参数窗格中的位置决定。 有关详细信息，请参阅[自定义报表 &#40; 中的参数窗格报表生成器 &#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-order-of-report-parameters"></a>更改报表参数的顺序  
  
可以通过执行下列其中一项操作，更改报表参数的顺序：  
  
-   单击  “报表数据”窗格中的参数，然后使用向上和向下箭头按钮在列表中上下移动该参数，如下图所示。  更改参数在  “报表数据”窗格中的顺序时，参数窗格中的参数位置也会发生变化。  
  
     ![更改报表数据窗格中的参数的顺序](../../reporting-services/report-design/media/ssrs-changeorderofparameters-reportdata.png "更改报表数据窗格中的参数的顺序")  
  
-   在参数窗格中，将参数拖到窗格中的新列或新行。 更改参数在窗格中的位置时，  “报表数据”窗格中的参数顺序也会发生变化。 有关移动在窗格中的参数的详细信息，请参阅[自定义报表 &#40; 中的参数窗格报表生成器 &#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
## <a name="see-also"></a>另請參閱  
 [报表参数 &#40;报表生成器和报表设计器 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [用于对话框、 窗格和向导的报表生成器帮助](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [将级联参数添加到报表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教程： 将参数添加到您的报表 &#40;报表生成器 &#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [添加数据集筛选器、 数据区域筛选器和组筛选器 （&） #40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [参数的集合引用 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
