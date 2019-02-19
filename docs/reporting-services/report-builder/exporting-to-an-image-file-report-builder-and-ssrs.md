---
title: 导出到图像文件（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2520444f633505bfaa74334fe977cbdccdd9e603
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294135"
---
# <a name="exporting-to-an-image-file-report-builder-and-ssrs"></a>导出到图像文件（报表生成器和 SSRS）
  图像呈现扩展插件可以将分页报表呈现为位图或图元文件。 默认情况下，图像呈现扩展插件将生成报表的 TIFF 文件，您可以按多页形式查看此类文件。 客户端收到图像时，可以在图像查看器中显示图像，并可以打印图像。 本主题提供了特定于图像呈现器的信息并说明了呈现规则的例外情况。  
  
 图像呈现扩展插件可以采用 [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)] 支持的任何格式生成文件：BMP、EMF、EMFPlus、GIF、JPEG、PNG 和 TIFF。 对于 TIFF 格式，主输出流的文件名为 *ReportName*.tif。 对于其他按照每个文件一页的方式进行呈现的所有格式，文件名为 *ReportName_Page.ext* ，其中， *ext* 是所选格式的文件扩展名。 若要以另一种受图像支持的格式生成文件，请在 **OutputFormatDeviceInfo** 设置中指定上面列出的任意字符串。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="SupportedImageFormats"></a> 支持的图像格式  
 下表显示了每种图像呈现器格式的文件扩展名和 MimeType。  
  
|**类型**|**扩展名**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|BMP|image/bmp|  
|GIF|GIF|image/gif|  
|JPEG|JPEG|image/jpeg|  
|PNG|PNG|image/png|  
|TIFF|tif|image/tiff|  
|EMF|EMF|image/emf|  
|EMFPlus|EMF|image/emf|  
  
  
##  <a name="RenderingMultiplePages"></a> 呈现多页  
 TIFF 是唯一一种支持在单个文件中包含多页文档的格式。 JPG 或 PNG 等其他格式一次只能输出一页并且需要单独为每页调用呈现扩展插件。  
  
  
##  <a name="Interactivity"></a> 交互  
 此呈现器生成的任何图像格式都不支持交互。 不会呈现以下交互元素：  
  
-   超链接  
  
-   显示或隐藏  
  
-   文档结构图  
  
-   钻取链接或点击链接  
  
-   最终用户排序  
  
-   固定标题  
  
-   书签  
  
  
##  <a name="DeviceInfo"></a> 设备信息设置  
 您可以通过更改设备信息设置来更改此呈现器的某些默认设置。 有关详细信息，请参阅 [Image Device Information Settings](../../reporting-services/image-device-information-settings.md)。  
  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同报表呈现扩展插件的交互功能（报表生成器和 SSRS）](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [呈现报表项（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
