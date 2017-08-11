---
title: "对数据区域 （报表生成器和 SSRS） 中的数据进行排序 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2fcb9be2-1daa-4c92-ad00-5f63cdf39f70
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 01fdabcd4005e5b3b15e6c2656daed1cff499211
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="sort-data-in-a-data-region-report-builder-and-ssrs"></a>对数据区域中的数据排序（报表生成器和 SSRS）
  若要更改报表首次运行时数据区域中数据的排序顺序，必须为数据区域或组设置排序表达式。 默认情况下，组的排序表达式自动设置为与组表达式相同的值。  
  
-   在 Tablix 数据区域中，可以为数据区域或为每个组（包括详细信息组）设置排序表达式。 如果在 Tablix 数据区域中只有一个详细信息组，则可以在查询中、在数据区域上或在详细信息组上定义排序表达式，它们全都有相同的效果。  
  
-   在图表数据区域中，可以为类别组和序列组设置排序表达式，以控制每个组的排序顺序。 图表图例中的颜色顺序由类别组中数据点的排序表达式确定。  
  
-   在仪表数据区域中，您通常不需要对数据进行排序，因为仪表将显示相对于范围的单个值。 如果确实需要对仪表中的数据进行排序，则必须首先定义组，然后设置组的排序表达式。  
  
 有关详细信息，请参阅[对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
 对于 Tablix 数据区域，还可以将交互式排序按钮添加到列标题的顶部，以便让用户能够更改组或详细信息行的排序顺序。 有关详细信息，请参阅[交互式排序（报表生成器和 SSRS）](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-sort-data-in-a-tablix-data-region"></a>对 Tablix 数据区域中的数据进行排序  
  
1.  在设计图面上，右键单击行控点，然后单击“Tablix 属性”。  
  
2.  单击 **“排序”**。  
  
3.  对于每个排序表达式，请按照下列步骤进行操作：  
  
    1.  单击 **“添加”**。  
  
    2.  键入或选择按其对数据进行排序的表达式。  
  
    3.  从“顺序”列下拉列表中，选择每个表达式的排序方向。 **A-Z** 按升序对表达式进行排序。 **Z-A** 按降序对表达式进行排序。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-values-in-a-group-including-the-details-group-for-a-tablix"></a>对 Tablix 的组（包括详细信息组）中的值进行排序  
  
1.  在设计图面上，单击 Tablix 数据区域以将其选中。 “分组”窗格将显示 Tablix 数据区域的行组和列组。  
  
2.  在“行组”窗格中，右键单击组名称，再单击“编辑组”。  
  
3.  在 **“Tablix 组”** 对话框中，单击 **“排序”**。  
  
4.  对于每个排序表达式，请按照下列步骤进行操作：  
  
    1.  单击 **“添加”**。  
  
    2.  键入或选择按其对数据进行排序的表达式。  
  
    3.  从“顺序”列下拉列表中，选择每个表达式的排序方向。 **A-Z** 按升序对表达式进行排序。 **Z-A** 按降序对表达式进行排序。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-x-axis-labels-in-alphabetical-order-on-a-chart"></a>在图表上按字母顺序对 x 轴标签进行排序  
  
1.  右键单击类别字段拖放区域中的某个字段，再单击“类别组属性”。  
  
2.  在 **“类别组属性”** 对话框中，单击 **“排序”**。  
  
3.  对于每个排序表达式，请按照下列步骤进行操作：  
  
    1.  单击 **“添加”**。  
  
    2.  选择与分组字段匹配的表达式。 通过单击 **“分组”**，可以验证分组字段的表达式。  
  
    3.  从“顺序”列下拉列表中，选择每个表达式的排序方向。 **A-Z** 按升序字母顺序对表达式进行排序。 **Z-A** 按降序字母顺序对表达式进行排序。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-the-data-points-in-ascending-or-descending-order-on-a-chart"></a>按升序或降序对图表上的数据点进行排序  
  
1.  右键单击类别字段拖放区域中的某个字段，再单击“类别组属性”。  
  
2.  在 **“类别组属性”** 对话框中，单击 **“排序”**。  
  
3.  对于每个排序表达式，请按照下列步骤进行操作：  
  
    1.  单击 **“添加”**。  
  
    2.  选择与数据字段匹配的表达式。 在大多数情况下，此为聚合值，例如 `=Sum(Fields!Quantity.Value)`。  
  
    3.  从“顺序”列下拉列表中，选择每个表达式的排序方向。 **A-Z** 按升序对表达式进行排序。 **Z-A** 按降序对表达式进行排序。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-data-in-ascending-or-descending-order-for-display-on-a-gauge"></a>按升序或降序对数据进行排序以便显示在仪表上  
  
1.  右键单击仪表，再单击“添加数据组”。  
  
2.  如有必要，在“仪表面板组属性”对话框中，单击“常规”。  
  
3.  在 **“组表达式”**中，单击 **“添加”**。  
  
4.  在 **“分组方式”**中，键入或选择要按其对数据进行分组的表达式。  
  
5.  重复步骤 3 和 4，直到已添加要使用的所有组表达式。  
  
6.  单击 **“排序”**。  
  
7.  对于每个排序表达式，请按照下列步骤进行操作：  
  
    1.  单击 **“添加”**。  
  
    2.  选择与分组字段匹配的表达式。 通过单击 **“分组”**，可以验证分组字段的表达式。  
  
    3.  从“顺序”列下拉列表中，选择每个表达式的排序方向。 **A-Z** 按升序对表达式进行排序。 **Z-A** 按降序对表达式进行排序。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 有关如何在仪表中对数据进行分组的详细信息，请参阅[仪表（报表生成器和 SSRS）](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另请参阅  
 [用于对话框、 窗格和向导的报表生成器帮助](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [图表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [在图表 &#40; 的格式设置轴标签报表生成器和 SSRS &#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [跨多个形状图 &#40; 指定一致的颜色报表生成器和 SSRS &#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
  
