---
title: 将多个数据区域链接到同一数据集（报表生成器）| Microsoft Docs
description: 了解如何在报表生成器中将多个数据区域添加到分页报表以提供同一报表数据集中的数据的不同视图。
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 90c94a91-8fb2-42cb-b998-563691f30d2d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 91a19a2d0e00fc33e7b9e9842c05f8781678a694
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84885260"
---
# <a name="linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs"></a>将多个数据区域链接到同一数据集（报表生成器和 SSRS）

可以将多个数据区域添加到一个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表以提供同一报表数据集中的数据的不同视图。 例如，您可能希望以表的形式显示数据，同时，还希望在图表中以可视化方式显示它。 为此，您必须对相应的筛选表达式、排序表达式和组表达式使用相同的表达式和作用域。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 若要使用图表和表或矩阵显示同一数据，了解表和形状图，以及矩阵和面积图、条形图、柱形图之间的相似之处很有用。 只包含一个行组的表可方便地显示为一个饼图。 随着行组的增加，您可以选择不同类型的图表以最佳方式显示嵌套组。 向饼图添加嵌套行组可增加饼图中的扇区数。 您必须确定父组和子组组合的组实例数是否过多，以致无法在一个饼图中显示。 对于在饼图中显示为小扇形的多个组值，您可以设置一个属性，使低于某一阈值的所有值都显示为一个饼图扇区。 有关详细信息，请参阅[收集饼图上的小切片](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)。  
  
 具有多个行组的表可以显示为一个具有多个类别组的柱形图。 有关详细信息，请参阅[在矩阵和图表上显示相同数据](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)。 有关呈现同一报表数据集的不同视图的表和图表的示例，请参阅 AdventureWorks 报表示例中的 Product Line Sales 报表。 由于表和图表都链接到该报表中的同一数据集，因此，当在对 Top Employees 表排序的过程中单击 Employee Name 的交互式排序按钮时，Top Employees 图表还会自动显示新的排序顺序。 有关下载此示例报表和其他内容的详细信息，请参阅 [报表生成器和报表设计器示例报表](https://go.microsoft.com/fwlink/?LinkId=198283)。  
  
 具有多个行组和列组的矩阵可以使用具有类别组和序列组的面积图、条形图或柱形图以最佳方式显示。 请对矩阵中的列组和图表中的类别组使用相同的组表达式，并对矩阵中的行组和图表中的序列组使用相同的表达式。 必须牢记组实例数影响图表的可读性。 您可以根据范围值定义组，以便减少图表中的组实例数。 有关详细信息，请参阅[组表达式示例](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)。  
  
## <a name="next-steps"></a>后续步骤

[图表](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[表、矩阵和列表](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
[嵌套的数据区域](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)  

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
