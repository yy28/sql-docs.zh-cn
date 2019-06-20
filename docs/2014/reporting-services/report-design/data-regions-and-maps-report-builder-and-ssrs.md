---
title: 数据区域和地图（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data regions
ms.assetid: 3afb8874-b36c-4e44-a0d8-80d2f7135fb1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f0b9722ad68107c626f0b4e569ac6e7cbf8c3bf8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106090"
---
# <a name="data-regions-and-maps-report-builder-and-ssrs"></a>数据区域和地图（报表生成器和 SSRS）
  数据区域是报表中的对象，显示来自报表数据集中的数据。 可以在表、矩阵或列表中以数字和文本形式显示报表数据；在图表或仪表中以图形方式显示报表数据；以及在地图中以地理为背景显示报表数据。 表、矩阵和列表都基于“Tablix  ”数据区域，这种数据区域可根据需要扩展以显示数据集中的所有数据。 Tablix 数据区域支持多个行组和列组，还支持静态和动态的行和列。 图表显示各种图表格式的多个序列和类别组。 仪表显示数据集的单个值或聚合值。 地图会将空间数据显示为地图元素，这些地图元素的外观会根据数据集中的聚合数据而变化。  
  
 您可以将数据区域或地图作为报表部件保存。 [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="table"></a>表  
 “表”是逐行显示数据的数据区域。 表列是静态的：列数是在设计报表时确定的。 表行是动态的：它们向下扩展以容纳数据。 您可以向表添加组，以按照所选的字段或表达式来组织数据。 有关向报表添加表的信息，请参阅[表（报表生成器和 SSRS）](tables-report-builder-and-ssrs.md)。  
  
## <a name="matrix"></a>矩阵  
 “矩阵”也称为交叉表。 矩阵数据区域包含动态列和行，它们都可以扩展以容纳数据。 矩阵可以具有动态列和行及静态列和行。 列或行可以包含其他列或行，并且可用于对数据进行分组。 有关向报表添加矩阵的信息，请参阅[矩阵&#40;报表生成器和 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)  
  
## <a name="list"></a>列表  
 “列表”是一种数据区域，其中的数据以自由格式排列。 您可以排列这些报表项来创建一个窗体，其中的文本框、图像和其他数据区域可以位于列表中的任何位置。 有关向报表添加列表的信息，请参阅[列出了&#40;报表生成器和 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。  
  
## <a name="chart"></a>图表  
 图表以图形方式显示数据。 图表示例包括条形图、饼图和折线图等，并支持其他多种样式。 有关向报表添加图表的信息，请参阅[图表&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)。  
  
## <a name="gauge"></a>测量  
 仪表显示某个范围之内的数据，并且带有一个指向该范围内的某个特定值的指示器。 仪表用于显示关键绩效指标 (KPI) 和其他指标。 仪表包括线性仪表和圆形仪表等。 有关向报表添加仪表的详细信息，请参阅[仪表&#40;报表生成器和 SSRS&#41;](gauges-report-builder-and-ssrs.md)。  
  
## <a name="map"></a>映射  
 地图用于在地理背景下显示数据。 地图数据可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询、ESRI 形状文件或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing 地图图块中的空间数据。 空间数据由一组坐标组成，这些坐标定义用于表示形状或区域的多边形、表示路线或路径的线条以及由标记表示的点。 您可以将聚合数据与地图元素关联，以自动改变其颜色和大小。 例如，您可以基于销售额改变商店的标记类型，也可以基于速度限制改变公路的颜色。 有关详细信息，请参阅[地图（报表生成器和 SSRS）](maps-report-builder-and-ssrs.md)。  
  
## <a name="data-regions-in-the-report-layout"></a>报表布局中的数据区域  
 您可以在报表中添加多个数据区域。 数据区域会扩大以容纳它们链接到的报表数据集数据。 例如，在显示每个产品的销售额的矩阵中，有一个按产品名的行组，和一个按年份的列组。 当您运行报表时，矩阵按每种产品纵向展开页面，按年份横向展开页面。 放置在报表设计图面上矩阵旁边的图表显示在呈现的报表中展开的矩阵的旁边。 数据区域在页面上的呈现方式遵循一组规则，这些规则基于报表的输出格式。 例如，若要帮助控制图表和矩阵在页面上的呈现方式，可以将矩形用作容器或在一个列表中同时嵌套两个数据区域。 有关详细信息，请参阅 [页面布局和呈现方式（报表生成器和 SSRS）](page-layout-and-rendering-report-builder-and-ssrs.md)保存。  
  
## <a name="nested-data-regions"></a>嵌套的数据区域  
 可以将数据区域嵌套在其他数据区域内。 例如，如果要在数据库中为每个销售人员创建一条销售记录，则可以使用文本框和图像创建一个列表，以显示雇员的有关信息，然后在列表中添加表和图表数据区域来显示该雇员的销售记录。 有关详细信息，请参阅 [嵌套数据区域（报表生成器和 SSRS）](nested-data-regions-report-builder-and-ssrs.md)。  
  
## <a name="multiple-data-regions-linked-to-the-same-dataset"></a>链接到同一数据集的多个数据区域  
 可以将多个数据区域链接到同一数据集以提供相同数据的不同视图。 例如，您可以在表和图表中显示相同的数据。 可以创作报表以在表中提供交互式排序按钮，这样，在对表进行排序时，图表也会自动进行排序。 有关详细信息，请参阅 [将多个数据区域链接到同一数据集（报表生成器和 SSRS）](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)。  
  
## <a name="data-for-a-data-region"></a>数据区域的数据  
 每个 Tablix、图表和仪表都设计为显示单个数据集中的数据。 地图显示来自相同或不同数据集的空间数据和分析数据。 还可以通过以下方式，包括未链接到数据区域的数据集中的值：  
  
-   聚合不依赖于排序顺序的值或属于其他数据集范围内的分组。  
  
-   从其他数据集内的名称/值对中查找值。  
  
 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [报表创作概念（报表生成器和 SSRS）](report-authoring-concepts-report-builder-and-ssrs.md)   
 [报表、报表部件和报表定义（报表生成器和 SSRS）](reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [页面布局和呈现方式（报表生成器和 SSRS）](page-layout-and-rendering-report-builder-and-ssrs.md)   
 [教程&#40;报表生成器&#41;](../report-builder-tutorials.md)   
 [Reporting Services 教程 (SSRS)](../reporting-services-tutorials-ssrs.md)  
  
  
