---
title: 对数据进行筛选、分组和排序（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.categorygroupproperties.general.f1
- "10403"
- sql13.rtp.rptdesigner.categorygroupproperties.sorting.f1
- sql13.rtp.rptdesigner.seriesgroupproperties.general.f1
- "10402"
- "10410"
- sql13.rtp.rptdesigner.seriesgroupproperties.sorting.f1
- "10412"
ms.assetid: 4dda2a7f-3f31-47e9-a88b-28d770ebd65e
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c2173ba773d10cb443c3c8b973cd64cd453ce567
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="filter-group-and-sort-data-report-builder-and-ssrs"></a>对数据进行筛选、分组和排序（报表生成器和 SSRS）
  在报表中，可以使用表达式来帮助对报表数据进行控制、组织和排序。 默认情况下，当您创建数据集和设计报表布局时，报表项的属性会基于数据集字段、参数以及显示在“报表数据”窗格中的其他项自动设置为表达式。 您还可向表或矩阵单元添加交互式排序按钮，以便用户能够通过交互方式，更改组或组内的行的行排序顺序。  
  
-   **筛选表达式** 筛选表达式基于您指定的比较来测试数据，以确定包含或排除这些数据。 在通过数据连接检索数据之后，筛选器将应用于报表中的数据。 您可向以下项添加筛选器的任意组合：报表服务器上的共享数据集定义；报表中的共享数据集实例或嵌入数据集；数据区域（例如表或图表）；数据区域组（例如表中的行组或图表中的类别组）。  
  
-   **组表达式** 组表达式可以基于数据集字段或其他值来组织数据。 组表达式是在您生成报表布局时自动创建的。 在将筛选器应用于数据之后，或者在合并报表数据和数据区域时，报表处理器会对组表达式进行计算。 您可在创建组表达式之后对其进行自定义。  
  
-   **排序表达式** 排序表达式控制数据在数据区域中的显示顺序。 排序表达式是在您生成报表布局时自动创建的。 默认情况下，组的排序表达式设置为与组表达式相同的值。 您可在创建排序表达式之后对其进行自定义。  
  
-   **交互式排序** 若要让用户能够对列进行排序，或反向切换列的排序顺序，您可向表或矩阵中的列标题或组头单元添加一个交互式排序按钮。  
  
 若要帮助用户自定义筛选表达式、组表达式或排序表达式，您可以更改表达式，添加对报表参数的引用。 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)的详细信息。  
  
 有关详细信息和示例，请参阅下列主题：  
  
-   [组表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
-   [筛选器公式示例（报表生成器和 SSRS）](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [报表生成器教程](../../reporting-services/report-builder-tutorials.md)  
  
-   [Reporting Services 教程 (SSRS)](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
-   [报表示例（报表生成器和 SSRS）](http://go.microsoft.com/fwlink/?LinkId=198283)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Filtering"></a> 对报表中的数据进行筛选  
 筛选器是报表的部件，可在通过数据连接检索报表数据后，帮助控制这些数据。 如果您无法将数据集查询更改为在从外部数据源检索数据之前筛选数据，则需要使用筛选器。  
  
 在可能的情况下，请生成仅返回需要显示在报表中的数据的数据集查询。 如果您减少了必须检索和处理的数据量，则会有助于提高报表性能。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
 在从外部数据源检索数据之后，您可以向数据集、数据区域和数据区域组（包括详细信息组）添加筛选器。 在运行时应用筛选器的顺序为：先对数据集，再对数据区域，最后对组，并按照组层次结构自上而下的顺序。 在表、矩阵或列表中，对行组、列组和相邻组分别应用各自的筛选器。 在图表中，对类别组和序列组分别应用各自的筛选器。 有关详细信息，请参阅 [添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)。  
  
 对于每个筛选器，需要指定一个“筛选器公式” 。 筛选器公式包括数据集字段或表达式，用于指定要筛选的数据、运算符以及要比较的值。 在处理项时，只包括与筛选条件匹配的数据值。  
  
 若要让用户能够控制报表中的数据，可以在筛选表达式中包括相应参数。 有关详细信息，请参阅[集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)。  
  
 若要为每个用户自定义视图，可在筛选器中包含对内置 UserID 字段的引用。 有关详细信息，请参阅[内置的全局和用户引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。  
  
  
##  <a name="Grouping"></a> 对报表中的数据进行分组  
 组可以组织报表中的数据，以便显示这些数据或计算聚合值。 了解如何定义组和使用组功能，有助于您设计更简洁的报表。  
  
 组表达式是在您执行以下操作时自动创建的：  
  
-   在表、矩阵和图表向导中排列数据集字段，或在地图向导中匹配字段。  
  
-   在表、矩阵或列表中，向“分组”窗格的“行组”或“列组”区域添加字段。  
  
-   在图表中，向“图表数据”窗格的“类别组”或“序列组”区域添加字段。  
  
-   在地图中，指定一个字段，用于将地图元素与“层数据”上下文菜单项中的分析数据匹配。  
  
 组是报表定义的一部分。 每个组都有一个名称。 默认情况下，组名就是它所基于的数据集字段。  
  
 在表或矩阵数据区域内，可以创建多个行组和列组。 可以通过组织嵌套组、相邻组和递归层次结构组（例如组织图），在直观的层次结构中显示数据。  
  
 组名标识表达式作用域。 可将组名指定为要在其中计算聚合的作用域，以便按层次结构方式组织数据，并切换明细报表中父节点的子节点的显示；在多个数据区域中显示相同数据的不同视图；在表、矩阵、图表、仪表或地图中可视化摘要数据。 有关详细信息，请参阅 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 若要根据若干数据集字段进行分组，请将每个字段添加到组表达式集合。 您还可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]中编写您自己的组表达式。 例如，您可以按照值范围进行分组，或者通过使用报表参数使用户能够选择对数据区域中的数据进行分组的方式。 有关详细信息，请参阅 [组表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)。  
  
 在报表显示方面，可以在各组或组的每个实例前后添加分页符，以减少每页中的数据量，帮助管理报表呈现性能。 有关详细信息，请参阅[添加分页符（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md)。  
  
 创建数据区域组是在报表中组织数据的方式之一。 可以通过多种方式组织数据，每种方式都具有自身的优势。 有关详细信息，请参阅 [钻取、深化、子报表和嵌套数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)。  
  
### <a name="defining-group-variables"></a>定义组变量  
 定义组时，可以创建一个组变量，在以组为作用域并且可以从嵌套组访问的表达式中使用。 组变量对于每个组实例进行一次计算，并且可从子组中的表达式访问。 例如，对于按区域或子区域分组的数据，可以针对每个区域计算税收，并在子区域组的计算中使用该税收值。  
  
 有关详细信息，请参阅 [报表和组变量集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md) 和 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
### <a name="groups-and-scope-in-data-regions"></a>数据区域中的组和作用域  
 若要提供同一数据集的数据的多个视图，可为每个数据区域指定相同的组表达式。 例如，可以在表中显示分类数据，以显示所有详细数据，而在饼图中显示聚合，帮助直观地显示每个类别与整个数据集的关系。 有关详细信息，请参阅 [将多个数据区域链接到同一数据集（报表生成器和 SSRS）](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)。  
  
 当您在表、矩阵或列表中的某个单元嵌套一个数据区域时，会自动将数据的作用域设置为单元最内部的组成员。 例如，假定您将图表添加到同时位于行组和列组内的单元中。 在运行时，对该图表可用的数据将以最内部行组实例和最内部列组实例作为作用域。 有关详细信息，请参阅 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
  
##  <a name="Sorting"></a> 对报表中的数据进行排序  
 若要控制报表中数据的排序顺序，您可以在数据集查询中对数据进行排序，或者为数据区域或组定义排序表达式。 您也可以向表和矩阵添加交互式排序按钮，以便用户能够更改行的排序顺序。  
  
 所有三种排序类型均可在同一报表中组合使用。 默认情况下，排序顺序取决于数据集查询返回数据的顺序。 排序表达式应用于数据区域和数据区域组。 交互式排序在排序表达式后应用。  
  
 对于包含聚合函数的表达式，大多数结果不受排序顺序的影响。 聚合函数 First、Last 和 Previous 的返回值会受到排序顺序的影响。 有关详细信息，请参阅 [聚合函数引用（报表生成器和 SSRS）](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)。  
  
### <a name="sorting-data-in-a-dataset-query"></a>在数据集查询中对数据进行排序  
 在数据集查询中包括排序顺序可在为报表检索数据之前对数据进行预排序。 通过在查询中对数据进行排序，排序工作将由数据源而非报表处理器完成。  
  
 对于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源类型，您可以向数据集查询添加 ORDER BY 子句。 例如，以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询对表 SalesOrders 中的 Sales 和 Region 列按 Sales 进行降序排序： `SELECT Sales, Region FROM SalesOrders ORDER BY Sales DESC`。 有关详细信息，请参阅 [SQL Server 联机丛书](http://go.microsoft.com/fwlink/?linkid=98335)中的“用 ORDER BY 对行进行排序”。  
  
> [!NOTE]  
>  并非所有数据源都支持在查询中指定排序顺序的功能。  
  
### <a name="sorting-data-with-sort-expressions"></a>使用排序表达式对数据进行排序  
 若要在从数据源中检索报表数据之后对其进行排序，您可以对 Tablix 数据区域或组（包括详细信息组）设置排序表达式。 以下列表说明了对不同项设置排序表达式的效果：  
  
-   **Tablix 数据区域。** 对表、矩阵或列表数据区域设置排序表达式，可在运行时应用数据集筛选器和数据区域筛选器之后控制数据区域中数据的排序顺序。  
  
-   **Tablix 数据区域组。** 为包括详细信息组在内的每个组设置排序表达式，可控制组实例的排序顺序。 例如，对于详细信息组，可控制详细信息行的顺序。 对于子组，可控制父组内子组的组实例的顺序。 默认情况下，创建组时，排序表达式将设置为组表达式和升序。  
  
     如果您只拥有一个详细信息组，则可以在查询中对数据区域或详细信息组定义排序表达式以获得相同效果。  
  
-   **图表数据区域。** 为类别和序列组设置排序表达式，可控制数据点的排序顺序。 默认情况下，数据点的顺序也是图表图例中颜色的顺序。 有关详细信息，请参阅 [设置图表上序列颜色的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)。  
  
-   **地图报表项。** 您通常不需要对地图数据区域的数据进行排序，因为地图组数据将在地图元素上显示。  
  
-   **仪表数据区域。** 您通常不需要对仪表数据区域的数据进行排序，因为仪表显示相对于某一范围的单一值。 如果不需要在仪表中对数据进行排序，您首先必须定义一个组，然后为该组设置一个排序表达式。  
  
#### <a name="sorting-by-a-different-value"></a>按不同值排序  
 您可能希望在数据区域中按照字段值以外的其他值对行进行排序。 例如，假定“Size”字段包括多个文本值，分别对应于小、中、大和超大。 默认情况下，基于“Size”行组的排序表达式也是 [Size]。 为了更好地控制数据排序方式，可向定义所需排序顺序的数据集查询添加字段。  
  
 或者，也可以定义一个数据集，仅包括大小值和一个指定所需顺序的值。 可以更改排序表达式，以使用 Lookup 函数定义排序顺序值。  
  
 例如，假定以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询定义了名为“Sizes”的数据集。 该查询使用 CASE 语句，为每个“Size”值定义排序顺序值 SizeSortOrder：  
  
```  
SELECT Size,   
  CASE Size  
        WHEN 'S' THEN 1  
        WHEN 'M' THEN 2    
        WHEN 'L' THEN 3  
        WHEN 'XL' THEN 4  
        ELSE 0  
  END as SizeSortOrder  
FROM Production.Product  
```  
  
 在表中，有一个基于 `[Size]`的行组，您可以更改组排序表达式，以使用 Lookup 函数查找与大小值对应的数字字段。 表达式应该类似于：  
  
```  
=Lookup(Fields!Size.Value, Fields!Size.Value, Fields!SizeSortOrder.Value, "Sizes")  
```  
  
 有关详细信息，请参阅[对数据区域中的数据排序（报表生成器和 SSRS）](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)和 [Lookup 函数（报表生成器和 SSRS）](../../reporting-services/report-design/report-builder-functions-lookup-function.md)。  
  
###  <a name="Interactive"></a> 为用户添加交互式排序  
 若要让用户能够更改表或矩阵中的报表数据的排序顺序，您可向列标题或组头添加交互式排序按钮。 用户可以单击该按钮以切换排序顺序。 允许用户交互的呈现格式（如 HTML）支持交互式排序。  
  
 您向 Tablix 数据区域单元中的文本框添加交互式排序按钮。 默认情况下，每个单元包含一个文本框。 在文本框属性中，可以指定要进行排序的表格或矩阵数据区域的部分（父组值、子组值或详细信息行）、排序依据以及是否对具有对等关系的其他报表项应用排序表达式。 例如，如果提供同一数据集的视图的表和图表均包含在矩形内，则它们为对等数据区域。 用户在表中切换排序顺序时，也将切换图表的排序顺序。 有关详细信息，请参阅[交互式排序（报表生成器和 SSRS）](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md)。  
  
  
##  <a name="HowTo"></a> 操作指南主题  
 [在滚动报表时保持标题可见（报表生成器和 SSRS）](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
 [与组一起显示组头和组尾（报表生成器和 SSRS）](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [将交互式排序添加到表或矩阵（报表生成器和 SSRS）](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
 [为数据区域设置“无数据”消息（报表生成器和 SSRS）](../../reporting-services/report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [创建一个递归层次结构组（报表生成器和 SSRS）](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
 [在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
 [与组一起显示组头和组尾（报表生成器和 SSRS）](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [在图表中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-chart-report-builder-and-ssrs.md)  
  
 [向组或 Tablix 数据区域添加总计（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
##  <a name="Section"></a> 本节内容  
 [组表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
 [筛选器公式示例（报表生成器和 SSRS）](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
 [添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)  
  
##  <a name="Related"></a> 相关章节  
 [了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)  
  
 [创建递归层次结构组（报表生成器和 SSRS）](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
  
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
 [报表和组变量集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)  
  
 [在图表中显示包含多个数据区域的序列（报表生成器和 SSRS）](../../reporting-services/report-design/displaying-a-series-with-multiple-data-ranges-on-a-chart.md)  
  
 [将多个数据区域链接到同一数据集（报表生成器和 SSRS）](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另请参阅  
 [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [地图（报表生成器和 SSRS）](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [迷你图和数据条（报表生成器和 SSRS）](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [仪表（报表生成器和 SSRS）](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [指示器（报表生成器和 SSRS）](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
