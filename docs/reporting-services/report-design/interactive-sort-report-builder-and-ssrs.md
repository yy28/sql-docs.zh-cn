---
title: 交互式排序（报表生成器）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 00cafed5-1a3c-4ce0-a1fb-ff1e2613f495
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5d87ccdb5cc240f73dc22c132bf4d3f88685919c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081976"
---
# <a name="interactive-sort-report-builder-and-ssrs"></a>交互式排序（报表生成器和 SSRS）
  对于表中的行或矩阵中的行和列，可以添加交互式排序按钮，以便用户能够在升序和降序顺序之间切换。 交互式排序最常见的用途是向每一个列标题添加一个排序按钮。 这样，用户就可以选择要按哪个列排序。  
  
 但是，您不仅可以向列标题添加交互式排序按钮，还可以向任何文本框添加这种按钮。 例如，对于行组外部的行中的文本框，可以为父组行或列、为子组行或列或者为详细信息行或列指定排序。 还可以将多个字段组合成单个组表达式，然后按多个字段排序。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 添加交互式排序时，必须指定以下项：  
  
-   **排序对象：** 行或列？  
  
-   **排序依据：** 依据表列中显示的某一字段？ 还是依据未显示的某一字段？  
  
-   **排序上下文：** 例如，可以在下列上下文中进行排序：与行组关联的行、与列组关联的列、详细信息行、父组内的子组，或同时在父组和子组中。  
  
-   **将排序按钮添加到哪个文本框：** 在列标题中，还是在组行标题中？  
  
-   **是否同步多个数据区域的排序：** 可以设计下面这样的报表：如果用户切换排序顺序，上级相同的其他数据区域也进行排序。  
  
 有关分步说明，请参阅 [将交互式排序添加到表或矩阵（报表生成器和 SSRS）](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)。  
  
 下表总结了通过使用交互式排序按钮可以取得的效果。  
  
|操作|排序对象|要将排序按钮添加到的位置|排序依据|排序范围|  
|------------|------------------|----------------------------------|---------------------|----------------|  
|对没有组的表的详细信息行进行排序|详细信息|列标题|绑定到此列的数据集字段|数据区域|  
|对矩阵的顶级组实例进行排序|组|列标题|父组的组表达式|数据区域|  
|对表中子组的详细信息行进行排序|详细信息|子组的标题行|要作为排序依据的数据集字段|子组|  
|对表中的多个行组的行以及详细信息行进行排序|组，但您必须重新定义组表达式|列标题|要作为排序依据的数据集字段的聚合|数据区域|  
|对多个数据区域同步排序顺序|组|通常是列标题|组表达式|数据集|  
  
 在应用所有数据区域和组排序表达式后，报表处理器会应用交互式排序。 有关详细信息，请参阅 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
## <a name="adding-interactive-sort-for-multiple-groups"></a>为多个组添加交互式排序  
 如果一个表具有嵌套的行组，且每个行组都基于单个数据集字段，则可以在该表中添加对父组值、子组值或详细信息行进行排序的交互式排序按钮。 但是，您可能需要向用户提供这样的功能：无需多次单击，即可同时按父组值和子组值对表进行排序。  
  
 为此，您必须重新设计该表，以按组合了多个字段的表达式进行分组。 例如，对于包含库存计数的数据集，如果原始表先按大小、再按颜色进行分组，则您可以使用由大小和颜色组合而成的组表达式指定单个组。 有关详细信息，请参阅 [将交互式排序添加到表或矩阵（报表生成器和 SSRS）](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对数据区域中的数据进行排序（报表生成器和 SSRS）](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [将交互式排序添加到表或矩阵（报表生成器和 SSRS）](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  
