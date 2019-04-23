---
title: PDF 设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 29274efcc4bc88c13537d240efcbc9ce4b25ea58
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59962735"
---
# <a name="pdf-device-information-settings"></a>PDF 设备信息设置
  下表列出以 PDF 格式呈现报表时的设备信息设置。  
  
|设置|ReplTest1|  
|-------------|-----------|  
|**“列”**|要为报表设置的列数。 此值将覆盖报表的原始设置。|  
|**ColumnSpacing**|要为报表设置的列间距。 此值将覆盖报表的原始设置。|  
|**DpiX**|输出设备在 X 方向的分辨率。|  
|**DpiY**|输出设备在 Y 方向的分辨率。|  
|**EndPage**|要呈现的报表的最后一页。 默认值为 `StartPage` 的值。|  
|`HumanReadablePDF`|指示是否应压缩 PDF，这使得源更易于读取。 默认值为 `false.`|  
|**MarginBottom**|要为报表设置的下边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如，1in）。 此值将覆盖报表的原始设置。|  
|**MarginLeft**|要为报表设置的左边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如，1in）。 此值将覆盖报表的原始设置。|  
|**MarginRight**|要为报表设置的右边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如，1in）。 此值将覆盖报表的原始设置。|  
|**MarginTop**|要为报表设置的上边距值，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如，1in）。 此值将覆盖报表的原始设置。|  
|**PageHeight**|要为报表设置的页高，以英寸为单位。 必须包含一个整数或小数值，后跟“in”（例如，11in）。 此值将覆盖报表的原始设置。|  
|**PageWidth**|要为报表设置的页宽，以英寸为单位。 您必须包含一个整数或十进制值，后跟“in”（例如，8.5in）。 此值将覆盖报表的原始设置。|  
|`StartPage`|要呈现的报表的第一页。 值为 `0` 指示将呈现所有页。 默认值为 `1`。|  
  
## <a name="see-also"></a>请参阅  
 [将设备信息设置传递给呈现扩展插件](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
