---
title: 插入或删除列（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: e9db79e2-7e7d-4359-a706-cb746c94182a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2796447d65a7fcabe029c67f460a76284daf242f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580207"
---
# <a name="insert-or-delete-a-column-report-builder-and-ssrs"></a>插入或删除列（报表生成器和 SSRS）
  可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中的 Tablix 数据区域中添加或删除列。 Tablix 数据区域可以是一个表、矩阵或列表。 下面的过程不适用于图表和仪表数据区域。  
  
 在 Tablix 数据区域中，您可以在组内添加与组相关联的列或在组外添加与组不相关联的列。 位于组内的列对于每个唯一组值只重复一次。 例如，如果某个组基于包含颜色名称的数据列中的值，则该组中的列对于不同的颜色名称只重复一次。 对于嵌套组，列可以位于子组的外部，但需要位于父组的内部。 在这种情况下，行针对父组中的每个唯一值只重复一次。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-that-the-row-and-column-handles-appear"></a>选择数据区域，以显示行控点和列控点  
  
-   在“设计”视图中，单击 Tablix 数据区域的左上角，以使数据区域的上方和旁边显示列控点和行控点。  
  
     有关数据区域的详细信息，请参阅 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
## <a name="to-insert-a-column-in-a-selected-data-region"></a>在所选数据区域中插入列  
  
-   右键单击要插入列的位置对应的列图柄，再单击“插入列”  ，然后单击“左侧”  或“右侧”  。  
  
     \- 或 -  
  
-   右键单击要插入行的数据区域中的单元，再单击“插入列”  ，然后单击“左侧”  或“右侧”  。  
  
## <a name="to-delete-a-column-from-a-selected-data-region"></a>删除所选数据区域中的列  
  
-   选择要删除的列，右键单击任一所选列的图柄，然后单击“删除列”  。  
  
     \- 或 -  
  
-   右键单击要删除的列所在的数据区域中的单元，然后单击“删除列”  。  
  
## <a name="to-insert-a-column-in-a-group-in-a-selected-data-region"></a>在所选数据区域的组中插入列  
  
-   在要插入列的 Tablix 数据区域的列组区域中，右键单击插入位置的列组单元，再单击“插入列”  ，然后单击“左侧 - 组外部”  、“左侧 - 组内部”  、“右侧 - 组内部”  或“右侧 - 组外部”  。  
  
     此时将在您单击过的列组单元所表示的组的内部或外部添加一列。  
  
## <a name="to-delete-a-column-from-a-group-in-a-selected-data-region"></a>删除所选数据区域的组中的列  
  
-   右键单击要删除的列所在的 Tablix 数据区域的列组区域中的列组单元，然后单击“删除列”  。  
  
## <a name="see-also"></a>另请参阅  
 [了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩阵（报表生成器和 SSRS）](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)      
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
