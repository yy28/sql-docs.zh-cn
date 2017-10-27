---
title: "实现 IRenderingExtension 接口 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- IRenderingExtension interface
- rendering extensions [Reporting Services], IRenderingExtension interface
ms.assetid: 74b2f2b7-6796-42da-ab7d-b05891ad4001
caps.latest.revision: 43
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 60eac755180faaba012c7fbd14001fcb66a37975
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-the-irenderingextension-interface"></a>实现 IRenderingExtension 接口
  呈现扩展插件从与实际数据相结合的报表定义中获取结果，并将得到的数据呈现为某种可用的格式。 组合的数据和格式的转换是通过一个实现 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> 的公共语言运行时 (CLR) 类完成的。 该类将对象模型转换为可由查看器、打印机或其他输出目标使用的输出格式。  
  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> 具有三个必须进行编码的方法：  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> - 呈现报表。  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> - 呈现报表中特定的流。  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> - 获取报表所需的其他信息，如图标。  
  
 下列各节更为详细地讨论这些方法。  
  
## <a name="render-method"></a>Render 方法  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> 方法包含表示以下对象的参数：  
  
-   *报表*你想要呈现。 此对象包含报表的属性、数据和布局信息。 report 是报表对象模型树的根。  
  
-   *ServerParameters*如果任何包含具有报表服务器的参数的字符串字典对象。  
  
-   *DeviceInfo*包含的设备设置的参数。 有关详细信息，请参阅[传递设备信息设置应用于呈现扩展](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)。  
  
-   *ClientCapabilities*参数，其中包含<xref:System.Collections.Specialized.NameValueCollection>字典对象具有与其呈现客户端信息。  
  
-   *RenderProperties* ，包含有关呈现结果信息。  
  
-   *CreateAndRegisterStream*是委托函数调用以获取流以将呈现到。  
  
### <a name="deviceinfo-parameter"></a>deviceInfo 参数  
 *DeviceInfo*参数包含呈现参数，不报表参数。 这些呈现参数将传递给呈现扩展插件。 *DeviceInfo*值会转换为<xref:System.Collections.Specialized.NameValueCollection>由报表服务器的对象。 中的项*deviceInfo*参数被视为不区分大小写的值。 如果由于 URL 发出的呈现请求访问，在窗体中的 URL 参数`rc:key=value`转换为键/值对中的*deviceInfo*字典对象。 浏览器检测代码还提供了中的以下项*clientCapabilities*字典： EcmaScriptVersion、 JavaScript、 MajorVersion、 MinorVersion、 Win32、 类型和 AcceptLanguage。 任何名称/值对中的*deviceInfo*不理解的呈现扩展插件的参数将被忽略。 以下代码示例显示用于检索图标的示例 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 方法：  
  
```csharp  
public void GetRenderingResource (CreateStream createStreamCallback, NameValueCollection deviceInfo)  
{  
    string[] iconTagValues = deviceInfo.GetValues("Icon");  
    if ((iconTagValues != null) && (iconTagValues.Length > 0) )  
    {  
        // Create a stream to output to.  
        Stream outputStream = createStreamCallback(m_iconResourceName, "gif", null, "image/gif", false);  
        // Get the GIF image for one of the buttons on the toolbar  
        Image requiredImage = (Image) m_resourcemanager.GetObject(m_iconResourceName  
        // Write the image to the output stream  
        requiredImage.Save(outputStream, requiredImage.RawFormat);  
    }  
    return;  
}  
```  
  
## <a name="renderstream-method"></a>RenderStream 方法  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> 方法呈现报表中的特定流。 所有流都是在初始 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> 调用过程中创建的，但最初不向客户端返回这些流。 此方法用于辅助流（如 HTML 呈现中的图像）或多页呈现扩展插件的其他页（如图像/EMF）。  
  
## <a name="getrenderingresource-method"></a>GetRenderingResource 方法  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 方法检索信息而不执行报表的完整呈现。 有时，报表所需的信息并不要求呈现此报表本身。 例如，如果你需要与呈现扩展插件关联的图标，则使用*deviceInfo*参数，其中包含一个标记**\<图标 >**。 在此类情况下，可以使用 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 方法。  
  
## <a name="see-also"></a>另请参阅  
 [实现的呈现扩展插件](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [呈现扩展插件概述](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
  
  

