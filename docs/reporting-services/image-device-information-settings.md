---
title: "图像设备信息设置 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- images [Reporting Services], rendering
- device information settings [Reporting Services], IMAGE rendering
ms.assetid: edad9498-69f7-4726-8699-fa615f704dff
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 528ff1aac617e36ac8b3faeed0bad0981479f651
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="image-device-information-settings"></a>图像设备信息设置
  下表列出了用于以 IMAGE 格式呈现的设备信息设置。  
  
|设置|“值”|  
|-------------|-----------|  
|**列**|要为报表设置的列数。 此值将覆盖报表的原始设置。|  
|**ColumnSpacing**|要为报表设置的列间距。 此值将覆盖报表的原始设置。|  
|**DpiX**|输出图像的水平分辨率。 默认值为 **96**。 适用于 **BMP**、 **GIF**、 **PNG**和 **TIFF** 输出格式。|  
|**DpiY**|输出图像的垂直分辨率。 默认值为 **96**。 适用于 **BMP**、 **GIF**、 **PNG**和 **TIFF** 输出格式。|  
|**EndPage**|要呈现的报表的最后一页。 默认值为 **StartPage**的值。|  
|**MarginBottom**|要为报表设置的下边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如， **1in**）。 此值将覆盖报表的原始设置。|  
|**MarginLeft**|要为报表设置的左边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如， **1in**）。 此值将覆盖报表的原始设置。|  
|**MarginRight**|要为报表设置的右边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如， **1in**）。 此值将覆盖报表的原始设置。|  
|**MarginTop**|要为报表设置的上边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如， **1in**）。 此值将覆盖报表的原始设置。|  
|**OutputFormat**|[!INCLUDE[ndptecgdiexpanded](../includes/ndptecgdiexpanded-md.md)] ([!INCLUDE[ndptecgdi](../includes/ndptecgdi-md.md)]) 受支持的输出格式之一： **BMP**、 **EMF**、 **GIF**、 **JPEG**、 **PNG**或 **TIFF**。|  
|**PageHeight**|要为报表设置的页高，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如， **11in**）。 此值将覆盖报表的原始设置。|  
|**PageWidth**|要为报表设置的页宽，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如， **8.5in**）。 此值将覆盖报表的原始设置。|  
|**PrintDpiX**|输出图像的水平分辨率。 默认值是 **300**秒。 适用于增强型图元文件 (**EMF**) 输出格式。|  
|**PrintDpiY**|输出图像的垂直分辨率。 默认值是 **300**秒。 适用于增强型图元文件 (**EMF**) 输出格式。|  
|**StartPage**|要呈现的报表的第一页。 值为 **0** 指示将呈现所有页。 默认值是 **1**秒。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [将设备信息设置传递给呈现扩展插件](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [自定义在 RSReportServer.Config 中的呈现扩展插件参数](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 &#40;SSRS &#41;](../reporting-services/technical-reference-ssrs.md)  
  
  

