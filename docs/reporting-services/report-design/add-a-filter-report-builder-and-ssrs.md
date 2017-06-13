---
title: "添加筛选器 （报表生成器和 SSRS） |Microsoft 文档"
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
ms.assetid: 10ae54e7-0e8a-4dff-995d-05516c51d076
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 088e219e120eeb6b4608db9379811caf1b5406cd
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="add-a-filter-report-builder-and-ssrs"></a>添加筛选器（报表生成器和 SSRS）
  如果您希望在计算或显示时包含或排除特定值，可向数据集、数据区域或组添加筛选器。 在运行时应用筛选器的顺序为：先对数据集，再对数据区域，最后对组，并按照组层次结构自上而下的顺序。 在表、矩阵或列表中，对行组、列组和相邻组分别应用各自的筛选器。 在图表中，对类别组和序列组分别应用各自的筛选器。  
  
 若要添加筛选器，必须指定一个或多个筛选器公式。 筛选器公式由标识了要筛选的数据的表达式、运算符和要比较的值组成。 所筛选数据的数据类型和值必须匹配。 不支持筛选数据集或数据区域的聚合值。  
  
 若要筛选图表中的数据点，可以对类别组或序列组设置筛选器。 默认情况下，图表使用内置函数 Sum 将属于同一组的值聚合到序列中的单个数据点中。 如果更改序列的聚合函数，则必须更改筛选表达式中的聚合函数。  
  
 有关筛选嵌入式数据集和共享数据集的详细信息，请参阅[向数据集添加筛选器（报表生成器和 SSRS）](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-filter-on-a-data-region"></a>对数据区域设置筛选器  
  
1.  在 **“设计”** 视图中打开报表。  
  
2.  选择设计图面上的数据区域，然后右键单击*\<数据区域 >***属性**。 对于仪表，选择 **“仪表面板属性”**。 *\<数据区域 >***属性**对话框随即打开。  
  
    > [!NOTE]  
    >  在 Tablix 数据区域上，右键单击角部单元格或行或列的控点，然后单击“Tablix 属性”。  
  
3.  单击 **“筛选器”**。 此时将显示当前筛选器公式的列表。 默认情况下，此列表是空的。  
  
4.  单击 **“添加”**。 此时将显示一个新的空白筛选器公式。  
  
5.  在 **“表达式”**中，键入或选择要筛选的字段的表达式。 若要编辑该表达式，请单击表达式 (*fx*) 按钮。  
  
6.  从下拉框中选择与您在步骤 5 中创建的表达式的数据类型相匹配的数据类型。  
  
7.  在 **“运算符”** 框中，选择一个供筛选器使用的运算符，以比较 **“表达式”** 框和 **“值”** 框中的值。 您所选择的运算符将决定下一步中使用的值数。  
  
8.  在 **“值”** 框中，键入筛选器对 **“表达式”**中的值进行比较时的目标表达式或值。  
  
     有关筛选器公式的示例，请参阅[筛选器公式示例（报表生成器和 SSRS）](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-tablix-row-or-column-group"></a>对 Tablix 行或列组设置筛选器  
  
1.  在 **“设计”** 视图中打开报表。  
  
2.  右键单击设计图面上的表、矩阵或列表数据区域以将其选中。 “分组”窗格将显示所选项的组。  
  
3.  在“分组”窗格中，右键单击组，然后单击“编辑组”。 此时将打开 **“Tablix 组”** 对话框。  
  
4.  单击 **“筛选器”**。 此时将显示当前筛选器公式的列表。 默认情况下，此列表是空的。  
  
5.  单击 **“添加”**。 此时将显示一个新的空白筛选器公式。  
  
6.  在 **“表达式”**中，键入或选择要筛选的字段的表达式。 若要编辑该表达式，请单击表达式 (*fx*) 按钮。  
  
7.  从下拉框中选择与您在步骤 5 中创建的表达式的数据类型相匹配的数据类型。  
  
8.  在 **“运算符”** 框中，选择一个供筛选器使用的运算符，以比较 **“表达式”** 框和 **“值”** 框中的值。 您所选择的运算符将决定下一步中使用的值数。  
  
9. 在 **“值”** 框中，键入筛选器对 **“表达式”**中的值进行比较时的目标表达式或值。  
  
     有关筛选器公式的示例，请参阅[筛选器公式示例（报表生成器和 SSRS）](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-chart-category-group"></a>对图表类别组设置筛选器  
  
1.  在 **“设计”** 视图中打开报表。  
  
2.  在设计图面上，单击图表两次以调出数据、序列和类别字段放置区。  
  
3.  右键单击包含在类别字段放置区中的字段，然后选择“类别组属性”。  
  
4.  单击 **“筛选器”**。 此时将显示当前筛选器公式的列表。 默认情况下，此列表是空的。  
  
5.  单击 **“添加”**。 此时将显示一个新的空白筛选器公式。  
  
6.  在 **“表达式”**中，键入或选择要筛选的字段的表达式。 若要编辑该表达式，请单击表达式 (*fx*) 按钮。  
  
7.  从下拉框中选择与您在步骤 5 中创建的表达式的数据类型相匹配的数据类型。  
  
8.  在 **“运算符”** 框中，选择一个供筛选器使用的运算符，以比较 **“表达式”** 框和 **“值”** 框中的值。 您所选择的运算符将决定下一步中使用的值数。  
  
9. 在 **“值”** 框中，键入筛选器对 **“表达式”**中的值进行比较时的目标表达式或值。  
  
     有关筛选器公式的示例，请参阅[筛选器公式示例（报表生成器和 SSRS）](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-chart-series-group"></a>对图表序列组设置筛选器  
  
1.  在 **“设计”** 视图中打开报表。  
  
2.  在设计图面上，单击图表两次以调出数据、序列和类别字段放置区。  
  
3.  右键单击包含在序列字段放置区中的字段，然后选择“序列组属性”。  
  
4.  单击 **“筛选器”**。 此时将显示当前筛选器公式的列表。 默认情况下，此列表是空的。  
  
5.  单击 **“添加”**。 此时将显示一个新的空白筛选器公式。  
  
6.  在 **“表达式”**中，键入或选择要筛选的字段的表达式。 若要编辑该表达式，请单击表达式 (*fx*) 按钮。  
  
7.  从下拉框中选择与您在步骤 5 中创建的表达式的数据类型相匹配的数据类型。  
  
8.  在 **“运算符”** 框中，选择一个供筛选器使用的运算符，以比较 **“表达式”** 框和 **“值”** 框中的值。 您所选择的运算符将决定下一步中使用的值数。  
  
9. 在 **“值”** 框中，键入筛选器对 **“表达式”**中的值进行比较时的目标表达式或值。  
  
     有关筛选器公式的示例，请参阅[筛选器公式示例（报表生成器和 SSRS）](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [仪表（报表生成器和 SSRS）](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
