---
title: “分组”窗格（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10033"
helpviewer_keywords:
- Grouping Pane dialog box
ms.assetid: 983ee5a4-944c-491e-8720-7cd9f3881961
caps.latest.revision: 16
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c9fc7f5f5caab253bf0a38aa17d9d7db0d878fd1
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2018
ms.locfileid: "40409359"
---
# <a name="grouping-pane-report-builder"></a>“分组”窗格（报表生成器）
  “分组”窗格显示当前所选 Tablix 数据区域的行组和列组。 “分组”窗格对“图表”或“仪表”数据区域不可用。 “分组”窗格包含“行组”窗格和“列组”窗格。 “分组”窗格有两种模式：默认和高级。 默认模式显示行组和列组的动态成员的层次结构视图。 高级模式同时显示行组和列组的动态及静态成员。 组是来自数据区域显示的报表数据集中的一组命名的数据。 组被组织到包括静态和动态成员的层次结构中。 有关详细信息，请参阅[了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  如果看不到“分组”窗格，请在“查看”选项卡的“显示/隐藏”组中单击“分组”。  
  
 行组和列组区域中的单元可以是 Tablix 行组或列组的静态或动态成员。 静态成员每个组重复一次，并且通常包含标签或总计。 动态成员则每个组实例重复一次，并且通常包含组表达式的唯一值。 在行组区域或列组区域中选择 Tablix 单元时，将在“行组”或“列组”窗格中选择相应的组成员。 反之，如果在“分组”窗格中选择某些组，则将在设计图面上选择与相应组成员关联的相应单元。 有关 Tablix 行和列组区域的详细信息，请参阅 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md)。  
  
 “分组”窗格支持以下模式：  
  
-   **默认。** 使用默认模式可以添加、编辑或删除组。 通过从“报表数据”窗格中拖动字段并将它们插入组层次结构中，可以添加父组、子组和详细信息组。 若要添加相邻组，必须使用 **“添加组”** 快捷方式。 有关详细信息，请参阅 [在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
-   **高级**。 使用 **“高级模式”** 可以查看行组和列组的所有成员，以及为静态成员设置属性。 创建组或添加总计时，将自动设置用于控制 Tablix 数据区域如何在每个报表页上呈现行和列的属性。 若要手动调整这些属性，必须在 Tablix 成员上设置它们。 有关详细信息，请参阅 [控制 Tablix 数据区域在报表页上的显示（报表生成器和 SSRS）](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)。  
  
## <a name="default-mode"></a>默认模式  
 在默认模式中，“行组”窗格和“列组”窗格将显示所有父组、子组和相邻组的层次结构视图。 子组缩进显示在其父组下面。 相邻组以与其同级组相同的缩进程度显示。 下图显示一个 Tablix 数据区域，其中包含嵌套行组和嵌套及相邻的列组。  
  
 ![Tablix、嵌套行组和列组，以及相邻行组和列组](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpane.gif "Tablix, nested and adjacent row and column groups")  
  
 “分组”窗格显示相应的行组和列组。 在下图中，在“行组”窗格中已选择基于子类别的组，并在 Tablix 数据区域中选择了 [Subcat] 分组单元：  
  
 ![嵌套行组和列组的“分组”窗格](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpanedefaultview.gif "Grouping pane for nested row and column groups")  
  
 在“行组”窗格中，基于子类别的组是基于类别的组的子组。 在“列组”窗格中，国家/地区组是地理组的子组。 年组和国家/地区组是相邻组。  
  
 有关详细信息，请参阅 [Tablix 数据区域单元、行和列（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
## <a name="advanced-mode"></a>“高级模式”  
 在高级模式中，“行组”窗格和“列组”窗格显示包括静态成员和动态成员在内的所有组的层次结构视图。 选定成员后，“属性”窗格将显示当前所选 Tablix 成员的属性。  
  
> [!NOTE]  
>  若要切换“高级模式”，请在“列组”窗格一侧右键单击向下箭头，然后单击“高级模式”。  
  
 在大多数情况下，在创建组或添加总计时，将自动设置用于控制静态和动态组行及组列的显示的属性。 若要编辑默认值，必须在“行组”或“列组”窗格中选择组成员，然后在“属性”窗口中更改属性值。 以下属性可用：  
  
-   **FixedData**。 布尔值。 适用于外部行标题和列标题。 在诸如 HTML 这样的呈现器中，当垂直滚动时冻结行组区域，或在水平滚动时冻结列组区域。  
  
-   **HideIfNoRows**。 布尔值。 仅适用于静态成员。 如果设置，“Hidden”和“ToggleItem”将被忽略。 如果 Tablix 数据区域不包含任何数据行，则隐藏该成员。  
  
-   **KeepTogether**。 布尔值。 指示应在一个页上显示整个 Tablix 成员和任何嵌套的成员（如果可能）。  
  
-   **KeepWithGroup**。 布尔值。 仅适用于静态行成员。 如果可能，则将此行与上一个或下一个同级动态成员一起显示（如果它未隐藏）。 若要将行标题与其关联的组一起显示，请将 KeepWithGroup 设置为 **After**。  
  
-   **RepeatOnNewPage**。 布尔值。 仅适用于静态行成员，并且 KeepWithGroup 不为“无”时。 如果可能，则在至少有一个由 KeepWithGroup 指定的动态成员实例的每一页上重复该静态行。 若要将行标题与其关联的组一起显示，请将 RepeatOnNewPage 设置为 **True**。  
  
-   **Hidden**。 布尔值。 指示行或列最初是否应当隐藏。  
  
-   **ToggleItem。** 字符串。 向其添加切换图像的文本框的名称。 该文本框必须在相同的组作用域或包含作用域中。  
  
 有关详细信息，请参阅[控制 Tablix 数据区域在报表页上的显示（报表生成器和 SSRS）](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)、[与组一起显示组头和组尾（报表生成器和 SSRS）](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)和[在多个页中显示行标题和列标题（报表生成器和 SSRS）](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)。  
  
 并非每个静态成员都有对应于设计图面上的单元的标题。 在“分组”窗格中，以下约定指示静态成员是否没有标题：  
  
-   **静态** 指示有标题单元的静态成员。  
  
-   **（静态）** 指示没有标题单元的静态成员，称为隐藏静态。  
  
## <a name="see-also"></a>另请参阅  
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
