---
title: 图像设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- images [Reporting Services], rendering
- device information settings [Reporting Services], IMAGE rendering
ms.assetid: edad9498-69f7-4726-8699-fa615f704dff
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 32498fbed24ddab591745ae1d01c5f123e976114
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109013"
---
# <a name="image-device-information-settings"></a>图像设备信息设置
  下表列出了用于以 IMAGE 格式呈现的设备信息设置。  
  
|设置|ReplTest1|  
|-------------|-----------|  
|**“列”**|要为报表设置的列数。 此值将覆盖报表的原始设置。|  
|**ColumnSpacing**|要为报表设置的列间距。 此值将覆盖报表的原始设置。|  
|`DpiX`|输出图像的水平分辨率。 默认值为 **96**。 适用于`BMP`， `GIF`， `PNG`，和`TIFF`输出格式。|  
|`DpiY`|输出图像的垂直分辨率。 默认值为 **96**。 适用于`BMP`， `GIF`， `PNG`，和`TIFF`输出格式。|  
|**EndPage**|要呈现的报表的最后一页。 默认值为 `StartPage` 的值。|  
|**MarginBottom**|要为报表设置的下边距值，以英寸为单位。 您必须包含一个整数或小数值，后跟“in”（例如，`1in`）。 此值将覆盖报表的原始设置。|  
|**MarginLeft**|要为报表设置的左边距值，以英寸为单位。 您必须包含一个整数或小数值，后跟“in”（例如，`1in`）。 此值将覆盖报表的原始设置。|  
|**MarginRight**|要为报表设置的右边距值，以英寸为单位。 您必须包含一个整数或小数值，后跟“in”（例如，`1in`）。 此值将覆盖报表的原始设置。|  
|**MarginTop**|要为报表设置的上边距值，以英寸为单位。 您必须包含一个整数或小数值，后跟“in”（例如，`1in`）。 此值将覆盖报表的原始设置。|  
|**OutputFormat**|[!INCLUDE[ndptecgdiexpanded](../includes/ndptecgdiexpanded-md.md)] ([!INCLUDE[ndptecgdi](../includes/ndptecgdi-md.md)]) 支持的输出格式之一：`BMP`、`EMF`、`GIF`、`JPEG`、`PNG` 或 `TIFF`。|  
|**PageHeight**|要为报表设置的页高，以英寸为单位。 您必须包含一个整数或小数值，后跟“in”（例如，`11in`）。 此值将覆盖报表的原始设置。|  
|**PageWidth**|要为报表设置的页宽，以英寸为单位。 您必须包含一个整数或小数值，后跟“in”（例如，`8.5in`）。 此值将覆盖报表的原始设置。|  
|**PrintDpiX**|输出图像的水平分辨率。 默认值是 `300`。 适用于增强型图元文件 (`EMF`) 输出格式。|  
|**PrintDpiY**|输出图像的垂直分辨率。 默认值为 `300`。 适用于增强型图元文件 (`EMF`) 输出格式。|  
|`StartPage`|要呈现的报表的第一页。 值为 `0` 指示将呈现所有页。 默认值是 `1`。|  
  
## <a name="see-also"></a>请参阅  
 [将设备信息设置传递给呈现扩展插件](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
