---
title: Excel 设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], Excel rendering
- Excel [Reporting Services], rendering
ms.assetid: bb5f3566-f033-4470-be87-1f52fb7a4ab6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d71c83195c8f91984bbbce95bd00402928fdb36e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109208"
---
# <a name="excel-device-information-settings"></a>Excel 设备信息设置
  下表列出以 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 格式呈现时的设备信息设置。  
  
|设置|值|  
|-------------|-----------|  
|**OmitDocumentMap**|指示是否对于支持文档结构图的报表忽略文档结构图。 默认值为 `false`。|  
|**OmitFormulas**|指示是否对所呈现报表忽略公式。 默认值为 `false`。|  
|`SimplePageHeade`rs|指示是否将报表的页眉呈现到 Excel 页眉。 值为 `false` 指示将页眉呈现到工作表的第一行。 默认值为 `false`。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [将设备信息设置传递给呈现扩展插件](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 Rsreportserver.config 中自定义呈现扩展插件参数](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
