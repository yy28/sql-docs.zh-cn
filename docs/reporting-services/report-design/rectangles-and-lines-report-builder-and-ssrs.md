---
title: 矩形和线条（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: d6226b0c-0398-4185-8565-96099876fc21
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 755c2269d31a6dd8eab56c9df83e5a326856cb68
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43266916"
---
# <a name="rectangles-and-lines-report-builder-and-ssrs"></a>矩形和线条（报表生成器和 SSRS）
  使用矩形和线条可在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中创建各种视觉效果。 可在“开始”选项卡的“边框”部分设置这些报表项的显示属性，还可使用“属性”窗格设置其他属性。 可以为矩形添加类似背景色或图像、工具提示或书签这样的功能。  
  
##  <a name="RectanglesLinesReportParts"></a> 将矩形和线条作为报表部件  
 您可以将矩形与它们所包含的项作为报表部件与报表分开发布。 报表部件是自包含的报表项，存储在报表服务器上并可以包含在其他报表中。  
  
 不能将矩形中的报表项作为报表部件发布。 当用户向报表添加该矩形时，他们将获取该矩形及其包含的项。  阅读有关 [报表部件](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)的详细信息。  
  
##  <a name="RectangleAsContainer"></a> 将矩形用作容器  
 可以将矩形用作其他项的容器。 移动矩形时，其中包含的项也将随之一起移动。 矩形中的项在其 **Parent** 属性中显示该矩形的名称。 有关使用矩形作为容器的详细信息，请参阅[添加矩形或容器（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)和[在矩阵和图表中显示相同数据（报表生成器）](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)。  
  
> [!NOTE]  
>  矩形是可在其中创建项或将项拖到其中的唯一容器。 如果您在设计图面上现有项的周围绘制一个矩形，则此矩形不会充当该项的容器。 矩形不会在项的 Parent 属性中列出。  
  
 使用矩形来包含报表项时，请考虑在报表呈现期间这些项作为整体将受到怎样的影响。 包含重复数据行（例如，表）的报表项将展开，以容纳查询所返回的数据，这将影响矩形中其他项的定位。 如果将项定位于数据区域的下面，表将使这些项下移。 若要将项定位到合适的位置，您可以将报表项放在矩形内，该矩形的上边缘要在表的下边缘之上。 有关详细信息，请参阅[呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
##  <a name="ReportBorder"></a> 添加报表边框  
 通过向表头、表尾和表体本身添加边框（而不是添加线条或矩形），可以为报表添加边框。 有关详细信息，请参阅 [向报表添加边框（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md)的详细信息。  
  
##  <a name="HowTo"></a> 操作指南主题  
 [向报表添加边框（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md)  
  
 [添加矩形或容器（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
 [添加和修改线条（报表生成器和 SSRS）](../../reporting-services/report-design/add-and-modify-a-line-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另请参阅  
 [添加矩形或容器（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
  
