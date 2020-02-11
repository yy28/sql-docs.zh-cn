---
title: 控制 Tablix 数据区域在报表页上的显示（报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f81c48cc-f038-4f57-988d-e9a3cbb46424
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c6fd4b09947bc10a9e4e960ca1097f807a47c14f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106212"
---
# <a name="controlling-the-tablix-data-region-display-on-a-report-page-report-builder-and-ssrs"></a>控制 Tablix 数据区域在报表页上的显示（报表生成器和 SSRS）
  本主题介绍 Tablix 数据区域的属性，您可以修改这些属性以便更改在报表中查看 Tablix 数据区域时该数据区域的显示方式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="controlling-the-appearance-of-data"></a>控制数据的外观  
 下列功能有助于控制 Tablix 数据区域的外观：  
  
-   **设置数据格式。** 若要在表、矩阵或列表中设置数据格式，请在单元格中设置文本框的属性。 可以同时设置多个单元的属性。 若要设置图表中的数据的格式，请在序列上设置格式设置属性。 有关详细信息，请参阅[设置报表项的格式（报表生成器和 SSRS）](formatting-report-items-report-builder-and-ssrs.md)和[设置图表格式（报表生成器和 SSRS）](formatting-a-chart-report-builder-and-ssrs.md)。  
  
-   **编写表达式**。 有关详细信息，请参阅[报表中的表达式用法（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)和[表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)。  
  
-   **控制排序顺序**。 若要控制排序顺序，必须在数据区域中定义排序表达式。 若要控制与组关联的行和列的排序顺序，必须在组中定义排序表达式，包括详细信息组。 您也可以添加交互式排序按钮，以使用户能够对 Tablix 数据区域及其包含的组进行排序。 有关详细信息，请参阅[对数据区域中的数据进行排序（报表生成器和 SSRS）](sort-data-in-a-data-region-report-builder-and-ssrs.md)。  
  
-   **当没有数据时显示一条消息**。 如果在运行时报表数据集中没有任何数据，则可以编写并显示您自己的消息来取代数据区域。 有关详细信息，请参阅[为数据区域设置“无数据”消息（报表生成器和 SSRS）](../report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)。  
  
-   有**条件地隐藏数据**。 若要有条件地控制是显示还是隐藏数据区域或数据区域的各个部分，可以将 Hidden 属性设置为`True`或将其设置为表达式。 表达式可以包括对报表参数的引用。 还可以指定切换项，以使用户可以决定是否显示详细信息数据。 有关详细信息，请参阅[深化操作（报表生成器和 SSRS）](drilldown-action-report-builder-and-ssrs.md)。  
  
-   **合并单元。** 您可以将表内多个连续单元合并为一个单元。 这称作列跨越（即单元合并）。 单元只能以水平方式或垂直方式合并。 当您合并单元后，只保留第一个单元中的数据， 而删除其他单元中的数据。 合并后的单元可以拆分为原来的列。 有关详细信息，请参阅[合并数据区域中的单元（报表生成器和 SSRS）](merge-cells-in-a-data-region-report-builder-and-ssrs.md)。  
  
## <a name="controlling-tablix-data-region-position-and-expansion-on-a-page"></a>控制 Tablix 数据区域在报表页中的位置和扩展  
 下列功能有助于控制 Tablix 数据区域在所呈现的报表中的显示方式：  
  
-   **控制 tablix 数据区域相对于其他报表项的位置**。 可以在报表设计图面上其他报表项的上方、旁边或下方放置 Tablix 数据区域。 在运行时， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 根据需要为在链接数据集中检索到的数据扩展 Tablix 数据区域，并根据需要将对等报表项移到旁边。 若要将 Tablix 定位到其他报表项旁，必须使这两个报表项对等并调整它们的相对位置。 有关详细信息，请参阅[呈现行为（报表生成器和 SSRS）](rendering-behaviors-report-builder-and-ssrs.md)。  
  
-   **更改扩展方向**。 若要控制 Tablix 数据区域是按从左到右 (LTR) 还是从右到左 (RTL) 的方向横向扩展，请使用 Direction 属性，该属性可以通过“属性”窗口访问。 有关详细信息，请参阅[呈现数据区域（报表生成器和 SSRS）](rendering-data-regions-report-builder-and-ssrs.md)。  
  
## <a name="controlling-how-a-tablix-data-region-renders-on-a-page"></a>控制 Tablix 数据区域在页面上的呈现方式  
 下面的列表介绍了可有助于控制 Tablix 数据区域在报表中的显示方式的方法：  
  
-   **控制分页**。 若要控制每个报表页中显示的数据量，可以对数据区域设置分页符。 还可以对组设置分页符。 分页符可以减少每页上需要处理的数据量，因而可影响按需呈现性能。 有关详细信息，请参阅 [Reporting Services 中的分页（报表生成器和 SSRS）](pagination-in-reporting-services-report-builder-and-ssrs.md)和[添加分页符（报表生成器和 SSRS）](add-a-page-break-report-builder-and-ssrs.md)。  
  
-   **在行标题的任意一侧显示数据**。 您并非只能在 Tablix 数据区域的一侧显示行标题。 可以在各个列之间移动行标题，使数据列显示在行标题的前面。 若要执行此操作，请修改矩阵的 GroupsBeforeRowHeaders 属性。 可以通过“属性”窗口访问此属性。 该属性的值为一个整数；例如，值为 2 将在显示包含行标题的列之前显示数据区域列数据的两个组实例。  
  
## <a name="controlling-how-tablix-row-and-column-groups-render"></a>控制 Tablix 行和列组的呈现方式  
 控制 Tablix 数据区域组的呈现方式取决于组结构。 Tablix 数据区域可包含四个区域，如下图所示：  
  
 ![Tablix 数据区域](../media/rs-tablixareas.gif "Tablix 数据区域")  
  
 行组区和列组区包含组标题。 当某一 tablix 数据区域具有组标题时，您可以通过在 **“Tablix 属性”** 对话框的 **“常规”** 页上设置属性，控制行和列的重复方式。  
  
 如果 Tablix 数据区域仅包含 Tablix 正文区，则没有组标题。 只有静态或动态 Tablix 成员。 静态成员相对于 Tablix 行组或列组显示一次。 一个动态成员针对每个唯一组值重复一次。 例如，在显示销售订单的 Tablix 数据区域中，销售订单中的列名可以显示在静态行成员上。 销售订单的每行都显示在动态行成员上。  
  
 通过在“属性”窗格中设置属性，可以帮助控制 Tablix 成员呈现的方式。 有关详细信息，请参阅[“分组”窗格（报表生成器）](grouping-pane-report-builder.md)中的“高级模式”。  
  
 下面的列表介绍了可有助于控制 Tablix 数据区域在报表中的显示方式的方法：  
  
-   **在多个页上重复行标题和列标题**。可以在 tablix 数据区域跨越的每个页上显示行标题和列标题。 有关详细信息，请参阅[在多个页中显示行标题和列标题（报表生成器和 SSRS）](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)。  
  
-   **滚动时在视图中保留行和列标题**。 您可以控制在使用浏览器滚动报表时是否显示行标题和列标题。 有关详细信息，请参阅[在滚动报表时保持标题可见（报表生成器和 SSRS）](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)。  
  
 如需深入了解将报表导出为其他格式对 Tablix 数据区域在报表页中的呈现方式产生的影响，请参阅[呈现行为（报表生成器和 SSRS）](rendering-behaviors-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [将多个数据区域链接到同一数据集（报表生成器和 SSRS）](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [嵌套数据区域（报表生成器和 SSRS）](nested-data-regions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域 &#40;报表生成器和 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)   
 [控制分页符、标题、列和行 &#40;报表生成器和 SSRS&#41;](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Tablix 数据区域（报表生成器和 SSRS）](../tablix-data-region-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](tables-report-builder-and-ssrs.md)   
 [矩阵（报表生成器和 SSRS）](create-a-matrix-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
