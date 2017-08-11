---
title: "向 Tablix 数据区域添加数据（报表生成器和 SSRS）| Microsoft Docs"
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
ms.assetid: 8f1d0a76-afed-480f-98fb-89e2d4eb09b1
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b6f41b4d1b42db5ca020841f9363df3f4cf3eb99
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="adding-data-to-a-tablix-data-region-report-builder-and-ssrs"></a>向 Tablix 数据区域添加数据（报表生成器和 SSRS）
在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中，若要在表或矩阵中显示报表数据集中的数据，请在每个数据单元格中，指定要显示的数据集字段的名称。 可以显示详细信息数据或分组数据。 如果将组添加到表或矩阵中，则会自动添加组值和组数据的行和列。 然后，可以为数据添加小计和总计。  
  
 一个数据区域中的所有数据至少属于一个组。 详细信息数据是详细信息组的成员。 有关详细信息数据和分组数据的详细信息，请参阅[了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-detail-data"></a>添加详细信息数据  
 详细信息数据是在向数据集、数据区域和详细信息组应用筛选器之后报表数据集中的所有数据。 在单个 Tablix 数据区域中显示的所有详细信息数据都必须来自于同一报表数据集。  
  
 若要将详细信息数据从报表数据集添加到 Tablix 数据区域，请将数据集字段从“报表数据”窗格拖到详细信息行中的每个单元。 对于 Tablix 数据区域中的现有单元，通过在每个单元中使用字段选择器，或通过将字段从“报表数据”窗格拖到相应单元，可以添加或编辑数据集字段表达式。 若要创建其他列，可以从“报表数据”窗格拖动字段，并将其插入到现有 Tablix 数据区域中。  
  
 默认情况下，在运行时，详细信息行中的单元显示详细信息数据，组行中的单元显示聚合值。 有关 Tablix 行和列的详细信息，请参阅 [Tablix 数据区域单元格、行和列（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
 表模板和列表模板提供详细信息行。 矩阵模板没有详细信息行。 如果 Tablix 数据区域没有详细信息行，通过定义详细信息组可以添加一个详细信息行。 有关详细信息，请参阅[添加详细信息组（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md)。  
  
## <a name="adding-grouped-data"></a>添加分组数据  
 分组数据是在向数据集、数据区域和组应用筛选器之后由组表达式指定的所有详细信息数据。 若要组织组中的详细信息数据，请将相应字段从“报表数据”窗格拖至“分组”窗格。 添加组时， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 自动将相关行或列添加到要在其中显示分组数据的 Tablix 数据区域。 这些行或列中的单元与分组数据关联。 有关详细信息，请参阅[在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
 默认情况下，将表示数字数据的数据集字段添加到组行或组列中的单元时，该单元的值是以该单元的最内部行组和列组成员身份为作用域的分组数据之和。 可以将默认聚合函数 Sum 更改为任何其他聚合函数，例如 Avg 或 Count。 您还可以更改聚合计算的默认作用域，以便用于计算某个值在行组中所占的百分比等目的。 有关详细信息，请参阅[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 默认情况下，所有分组数据都来自同一报表数据集。 在 Tablix 数据区域中，通过将另一数据集名称指定为作用域，可以将该数据集的聚合值包括进来。 可以在单个 Tablix 数据区域中指定来自多个数据集的多个聚合值。 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)。  
  
## <a name="adding-subtotals-and-totals"></a>添加小计和总计  
 若要为组添加小计和为数据区域添加总计，请在单元或“分组”窗格中使用快捷菜单上的“添加总计”功能。 显示总计的行和列是自动添加的。 小计和总计表达式默认使用 [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md) 聚合函数。 在添加表达式之后，可以更改默认函数。 有关详细信息，请参阅[向组或 Tablix 数据区域添加总计（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="adding-labels"></a>添加标签  
 若要为组或数据区域添加标签，请在要标记的组之外添加一行或一列。 标签行和列类似于为显示总计而添加的行和列。 有关详细信息，请参阅[插入或删除行（报表生成器和 SSRS）](../../reporting-services/report-design/insert-or-delete-a-row-report-builder-and-ssrs.md)或[插入或删除列（报表生成器和 SSRS）](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
## <a name="adding-an-existing-tablix-data-region-from-another-report"></a>添加其他报表的现有 Tablix 数据区域  
 可以复制其他报表中的数据区域，并将其粘贴到新报表或现有报表中。 粘贴相应数据区域之后，必须确保定义该数据区域使用的数据集，并确保相应数据集字段的名称和数据类型与其在原始报表中时相同。 您无法将数据集从一个报表复制到另一个报表，但是，如果您的报表使用共享数据源，则可以快速复制另一个报表中的数据集。 此外，您还可以导入用于检索数据集中数据的查询的查询文本，这样可以很容易地复制报表中的查询。 有关详细信息，请参阅[报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [表达式 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [报表参数 &#40;报表生成器和报表设计器 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [交互式排序、 文档结构图和链接 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [添加数据集筛选器、 数据区域筛选器和组筛选器 （&） #40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [添加、 编辑和刷新报表数据窗格 &#40; 中的字段报表生成器和 SSRS &#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)   
 [添加表达式 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)  
  
  
