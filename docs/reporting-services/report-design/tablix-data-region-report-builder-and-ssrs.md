---
title: "Tablix 数据区域（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99f83b32-4b86-4d40-973c-9a328d23ac8b
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 90f52e1c600c0f866eb6a2754c486d0c4e5af08a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="tablix-data-region-report-builder-and-ssrs"></a>Tablix 数据区域（报表生成器和 SSRS）
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]中，Tablix 数据区域是按单元显示分页报表数据并将这些单元组织为行和列的通用布局报表项。 报表数据可以是从数据源中检索的详细信息数据，也可以是按照指定的组进行分组的聚合详细信息数据。 每个 Tablix 单元可以包含任何报表项（例如文本框或图像），也可以包含其他数据区域（例如 Tablix 区域、图表或仪表）。 若要向某一单元添加多个报表项，请首先添加一个充当容器的矩形， 然后将报表项添加到该矩形中。  
  
 在功能区上，表、矩阵和列表数据区域是用基础 Tablix 数据区域的模板表示的。 向报表添加其中一个模板时，您实际上添加的是针对特定数据布局优化的 Tablix 数据区域。 默认情况下，表模板以网格布局显示详细信息数据，矩阵以网格布局显示分组数据，而列表则以自由格式布局显示详细信息数据。  
  
 在默认情况下，表或矩阵中的每个 Tablix 单元都包含一个文本框。 列表中的单元包含一个矩形。 可以将默认报表项替换为其他报表项，如图像。  
  
 为表、矩阵或列表定义组时，报表生成器和报表设计器会向 Tablix 数据区域添加行或列，并在这些行或列中显示分组数据。  
  
 了解以下几点将有助于了解 Tablix 数据区域：  
  
*   详细信息数据和分组数据之间的区别。  
  
*   组作为组层次结构的成员进行组织，它在水平轴上组织为行组，在垂直轴上组织为列组。  
  
*  Tablix 数据区域的以下四个区域中的 Tablix 单元的用途：正文区、行组标题、列组标题和角部区。  
  
*  静态/动态行和列以及它们与组之间的关系。  
  
 本文阐述了这些概念来解释在添加模板并创建组时“报表生成器”和“报表设计器”所添加的结构，因而你可以修改该结构以满足你的需求。 报表生成器和报表设计器提供了多个有助于您识别 Tablix 数据区域结构的可视指示器。 有关详细信息，请参阅 [Tablix 数据区域单元、行和列（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-detail-and-grouped-data"></a>了解详细信息数据和分组数据  
 详细信息数据是从数据源返回的报表数据集中的所有数据。 详细信息数据实质上是运行数据集查询时查询设计器结果窗格中的显示内容。 实际详细信息数据包括创建的计算字段，并受对数据集、数据区域和详细信息组设置的筛选器的限制。 使用诸如 [Quantity] 的简单表达式可以在详细信息行上显示详细信息数据。 运行报表时，将在运行时对查询结果中的每个行重复一次详细信息行。  
  
 分组数据是根据在组定义中指定的值组织的详细信息数据，如 [SalesOrder]。 使用聚合分组数据的简单表达式（如 [Sum(Quantity)]）可以在组行和组列中显示分组数据。 有关详细信息，请参阅[了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)。  
  
## <a name="understanding-group-hierarchies"></a>了解组层次结构  
 组都组织为组层次结构的成员。 行组和列组层次结构是不同轴上的相同结构。 请将行组视为在页面内向下扩展，而将列组视为在页面内横向扩展。  
  
 树结构表示具有父/子关系的嵌套行组和列组，例如具有子类别的类别。 父组是树的根，而子组则是其分支。 多个组之间还可以具有独立的相邻关系，例如，基于地区的销售额和基于年份的销售额。 多个不相关的树层次结构称为林。 在 Tablix 数据区域中，行组和列组分别表示为独立的林。 有关详细信息，请参阅[了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)。  
  
## <a name="understanding-tablix-data-region-areas"></a>了解 Tablix 数据区域  
 Tablix 数据区域具有四个可能的单元区域：Tablix 角部区、Tablix 行组层次结构、Tablix 列组层次结构或 Tablix 正文区。 Tablix 正文区始终存在。 其他区域可选。  
  
 Tablix 正文区中的单元显示详细信息数据和组数据。  
  
 当创建行组时，会自动创建“行组”区中的单元。 在默认情况下，这些单元作为行组标题单元，并显示行组实例值。 例如，当根据 [SalesOrder] 分组时，组实例值是作为分组依据的单个销售订单。  
  
 当创建列组时，会自动创建“列组”区中的单元。 在默认情况下，这些单元作为列组标题单元，并显示列组实例值。 例如，当根据 [Year] 分组时，组实例值是作为分组依据的单个年份。  
  
 定义了行组和列组后，将自动在 Tablix 角部区中创建单元。 该区域中的单元可以显示标签，或者您也可以合并这些单元并创建标题。  
  
 有关详细信息，请参阅 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md)。  
  
## <a name="understanding-static-and-dynamic-rows-and-columns"></a>了解静态/动态行和列  
 Tablix 数据区域按与组关联的行和列的形式组织单元。 行组和列组的组结构是相同的。 该示例使用的是行组，但您可以将相同的概念应用于列组。  
  
 行是静态或动态行。 静态行不与组关联。 运行报表时，静态行仅呈现一次。 表头和表尾是静态行。 静态行显示标签和总计。 静态行中的单元以数据区域作为作用域。  
  
 动态行与一个或多个组相关联。 动态行针对最内部组的每个唯一组值呈现一次。 动态行中的单元的作用域是该单元所属的最内部行组和列组。  
  
 动态详细信息行与向设计图面添加表或列表时自动创建的详细信息组关联。 按照定义，详细信息组是 Tablix 数据区域的最内部组。 详细信息行中的单元显示详细信息数据。  
  
 动态组行是在向现有 Tablix 数据区域添加行组或列组时创建的。 动态组行中的单元显示默认作用域的聚合值。  
  
 添加总计功能在当前组以外自动创建一个行，用于显示以该组为作用域的值。 还可以手动添加静态和动态行。 可视指示符可帮助您了解哪些行是静态行以及哪些行是动态行。 有关详细信息，请参阅 [Tablix 数据区域单元、行和列（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [将多个数据区域链接到同一数据集（报表生成器和 SSRS）](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [控制 Tablix 数据区域在报表页上的显示（报表生成器和 SSRS）](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)   
 [利用 Tablix 数据区域的灵活性（报表生成器和 SSRS）](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
