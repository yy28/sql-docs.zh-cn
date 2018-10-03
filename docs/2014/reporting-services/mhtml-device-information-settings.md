---
title: MHTML 设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], MHTML rendering
- MHTML [Reporting Services]
ms.assetid: 60b85dd8-b4fb-4ad9-be6a-e7c89ac076fe
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: dd75a21625eb3ab31c9b1655e0f85943470cee54
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117457"
---
# <a name="mhtml-device-information-settings"></a>MHTML 设备信息设置
  下表列出的是以 Web 存档 (MHTML) 格式呈现报表时的设备信息设置。  
  
|设置|ReplTest1|  
|-------------|-----------|  
|**JavaScript**|指示是否在所呈现报表中支持 JavaScript。|  
|**OutlookCompat**|指示是否呈现可改善报表在 Outlook 中的外观的额外元数据。 默认值是 `true`。|  
|**MHTML 片段**|指示是否创建一个 MHTML 片段以取代完整 MHTML 文档。 MHTML 片段包含 TABLE 元素中的报表内容，并忽略 HTML 和 BODY 元素。 默认值是 `false`。|  
|**DataVisualizationFitSizing**|指示 tablix 内数据可视化调整大小行为。 这包括图表、仪表和地图。<br /><br /> 可能的值包括 **“近似”** 和 **“精确”**。<br /><br /> 默认值为 **“近似”**。 如果从 **rsreportserver.config** 文件删除该设置，则默认行为为 **“精确”**。<br /><br /> 启用 **“精确”** 可能会影响性能，因为确定精确大小所需的处理时间可能更长。|  
  
## <a name="see-also"></a>请参阅  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [将设备信息设置传递给呈现扩展插件](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
