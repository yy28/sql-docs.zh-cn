---
title: "了解组（报表生成器和 SSRS） | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "10056"
  - "10424"
ms.assetid: c32d4d89-45e4-4f77-a3e9-0429f53f9d6f
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# 了解组（报表生成器和 SSRS）
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，组是绑定到数据区域的报表数据集中的命名数据集。 基本上，一个组可组织一个报表数据集视图。 数据区域中的所有组都指定相同报表数据集的不同视图。  
  
 为帮助直观地了解什么是组，请参考下图，该图显示了预览中的 Tablix 数据区域。 在此图中，行组按产品类型对数据集分类，列组按地理区域和年份对数据集分类。  
  
 ![Tablix 数据区域](../../reporting-services/report-design/media/rs-tablixareas.gif "Tablix 数据区域")  
  
 以下几节帮助描述组的各个方面。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## 什么构成组？  
 一个组具有指定的名称和一个组表达式集。 该组表达式集可以是单个数据集字段引用，也可以是多个表达式的组合。 在运行时，如果组包含多个表达式，则合并组表达式，并应用于组中的数据。 例如，有一个组使用日期字段来组织数据区域中的数据。 在运行时，按日期组织数据，然后与每个日期的其他数据集值总计一起显示。  
  
## 何时创建组？  
 大多数情况下，报表生成器和报表设计器会在您设计数据区域时自动为您创建组。 对于表、矩阵或列表，当您在“分组”窗格上放置字段时，将创建组。 对于图表，当您在图表放置区上放置字段时，将创建组。 对于仪表，则必须使用仪表属性对话框。 对于表、矩阵或列表，还可以手动创建组。 有关详细信息，请参阅[在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。 有关如何在创建报表时添加组的示例，请参阅[教程：创建基本表报表（报表生成器）](../../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)或[创建基本表报表（SSRS 教程）](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)。  
  
## 如何修改组？  
 在创建组之后，可以设置特定于数据区域的属性（例如筛选器和排序表达式、分页符和组变量），以存储特定于作用域的数据。 有关详细信息，请参阅[对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
 若要修改现有组，请打开相应的组属性对话框。 可以更改组的名称。 而且，可以基于单个字段或多个字段，或者基于在运行时指定值的报表参数指定组表达式。 还可以使组基于一个表达式集，例如一个用于指定人口统计学数据的年龄范围的表达式集。 有关详细信息，请参阅[组表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  如果更改组的名称，则必须手动更新引用该组的以前名称的任何组表达式。  
  
## 如何组织组？  
 了解组的组织方式，可帮助您通过指定相同的组表达式设计显示相同数据的不同视图的数据区域。  
  
 对于每个数据区域，组都在内部组织为一个或多个层次结构的成员。 组层次结构包含嵌套的且可以有相邻组的父/子组。  
  
 如果将父/子组视为树结构，则每个组层次结构都是树结构的森林。 Tablix 数据区域包括行组层次结构和列组层次结构。 与行组成员关联的数据在页上水平展开，与列组成员关联的数据则沿页垂直展开。 “分组”窗格显示在设计图面上当前所选 Tablix 数据区域的行组和列组成员。 有关详细信息，请参阅[“分组”窗格（报表生成器）](../../reporting-services/report-design/grouping-pane-report-builder.md)。  
  
 图表数据区域包括类别组层次结构和序列组层次结构。 类别组成员显示在类别轴上，序列组成员显示在序列轴上。  
  
 尽管通常仪表数据区域不需要组，但使用组可以指定如何对要在仪表上聚合的数据进行分组。  
  
## 每个数据区域有哪些可用的组类型？  
 作为网格展开的数据区域所支持的组与以可见方式显示摘要数据的数据区域支持的组不同。 因此，Tablix 数据区域以及基于 Tablix 数据区域的表、列表和矩阵支持不同于图表或仪表的组。 以下几节讨论在每种类型的数据区域中分组的类型和目的。  
  
> [!NOTE]  
>  尽管组在不同数据区域中有不同的名称，但如何创建和使用组的原则是相同的。 在为数据区域创建组时，需要指定一种方式来组织链接到数据区域的数据集中的详细信息数据。 每个数据区域都支持一个用于显示分组数据的组结构。  
  
### Tablix 数据区域中的组：详细信息组、行组和列组  
 如本主题前面所示，Tablix 数据区域使您能够按行或列将数据组织到组中。 但是，行组和列组不是 Tablix 数据区域中唯一可用的组。 此数据区域可以具有以下类型的组：  
  
-   **详细信息组** 详细信息组包含在报表生成器或报表设计器应用数据集和数据区域筛选器之后报表数据集中的所有数据。 因此，详细信息组是唯一没有组表达式的组。  
  
     基本上，详细信息组指定了在查询设计器中运行数据集查询时会看见的数据。 例如，有一个从销售订单表中检索所有列的查询。 因此，此详细信息组中的数据包括表中每一行所有列的所有值。 此详细信息组中的数据还包括已经创建的任何计算数据集字段的值。  
  
    > [!NOTE]  
    >  详细信息组中的数据还可以包括服务器聚合，它们是对数据源进行计算以及在查询中检索得到的聚合。 默认情况下，除非你的报表包括使用聚合函数的表达式，否则报表生成器和报表设计器会将服务器聚合视为详细信息数据。 有关详细信息，请参阅 [聚合](../../reporting-services/report-design/aggregate-function-report-builder-and-ssrs.md)。  
  
     默认情况下，向报表添加表或列表时，报表生成器和报表设计器会自动为您创建详细信息组，并添加行以显示详细信息数据。 默认情况下，将数据集字段添加到此行中的单元时，您将看到这些字段的简单表达式，例如 [Sales]。 查看数据区域时，将在结果集中对每个值重复一次详细信息行。  
  
-   **行组和列组** ：可以按行或列将数据组织到组中。 行组在页上垂直展开。 列组在页上水平展开。 组可以嵌套，例如，首先按 [Year] 分组，接着按 [Quarter] 分组，然后再按 [Month] 分组。 组还可以相邻，例如，在 [Territory] 上的组和单独在 [ProductCategory] 上的组。  
  
     为数据区域创建组时，报表生成器和报表设计器会向该数据区域自动添加行或列，并使用这些行或列显示组数据。  
  
-   **递归层次结构组** ：递归层次结构组将包括多个级别的单个报表数据集中的数据组织起来。 例如，递归层次结构组可以显示组织层次结构，例如，向 [Employee] 报告的 [Employee]。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供的组属性和内置函数使你能够为这种报表数据创建组。 有关详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
 下面的列表总结了对每个数据区域使用组的方式：  
  
-   **表**：定义嵌套行组、相邻行组和递归层次结构行组（例如，为组织图）。 默认情况下，表包括详细信息组。 可通过将数据集字段拖到所选表的“分组”窗格添加组。  
  
-   **矩阵** ：定义嵌套行组和列组，以及相邻行组和列组。 可通过将数据集字段拖到所选矩阵的“分组”窗格添加组。  
  
-   **列表** ：默认情况下，支持详细信息组。 典型用法是支持一个级别的分组。 可通过将数据集字段拖到所选列表的“分组”窗格添加组。  
  
 添加组之后，数据区域的行和列控点将更改，以反映组成员身份。 删除组时，可以选择仅删除组定义，也可以选择删除组及其所有关联的行和列。 有关详细信息，请参阅 [Tablix 数据区域单元、行和列（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
 若要限制要在详细信息数据或组数据的计算中显示或使用的数据，请为组设置筛选器。 有关详细信息，请参阅[添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](../../reporting-services/report-design/add dataset filters, data region filters, and group filters.md)。  
  
 默认情况下，在创建组时，组的排序表达式与组表达式相同。 若要更改排序顺序，请更改排序表达式。 有关详细信息，请参阅[对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
#### 了解 Tablix 单元的组成员身份  
 Tablix 数据区域的行或列中的单元可以属于多个行组和列组。 在使用聚合函数（例如 `=Sum(Fields!FieldName.Value`）的单元的文本框中定义表达式时，单元的默认组作用域是其所属的最内部的子组。 如果某个单元同时属于行组和列组，则作用域是两个最内部的组。 还可以编写表达式，用于相对于另一个数据集计算以某组为作用域的聚合小计。 例如，可以相对于列组或相对于数据区域的所有数据（例如 `=Sum(Fields!FieldName.Value)/Sum(Fields!FieldName.Value,"ColumnGroup")`）计算组的百分比。 有关详细信息，请参阅 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)。  
  
## 另请参阅  
 [在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [向组或 Tablix 数据区域添加总计（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)   
 [对数据区域中的数据进行排序（报表生成器和 SSRS）](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [深化操作（报表生成器和 SSRS）](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  