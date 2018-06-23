---
title: 将设备信息设置传递给呈现扩展插件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- device information settings [Reporting Services]
- Render method
- Report Server Web service, device information settings
- Web service [Reporting Services], device information settings
- XML Web service [Reporting Services], device information settings
- passing device information [Reporting Services]
- rendering extensions [Reporting Services], device information settings
- rendering [Reporting Services], settings
- device information settings [Reporting Services], about device information settings
- extensions [Reporting Services], device information settings
ms.assetid: fe718939-7efe-4c7f-87cb-5f5b09caeff4
caps.latest.revision: 46
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 71eb9ad4d6066b6dbf3b0c942ee9d7e6f521a590
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125564"
---
# <a name="passing-device-information-settings-to-rendering-extensions"></a>将设备信息设置传递给呈现扩展插件
  在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]中，设备信息设置用于将呈现参数传递到呈现扩展插件。 报表服务器 Web 服务中的设置将以 **DeviceInfo** XML 元素的形式传递并由报表服务器进行处理。 由于设备信息设置均具有默认值，因此在呈现进程中可将其视为可选参数。 但是，您可以使用设备信息设置对呈现进行自定义并覆盖由服务器提供的默认值。  
  
 可以用多种方式指定设备信息设置。 可以通过编程方式使用 Render 方法。 如果要通过报表的 URL 访问报表，则可以指定设备信息作为 URL 参数。 还可以在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配置文件中编辑设备信息设置，以指定全局呈现参数。 有关全局指定呈现参数的详细信息，请参阅[在 RSReportServer.Config 中自定义呈现扩展插件参数](../../customize-rendering-extension-parameters-in-rsreportserver-config.md)。  
  
## <a name="passing-device-information-using-the-render-method"></a>使用 Render 方法传递设备信息  
 若要将设备信息设置传递给呈现扩展插件，请使用<xref:ReportExecution2005.ReportExecutionService.Render%2A>方法。 例如，当以 HTML 格式呈现时，可将以下 XML 字符串传递到 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法以创建一个 HTML 段落。  
  
```  
<DeviceInfo>  
   <HTMLFragment>True</HTMLFragment>  
</DeviceInfo>  
```  
  
 当报表作为 HTML 段落呈现时，报表的内容包含在 TABLE 元素内，而不使用 HTML 或 BODY 元素。 可以使用 HTML 段落将报表并入现有 HTML 文档中。 有关 HTML 输出的设备信息设置的详细信息，请参阅 [HTML 设备信息设置](../../html-device-information-settings.md)。  
  
## <a name="passing-device-information-using-url-access"></a>使用 URL 访问传递设备信息  
 您也可以通过 URL 访问传递设备信息设置。 设备信息设置以 URL 参数的形式传递。 可以将以下 URL 访问字符串传递到报表服务器以生成不带 HTML 查看器工具栏的所呈现报表。  
  
```  
http://<Server Name>/reportserver?/SampleReports/Sales Order Detail&rs:Command=Render&rs:Format=HTML4.0&rc:Toolbar=False  
```  
  
 有关详细信息，请参阅[在 URL 中指定设备信息设置](../../specify-device-information-settings-in-a-url.md)。  
  
## <a name="see-also"></a>请参阅  
 [呈现扩展插件的设备信息设置 (Reporting Services)](../../device-information-settings-for-rendering-extensions-reporting-services.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](../../customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [使用 Web 服务和.NET Framework 构建应用程序](building-applications-using-the-web-service-and-the-net-framework.md)  
  
  