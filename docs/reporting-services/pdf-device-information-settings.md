---
title: PDF 设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
caps.latest.revision: 41
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 0f0ec8d6bfe88182f84078aa8155afed9f149828
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="pdf-device-information-settings"></a>PDF 设备信息设置
  下表列出以 PDF 格式呈现报表时的设备信息设置。  
  
|设置|ReplTest1|  
|-------------|-----------|  
| AccessiblePDF | 指示是否呈现可访问/已标记的 PDF，此 PDF 大小更大，但更易于屏幕阅读器和其他辅助技术读取和导航。 默认值是 **false**秒。 [在 Power BI 报表服务器（2018 年 3 月版）及更高版本中可用] |
|**“列”**|要为报表设置的列数。 此值将覆盖报表的原始设置。|  
|**ColumnSpacing**|要为报表设置的列间距。 此值将覆盖报表的原始设置。|  
|**DpiX**|输出设备在 X 方向的分辨率。|  
|**DpiY**|输出设备在 Y 方向的分辨率。|  
|**EndPage**|要呈现的报表的最后一页。 默认值为 **StartPage**的值。|  
|**HumanReadablePDF**|指示是否呈现未压缩的 PDF 文件，此文件大小更大，但在纯文本编辑器中更易于人们阅读。 默认值为 **false.**|  
|**MarginBottom**|要为报表设置的下边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如，1in）。 此值将覆盖报表的原始设置。|  
|**MarginLeft**|要为报表设置的左边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如，1in）。 此值将覆盖报表的原始设置。|  
|**MarginRight**|要为报表设置的右边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如，1in）。 此值将覆盖报表的原始设置。|  
|**MarginTop**|要为报表设置的上边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如，1in）。 此值将覆盖报表的原始设置。|  
|**PageHeight**|要为报表设置的页高，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如，11in）。 此值将覆盖报表的原始设置。|  
|**PageWidth**|要为报表设置的页宽，以英寸为单位。 您必须包含一个整数或十进制值，后跟“in”（例如，8.5in）。 此值将覆盖报表的原始设置。|  
|**StartPage**|要呈现的报表的第一页。 值为 **0** 指示将呈现所有页。 默认值是 **1**秒。|  
  
## <a name="see-also"></a>另请参阅  
 [将设备信息设置传递给呈现扩展插件](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../reporting-services/technical-reference-ssrs.md)  
  
  
