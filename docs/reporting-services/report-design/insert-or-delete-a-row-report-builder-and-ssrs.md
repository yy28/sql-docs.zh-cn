---
title: 插入或删除行（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b9642af3-b3ae-4f78-b0be-8f96b79fc313
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3b20b95586e387484d536ad8005c6f57c1de4698
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580162"
---
# <a name="insert-or-delete-a-row-report-builder-and-ssrs"></a>插入或删除行（报表生成器和 SSRS）
可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中的 Tablix 数据区域中添加或删除行。 Tablix 数据区域可以是一个表、矩阵或列表。 下面的过程不适用于图表和仪表数据区域。  
  
 在 Tablix 数据区域中，您可以在组内添加与组相关联的行或在组外添加与组不相关联的行。 位于组内的行对于每个唯一组值只重复一次。 例如，如果某个组基于包含颜色名称的数据列中的值，则该组中的行对于不同的颜色名称只重复一次。 对于嵌套组，行可以位于子组的外部，但需要位于父组的内部。 在这种情况下，行针对父组中的每个唯一值只重复一次。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-the-row-and-column-handles-appear"></a>选择数据区域，以显示行控点和列控点  
  
-   在“设计”视图中，单击 Tablix 数据区域的左上角，以使数据区域的上方和侧面显示列控点和行控点。  
  
     有关数据区域的详细信息，请参阅 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
## <a name="to-insert-a-row-in-a-selected-data-region"></a>在所选数据区域中插入行  
  
-   右键单击要插入行的位置对应的行控点，再单击“插入行”，然后单击“上方”或“下方”    。  
  
     \- 或 -  
  
-   右键单击要插入行的数据区域中的单元，再单击“插入行”，然后单击“上方”或“下方”    。  
  
## <a name="to-delete-a-row-from-a-selected-data-region"></a>删除所选数据区域中的行  
  
-   选择要删除的行，右键单击任一所选行的控点，然后单击“删除行”  。  
  
     \- 或 -  
  
-   右键单击要删除的行所在的数据区域中的单元，然后单击“删除行”  。  
  
## <a name="to-insert-a-row-in-a-group-in-a-selected-data-region"></a>在所选数据区域的组中插入行  
  
-   在要插入行的 Tablix 数据区域的行组区中，右键单击插入位置的行组单元，再单击“插入行”，然后单击“上方 – 组外部”、“上方 – 组内部”、“下方 – 组内部”或“下方 – 组外部”      。  
  
     此时将在您单击过的行组单元所表示的组的内部或外部添加一行。  
  
## <a name="to-delete-a-row-from-a-group-in-a-selected-data-region"></a>删除所选数据区域的组中的行  
  
-   右键单击要删除的行所在的 Tablix 数据区域的行组区中的行组单元，然后单击“删除行”  。  
  
## <a name="see-also"></a>另请参阅  
 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩阵（报表生成器和 SSRS）](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)     
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
