---
title: 添加、移动或删除表、矩阵或列表（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4b97c470-cde0-4bb1-a46e-5f5f5553feaa
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7239efa5a2d64b3751fde34d7cd1e676ea905dd4
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65581997"
---
# <a name="add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs"></a>添加、移动或删除表、矩阵或列表（报表生成器和 SSRS）
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分区报表中，数据区域可显示来自报表数据集的数据。 数据区域包括表、矩阵、列表、图表和仪表。 若要将一个数据区域嵌套到另一个数据区域中，请分别添加每个数据区域，然后将子数据区域拖到父数据区域中。  
  
 将表或矩阵数据区域添加到报表中的最简单方式是运行新建表或新建矩阵向导。 这些向导将引导您完成选择数据源的连接、安排字段以及选择布局和样式的过程。 这些向导仅在报表生成器中提供。  
  
## <a name="to-add-a-table-or-matrix-to-a-report-by-using-the-new-table-or-new-matrix-wizard"></a>通过使用新建表或新建矩阵向导，将表或矩阵添加到报表  
  
1.  在 **“插入”** 选项卡上，单击 **“表”** 或 **“矩阵”**，然后单击 **“表向导”** 或 **“矩阵向导”**。  
  
2.  执行“新建表”或“新建矩阵”向导中的步骤。  
  
3.  在 **“主文件夹”** 选项卡上，单击 **“运行”** ，以查看所呈现的报表。  
  
4.  在 **“运行”** 选项卡上，单击 **“设计”** 以继续处理报表。  
  
## <a name="to-add-a-data-region"></a>添加数据区域  
  
1.  在 **“功能区”** 上的 **“数据区域”** 组中，单击要添加的数据区域。  
  
2.  单击设计图面，然后拖动鼠标根据所需数据区域的大小创建一个框。  
  
3.  在“报表数据”窗格中，将报表数据集字段从“报表数据”窗格拖放至数据区域单元中。 该数据区域现已绑定到报表数据集的数据。  
  
## <a name="to-select-a-data-region"></a>选择数据区域  
  
-   对于 tablix 数据区域，右键单击角部控点。 对于图表或仪表数据区域，单击数据区域。  
  
     随即显示一个选择控点和八个大小调整控点。  
  
     对于嵌套数据区域，在该嵌套数据区域中右键单击，再单击“选择”，然后选择所需的报表项。 若要验证所选择的报表项，请使用“属性”窗格。 设计图面上所选项的名称显示在“属性”窗格的工具栏中。  
  
## <a name="to-move-a-data-region"></a>移动数据区域  
  
-   若要移动数据区域，请单击数据区域的选择控点，然后拖动该数据区域。 使用对齐线可以将该数据区域与现有报表项对齐。  
  
     如果标尺不可见，请单击“视图”选项卡并选择 **“标尺”** 选项。  
  
     此外，也可以使用箭头键在设计图面上移动所选数据区域。  
  
## <a name="to-delete-a-data-region"></a>删除数据区域  
  
-   选择数据区域，在该数据区域中右键单击，然后单击“删除”。  
  
## <a name="see-also"></a>另请参阅  
 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
