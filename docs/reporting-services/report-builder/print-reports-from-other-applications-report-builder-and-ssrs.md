---
title: "打印报表 （报表生成器和 SSRS） 的其他应用程序从 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a5560581-fd57-4a45-b7ea-43b21a8a7419
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a77635508b96b02254e90b77e4f67800a6afc49f
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="print-reports-from-other-applications-report-builder-and-ssrs"></a>从其他应用程序打印报表（报表生成器和 SSRS）
  通过报表生成器提供的导出选项，可以在其他应用程序中轻松查看报表。 **Export** 命令可以在报表工具栏上找到，当你在浏览器或基于 Web 的应用程序中打开报表时，该工具栏将显示在报表的顶部。 导出报表将会在其他应用程序中显示该报表（例如，将报表导出到 Excel 将会在 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)]中打开该报表）。 出于打印目的，建议仅当相关应用程序具有您需要使用的特定打印功能时才导出报表。  
  
 若要将报表导出到其他应用程序，您必须已安装该应用程序。 例如，在可以导出到 Acrobat (PDF) 格式之前，必须先在计算机上安装 Adobe Acrobat Reader。 如果选择将报表导出为 TIFF 格式，报表服务器将把报表置于与 TIFF 文件类型关联的查看应用程序中。 尽管所用的应用程序取决于您使用哪个 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 版本，但通常该工具是 Windows 图片和传真查看器。 默认分辨率对应于屏幕分辨率每英寸 96 点 (DPI)。 可以在 Windows 图片和传真查看器中将分辨率增加到 300 DPI 或 600 DPI，以匹配打印机的能力。 有关调整分辨率的详细信息，请参阅 Windows 产品文档。  
  
 如果选择导出为 Web 存档（也称为 MHTML）格式，则会将报表导出到您的默认浏览器。 通过浏览器进行打印可能会导致在每页的底部添加报表路径信息。 在大多数情况下，您可以通过设置浏览器选项，以避免在打印的页面上添加路径信息。 有关详细信息，请参阅所用浏览器的产品文档。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)   
 [使用打印控件从浏览器中打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [将报表导出为其他文件类型（报表生成器和 SSRS）](http://msdn.microsoft.com/library/b577568b-ecbd-44c3-be88-31dab6fc38a2)   
 [查找、查看和管理报表（报表生成器和 SSRS）](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
