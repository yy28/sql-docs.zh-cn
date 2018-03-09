---
title: "利用 Tablix 数据区域的灵活性（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fef19359-a618-4d21-a7e4-e391cdefd4eb
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b795c6ab6d2106c781dbcd75cbf913dda85298d5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs"></a>利用 Tablix 数据区域的灵活性（报表生成器和 SSRS）
在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中，通过功能区上的“插入”选项卡添加表、矩阵或列表数据区域时，应从 Tablix 数据区域的初始模板开始， 但不受该模板的限制。 通过添加或删除组、行和列等任何 Tablix 数据区域功能，可以继续开发数据的显示方式。  
  
 删除行组或列组时，您可以选择删除用于显示组值的行和列。 还可以手动添加或删除行和列。 若要了解如何使用行和列显示详细信息数据和组数据，请参阅 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)。  
  
 在更改 Tablix 数据区域的结构之后，可以设置相应属性以帮助控制报表呈现数据区域的方式；例如，可以在每页顶部重复列标题，或者将组标题与组保留在一起。 有关详细信息，请参阅 [控制 Tablix 数据区域在报表页上的显示（报表生成器和 SSRS）](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="changing-a-table-to-a-matrix"></a>将表更改为矩阵  
 默认情况下，表具有用于显示报表数据集的值的详细信息行。 通常，表包括按组组织详细信息数据的行组，以及基于每个组的聚合值。 若要将表更改为矩阵，请添加列组。 通常，当数据区域包含行组和列组时，您需要删除详细信息组，以便仅显示各组的汇总值。 有关详细信息，请参阅 [在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
 根据定义，创建矩阵时，将添加一个 Tablix 角单元。 可以在该区域中合并单元并添加标签。 有关详细信息，请参阅[合并数据区域中的单元（报表生成器和 SSRS）](../../reporting-services/report-design/merge-cells-in-a-data-region-report-builder-and-ssrs.md)。  
  
## <a name="changing-a-matrix-to-a-table"></a>将矩阵更改为表  
 默认情况下，矩阵包含行组和列组，但不包含任何详细信息组。 若要将矩阵更改为表，请删除列组，并添加详细信息组以便在详细信息行上显示。 有关详细信息，请参阅[在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)和[添加详细信息组（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md)。  
  
## <a name="changing-a-default-list-to-a-grouped-list"></a>将默认列表更改为分组列表  
 默认情况下，列表包含详细信息行，但不包含任何组。 若要将列表更改为使用组行，请重命名详细信息组，并指定组表达式。 有关详细信息，请参阅[在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
## <a name="creating-stepped-displays"></a>创建递阶显示  
 默认情况下，将组添加到 Tablix 数据区域后，行组标题区域中的单元将在列中显示组值。 当具有嵌套组时，将在单独的列中显示每个组。 若要创建递阶显示，请保留一个组列并删除所有其他组列，设置保留列的格式，使其按缩进文本显示形式来显示组层次结构。 有关详细信息，请参阅[创建递阶报表（报表生成器和 SSRS）](../../reporting-services/report-design/create-a-stepped-report-report-builder-and-ssrs.md)。  
  
## <a name="adding-an-adjacent-details-group"></a>添加相邻详细信息组  
 默认情况下，详细信息组是组层次结构中最内部的子组。 不能在详细信息组下嵌套组。 例如，可以创建其他相邻详细信息组，以便显示按销售额排序位于前 5 名和最后 5 名的产品。 由于可以对每个组添加筛选器和排序表达式，因此，可以在一个 Tablix 数据区域中显示同一数据集的两个详细信息数据视图。 有关详细信息，请参阅[了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)、[在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)和[将筛选器添加到数据集（报表生成器和 SSRS）](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩阵（报表生成器和 SSRS）](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
  
  
