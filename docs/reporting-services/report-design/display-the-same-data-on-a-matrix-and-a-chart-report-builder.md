---
title: 在矩阵和图表上显示相同数据（报表生成器）| Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 1262f283-9fc2-4bc1-9c79-457f7642abc7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f3eafaec96e27d6e78521b0c4ef7580af103a12e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792245"
---
# <a name="display-the-same-data-on-a-matrix-and-a-chart-report-builder"></a>在矩阵和图表上显示相同数据（报表生成器）
  如果希望在矩阵和图表中显示相同数据，则必须将两个数据区域的属性都设置为指定相同数据集，而且还要为筛选器、组、排序和数据指定相同表达式。  
  
 由于两个数据区域的数据将有相同的祖先（报表数据集），因此在向矩阵添加交互式排序按钮之后，当用户单击该按钮时它会同时更改矩阵和图表的排序顺序。 有关详细信息，请参阅 [将交互式排序添加到表或矩阵（报表生成器和 SSRS）](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)。  
  
 若要使用矩阵列组值作为图表的图例，必须指定图表上序列数据的颜色，然后使用与填充颜色相同的颜色作为用于显示组值的矩阵单元中文本框的背景色。 有关详细信息，请参阅[对多个形状图指定一致的颜色（报表生成器和 SSRS）](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)。  
  
 在运行时，如果组定义中有太多组值，则报表可能显得很混乱。 您可能需要筛选值、组合组或调整阈值，以便图表为您组合组。 有关详细信息，请参阅 [将多个数据区域链接到同一数据集（报表生成器和 SSRS）](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-matrix-and-chart-to-display-the-same-data"></a>添加矩阵和图表以显示相同数据  
  
1.  在设计视图中打开报表。  
  
2.  在 **“插入”** 选项卡的 **“数据区域”** 组中，单击 **“矩阵”**，然后单击报表正文或报表正文中的矩形。 将在报表中添加一个矩阵。  
  
3.  在 **“插入”** 选项卡的 **“数据区域”** 组中，单击 **“图”**，然后选择图表类型。 将在报表中添加一个图表。  
  
4.  （可选）在“插入”选项卡的“报表项”组中，单击“矩形”，然后单击报表。 将在报表中添加一个矩形。 将步骤 2 和 3 中的矩阵和图表拖到该矩形中。  
  
     通过在矩形容器中放入多个数据区域，可以帮助控制当您查看报表时如何呈现矩阵和图表。  
  
     在后面几个步骤中，将选择要在矩阵中显示和在图表中显示的相同数据集字段。  
  
5.  从“报表数据”窗格中，将数值数据集字段拖到矩阵中的数据单元。  
  
     默认情况下，将使用聚合函数 Sum 计算组值。 如果更改矩阵中的聚合函数，还必须在图表中进行更改。  
  
6.  在矩阵中，右键单击包含数据的单元，单击“文本框属性”，再单击“数字”。 为数据集字段值选择适当的格式。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  将在步骤 3 中选择的相同数据集字段拖到图表上的 **“值”** 区域中。  
  
9. 在图表中，右键单击 Y 轴，单击“轴属性”，再单击“数字”。 为在步骤 4 中选择的数据选择相同格式。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     在后面几个步骤中，需要将矩阵行组和图表序列组设置为相同表达式，而且还要设置图表序列组的排序顺序。  
  
11. 从“报表数据”窗格中，将要按其为矩阵行分组的数据集字段拖到“行组”窗格。  
  
     默认情况下，矩阵行组会添加与组表达式相同的排序表达式。  
  
12. 将在步骤 9 中使用的相同数据集字段拖到图表的 **“序列组”** 区域。  
  
13. 在“序列组”区域中右键单击该组，然后单击“序列组属性”。  
  
14. 单击 **“排序”**。  
  
15. 单击 **“添加”**。 将在排序表达式网格中出现一个新行。  
  
16. 在“排序依据”中，从下拉列表选择在步骤 9 中选择要按其分组的数据集字段。  
  
17. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     在后面几个步骤中，需要将矩阵列组和图表类别组设置为相同表达式，而且还要设置图表类别组的排序顺序。  
  
18. 从“报表数据”窗格中，将要按其为矩阵列分组的数据集字段拖到“列组”窗格。  
  
     默认情况下，矩阵列组会添加与组表达式相同的排序表达式。  
  
19. 将在步骤 16 中使用的相同数据集字段拖到图表的 **“类别组”** 区域。  
  
20. 在“类别组”区域中右键单击该组，然后单击“类别组属性”。  
  
21. 单击 **“排序”**。  
  
22. 单击 **“添加”**。 将在排序表达式网格中出现一个新行。  
  
23. 在“排序依据”中，从下拉列表选择在步骤 16 中选择要按其分组的数据集字段。  
  
24. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
25. 预览结果。 矩阵行组和列组将显示与图表序列组和类别组相同的数据。  
  
## <a name="see-also"></a>另请参阅  
 [将多个数据区域链接到同一数据集（报表生成器和 SSRS）](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [图表&#40;报表生成器和 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
