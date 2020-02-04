---
title: 添加矩形或容器（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10061"
- sql13.rtp.rptdesigner.rectangleproperties.general.f1
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2079eeb5cb871b5006ac4b2c45b60e9c8a3a3c97
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65574772"
---
# <a name="add-a-rectangle-or-container-report-builder-and-ssrs"></a>添加矩形或容器（报表生成器和 SSRS）
  如果希望使用图形元素分隔报表的各部分、强调某些报表区或为一个或多个报表项提供背景，则可向 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中添加矩形。 矩形还可以用作容器，以控制数据区域在报表中的呈现方式。 可以通过编辑矩形属性（如背景和边框颜色）自定义矩形的外观。 有关使用矩形作为容器的详细信息，请参阅[矩形和线条（报表生成器和 SSRS）](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)和[在矩阵和图表中显示相同数据（报表生成器）](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)。    
   
## <a name="to-add-a-rectangle"></a>添加矩形    
    
1.  在 **“插入”** 选项卡的 **“报表项”** 组中，单击 **“矩形”** 。    
    
2.  在设计图面上，单击希望矩形左上角所处的位置，并拖动至希望矩形右下角所处的位置。    
    
     请注意，当移动游标时，“对齐线”将以游标行的形式与其他对象一起显示在设计图面上。 如果您要使对象对齐，这些对齐线将对您很有帮助。    
    
## <a name="to-create-a-container"></a>创建容器    
    
1.  向报表中添加矩形报表项。    
    
2.  将其他报表项拖到矩形中。    
    
    > [!NOTE]    
    >  矩形是可在其中创建项或将项拖到其中的唯一容器。 如果您在设计图面上现有项的周围绘制一个矩形，则此矩形不会充当该项的容器。    
    
## <a name="to-change-rectangle-properties-such-as-color-style-or-weight"></a>更改矩形的属性（如颜色、样式或粗细）    
    
1.  选择矩形，然后在“主页”选项卡的 **“边框”** 部分单击线条的颜色、样式或粗细选项。    
    
2.  单击 **“边框”** 按钮旁的箭头以确定要更改矩形的哪些边。    
    
    > [!NOTE]    
    >  如果将线条样式设置为“双线”并且线条宽度为 1 1/2 pt 或更窄，则在报表生成器、报表设计器或  **Web 门户中运行报表时，线条可能不会显示为双线**[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]。 将报表导出为其他格式（例如 Microsoft Word 和 Acrobat PDF）后，线条会显示为双线。    
    
## <a name="see-also"></a>另请参阅    
 [矩形和线条（报表生成器和 SSRS）](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)     
 [呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)    
    
  
