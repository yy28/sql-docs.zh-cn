---
title: 在数据区域中添加或删除组（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4de53c3c-c6fc-49ce-b692-3609fc0b3ec5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 66883f42947ba54205a5f272bb6bbfd5a90376f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106583"
---
# <a name="add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs"></a>在数据区域中添加或删除组（报表生成器和 SSRS）
  如果您希望在显示或计算时根据特定值或表达式集来组织数据，可向数据区域添加组。 组具有标识该组所包含的数据集数据的名称和表达式。 有关组的详细信息，请参阅 [了解组（报表生成器和 SSRS）](understanding-groups-report-builder-and-ssrs.md)。  
  
 在 Tablix 数据区域中，单击表、矩阵或列表可以显示“分组”窗格。 将数据集字段拖到“行组”和“列组”窗格可以创建父组或子组。 右键单击现有组可以添加相邻组。 根据定义，详细信息组是最内部的组，并且只能作为子组添加。 右键单击现有组可以删除它。 显示组值的行和列是自动添加的。 有关详细信息，请参阅 [表、矩阵和列表（报表生成器和 SSRS）](tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
 在图表数据区域中，单击图表以显示放置区。 通过将数据集字段拖到类别和序列放置区来创建组。 若要添加嵌套组，请向放置区添加多个字段。  
  
 默认情况下，组不在仪表中定义。 仪表的默认行为是将指定字段中的所有值聚合为在仪表中显示的一个值。 有关详细信息，请参阅 [仪表（报表生成器和 SSRS）](gauges-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-parent-or-child-row-or-column-group-to-a-tablix-data-region"></a>向 Tablix 数据区域添加父/子行组或父/子列组  
  
1.  将字段从 **“报表数据”** 窗格拖到 **“行组”** 窗格或 **“列组”** 窗格。  
  
    > [!NOTE]  
    >  如果未显示“分组”窗格，请在“视图”选项卡上，单击“分组”  。  
  
2.  使用向导栏将该字段拖到组层次结构之上或之下，将其放置到相应位置作为现有组的父组或子组。  
  
     添加的组具有默认名称、组表达式和基于字段名称的排序表达式。  
  
### <a name="to-add-an-adjacent-row-or-column-group-to-a-tablix-data-region"></a>向 Tablix 数据区域添加相邻的行组或列组  
  
1.  在“分组”窗格中，右键单击要添加的组的对等组。 单击 **“添加组”** ，然后单击 **“前面相邻”** 或 **“后面相邻”** 以指定组的添加位置。 此时将打开 **“Tablix 组”** 对话框。  
  
2.  在 **“名称”** 中，键入组的名称。  
  
3.  在“组表达式”中，键入表达式，或者单击表达式按钮 (fx)，创建表达式   。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     新组即被添加到“分组”窗格，显示组值的行或列则被添加到设计图面上的 Tablix 数据区域中。  
  
### <a name="to-add-a-details-group-to-a-tablix-data-region"></a>向 tablix 数据区域添加详细信息组  
  
1.  在“分组”窗格中，右键单击作为最内部的子组的组，而非“详细信息”组  。 单击 **“添加组”** ，然后单击 **“子组”** 。 此时将打开 **“Tablix 组”** 对话框。  
  
2.  在 **“组表达式”** 中，使表达式保留为空白。 详细信息组没有任何表达式。  
  
3.  选择 **“显示详细信息数据”** 。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     新的详细信息组作为子组添加到“分组”窗格，在步骤 1 中选择的组的行控点显示详细信息组图标。 有关控点的详细信息，请参阅 [Tablix 数据区域单元、行和列（报表生成器和 SSRS）](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
### <a name="to-edit-a-row-or-column-group-in-a-tablix-data-region"></a>在 Tablix 数据区域中编辑行组或列组  
  
1.  在报表设计图面上，单击 Tablix 数据区域中的任意位置以将其选中。 “分组”窗格随即显示行组和列组。  
  
2.  右键单击该组，然后单击“组属性”  。  
  
3.  在 **“名称”** 中，键入组的名称。  
  
4.  在“组表达式”中，键入或选择简单表达式，或者单击表达式 (fx) 按钮，创建组表达式   。  
  
5.  单击 **“添加”** 以创建其他表达式。 使用逻辑与组合指定的所有表达式，以便指定该组的数据。  
  
6.  （可选）单击“分页符”设置分页符选项  。  
  
7.  （可选）单击“排序”，选择或键入指定组中的值的排序顺序的表达式  。  
  
8.  （可选）单击“可见性”，选择该项的可见性选项  。  
  
9. （可选）单击“筛选器”，设置该组的筛选器  。  
  
10. （可选）单击“变量”，定义以该组作为作用域、并且可以从任何子组访问的变量  。  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-group-from-a-tablix-data-region"></a>删除 Tablix 数据区域中的组  
  
1.  在“分组”窗格中，右键单击组，然后单击“删除组”  。  
  
2.  在 **“删除组”** 对话框中，请选择下列选项之一：  
  
    -   **删除组以及相关行和列** ：选择该选项可以删除组定义和显示组数据的所有相关行。 对于详细信息组，如果同一行同时作为详细信息和组数据，则仅删除详细信息数据行。  
  
    -   **仅删除组** 选择该选项可以使 Tablix 数据区域的结构保持不变，并且仅删除组定义。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-details-group-from-a-tablix-data-region"></a>删除 Tablix 数据区域中的详细信息组  
  
1.  在“分组”窗格中，右键单击详细信息组，然后单击“删除组”  。  
  
2.  在 **“删除组”** 对话框中，请选择下列选项之一：  
  
    -   **删除组以及相关行和列** ：选择该选项可以删除组定义和显示组数据的所有相关行。 对于详细信息组，如果同一行同时作为详细信息和组数据，则仅删除详细信息数据行。  
  
    -   **仅删除组** 选择该选项可以使 Tablix 数据区域的结构保持不变，并且仅删除组定义。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     详细信息组即被删除。  
  
    > [!NOTE]  
    >  验证在删除详细信息行之后，每个单元中的表达式视具体情况指定聚合表达式。 如有必要，请编辑表达式以便根据需要指定聚合函数。  
  
## <a name="see-also"></a>请参阅  
 [报表和组变量集合引用（报表生成器和 SSRS）](built-in-collections-report-and-group-variables-references-report-builder.md)   
 [组表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Tablix 数据区域（报表生成器和 SSRS）](../tablix-data-region-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](tables-report-builder-and-ssrs.md)   
 [矩阵（报表生成器和 SSRS）](create-a-matrix-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
