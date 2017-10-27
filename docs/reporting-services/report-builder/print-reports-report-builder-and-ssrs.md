---
title: "打印报表 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4bad1b6e-7d94-4b17-9502-ccd3dce0fdd9
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e57d90ca72920722ddcf16d5d5708a782db5a71f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="print-reports-report-builder-and-ssrs"></a>打印报表（报表生成器和 SSRS）
  在将报表保存到报表服务器之后，可以通过浏览器、报表管理器或用于查看导出报表的任意应用程序查看和打印报表。 在保存报表之前，可以在预览报表时打印它。  
  
 所有打印处理都是在客户端计算机上按需执行的。 现在还没有任何服务器端打印功能可以实现以下操作：即将打印作业从报表服务器直接传送到与 Web 服务器连接的打印机。 打印机和打印选项由每个报表用户使用标准的 **“打印”** 对话框自行选择。  
  
 对于所设计报表专用于打印输出的报表作者来说，可以使用分页符、页眉和页脚、表达式和背景图像，来创建符合打印目的的设计方案。 专用于打印输出的报表设计元素示例包括在每个报表背面打印的条款和条件，或类似信头的图形和文本元素等等。  
  
 由于不同呈现格式的分页方式不同，因此对于所有报表的每种呈现格式，您可能无法都获得最佳的打印输出效果。 下面的列表提供示例：  
  
1.  报表页设计为可以容纳可变的数据量。 例如，对于包括矩阵的报表，根据用户是否以交互方式切换行和列，报表页可能会在水平方向和垂直方向同时扩展。 不扩展矩阵的用户将获得与扩展矩阵的用户不同的打印效果。  
  
2.  您无法将横向模式页面和纵向模式页面组合在同一报表中，也无法创建能够替换报表布局或与之并存的满足打印要求的布局（如在浏览器或其他应用程序中所呈现的布局）。  
  
3.  对于大多数的导出报表，报表打印输出包括报表上的所有可见内容，与用户在计算机监视器上看到的内容没有分别。 而报表设计图面中的空白区域将会保留。 若要以水平方式添加或删除额外的空白页，请更改报表页面宽度。  
  
> [!NOTE]  
>  如果使用浏览器的“打印”命令，则 HTML 报表打印输出可能仅包含第一页中的内容。 如果使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 客户端打印功能打印 HTML 报表，效果将更加出色。 有关详细信息，请参阅 [使用打印控件从浏览器中打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>本节内容  
 [使用打印控件从浏览器中打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)  
 介绍如何使用客户端打印功能通过 Web 浏览器或报表管理器打印报表。  
  
 [从其他应用程序打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-reports-from-other-applications-report-builder-and-ssrs.md)  
 介绍如何打印已导出到其他应用程序的报表。  
  
 [打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
 提供有关如何打印报表、如何控制页边距以及如何为硬分页呈现器（PDF、图像或打印）将呈现的报表指定纸张大小的分步说明。  
  
## <a name="see-also"></a>另请参阅  
 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [页眉和页脚 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [映像 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Reporting Services &#40; 中的分页报表生成器和 SSRS &#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)  
  
  

