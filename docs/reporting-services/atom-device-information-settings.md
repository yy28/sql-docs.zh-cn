---
title: ATOM 设备信息设置 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6eca493656f8254f9306c77efe73e8d7526f57ac
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43276042"
---
# <a name="atom-device-information-settings"></a>ATOM 设备信息设置
  用于 Atom 呈现扩展插件的设备信息设置支持要使用的 Atom 馈送和字符编码的名称的提交。  
  
 下表列出了用于向数据服务文档呈现的设备信息设置。  
  
|设置|ReplTest1|  
|-------------|-----------|  
|**DataFeed**|如果指定，则呈现与在此设置中提供的馈送名称相对应的 Atom 馈送。 如果未指定，则呈现报表的 Atom 服务文档。 数据馈送的唯一自动生成的标识符。 该值在内部使用，而且不应更改它。|  
|**编码**|.NET Framework 支持的字符编码的 Internet 编号分配机构 (IANA) 名称。 默认值为 **UTF-8**。 其他值的示例包括 ASCII、UTF-7 和 UTF-16。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [将设备信息设置传递给呈现扩展插件](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../reporting-services/technical-reference-ssrs.md)  
  
  
