---
title: Excel 设备信息设置 | Microsoft Docs
description: 详细了解各种设备信息设置以使用 Microsoft Excel 格式进行呈现。
ms.date: 01/23/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], Excel rendering
- Excel [Reporting Services], rendering
ms.assetid: bb5f3566-f033-4470-be87-1f52fb7a4ab6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c4d84c98923a3cee94f64fed863e621821bd7a39
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245126"
---
# <a name="excel-device-information-settings"></a>Excel 设备信息设置
  下表列出以 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 格式呈现时的设备信息设置。  
  
|设置|值|  
|-------------|-----------|  
|**OmitDocumentMap**|指示是否对于支持文档结构图的报表忽略文档结构图。 默认值是 **false**秒。|  
|**OmitFormulas**|指示是否对所呈现报表忽略公式。 默认值是 **false**秒。|  
|**SimplePageHeaders**|指示是否将报表的页眉呈现到 Excel 页眉。 值为 **false** 指示将页眉呈现到工作表的第一行。 默认值是 **false**秒。|  
|**DynamicImageDpi**|动态图像（如图表、仪表和地图）的分辨率。 默认值为 **96**。 （在 Power BI 报表服务器(2020 年 1 月版)及更高版本中可用）|  

  
## <a name="see-also"></a>另请参阅  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [将设备信息设置传递给呈现扩展插件](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../reporting-services/technical-reference-ssrs.md)  
  
  
