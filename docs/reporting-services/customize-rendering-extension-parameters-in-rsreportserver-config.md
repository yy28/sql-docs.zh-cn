---
title: 在 RSReportServer.Config 中自定义呈现扩展插件参数 | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- configuration options [Reporting Services]
- DeviceInfo settings
- rendering extensions [Reporting Services], overriding behaviors
- parameters [Reporting Services], report rendering
- overriding report rendering behavior
- extensions [Reporting Services], rendering
ms.assetid: 3bf7ab2b-70bb-41c8-acda-227994d15aed
caps.latest.revision: 31
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 00f7c8ec10f402e8c1246f81c5ab929536ebb024
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="customize-rendering-extension-parameters-in-rsreportserverconfig"></a>在 RSReportServer.Config 中自定义呈现扩展插件参数
  可以在 RSReportServer 配置文件中指定呈现扩展插件参数，以覆盖在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器上运行的报表的默认报表呈现行为。 可通过修改呈现扩展插件参数来实现以下目标：  
  
-   更改呈现扩展插件名称在报表工具栏的“导出”列表中的显示方式（例如，将“Web 存档”更改为“MHTML”），或将该名称本地化为其他语言。  
  
-   创建同一呈现扩展插件的多个实例以支持不同的报表显示选项（例如，图像呈现扩展插件的纵向模式和横向模式版本）。  
  
-   更改默认的呈现扩展插件参数以使用不同的值（例如，图像呈现扩展插件使用 TIFF 作为默认输出格式；您可以修改扩展插件参数以改用 EMF）。  
  
 更改呈现扩展插件参数只影响报表服务器上的呈现操作。 您不能覆盖报表设计器的报表预览中的呈现扩展插件设置。  
  
 在配置文件中指定呈现扩展插件参数会在全局范围内对呈现扩展插件产生影响。 无论何时使用某个特定的呈现扩展插件，都会使用配置文件中的设置来替代默认值。 如果要为特定的报表或呈现操作设置呈现扩展插件参数，必须使用 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法或者通过对报表 URL 指定设备信息设置来以编程方式指定设备信息。 有关为呈现操作指定设备信息设置以及查看设备信息设置完整列表的详细信息，请参阅 [将设备信息设置传递给呈现扩展插件](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)。  
  
## <a name="finding-and-modifying-rsreportserverconfig"></a>查找并修改 RSReportServer.config  
 报表输出格式的配置设置被指定为 RSReportServer.config 文件中的呈现扩展插件参数。 若要在配置文件中指定呈现扩展插件参数，必须知道如何定义用于设置呈现参数的 XML 结构。 有两种 XML 结构可以修改：  
  
-   **OverrideNames** 元素定义呈现扩展插件的显示名称和语言。  
  
-   **DeviceInfo** XML 结构定义呈现扩展插件使用的设备信息设置。 大多数呈现扩展插件参数作为设备信息设置进行指定。  
  
 可以使用文本编辑器修改该文件。 可在 \Reporting Services\Report Server\Bin 文件夹中找到 RSReportServer.config 文件。 有关修改配置文件的详细信息，请参阅[修改 Reporting Services 配置文件 (RSreportserver.config)](../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
## <a name="changing-the-display-name"></a>更改显示名称  
 呈现扩展插件的显示名称显示在报表工具栏的“导出”列表中。 默认显示名称的示例包括 Web 存档、TIFF 文件和 Acrobat (PDF) 文件。 通过在配置文件中指定 **OverrideNames** 元素，可以将默认的显示名称替换为自定义值。 此外，如果您要定义单个呈现扩展插件的两个实例，则可在“导出”列表中使用 **OverrideNames** 元素来区分每个实例。  
  
 由于显示名称已本地化，因此如果要用自定义值来替换默认的显示名称，必须设置 **Language** 属性。 否则，将忽略您指定的任何名称。 设置的语言值必须对报表服务器计算机有效。 例如，如果报表服务器在法语操作系统中运行，则应该指定“fr-FR”作为属性值。  
  
 下面的示例说明了如何在英文报表服务器上提供自定义名称：  
  
```  
<Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering">  
   <OverrideNames>  
     <Name Language="en-US">My Custom Display Name for XML Rendering</Name>  
   </OverrideNames>  
</Extension>  
```  
  
## <a name="changing-device-information-settings"></a>更改设备信息设置  
 若要修改已在报表服务器上部署的呈现扩展插件所使用的默认设备信息设置，必须在配置文件中键入 **DeviceInfo** XML 结构。 每个呈现扩展插件都支持对该扩展插件唯一的设备信息设置。 若要查看设备信息设置的完整列表，请参阅 [将设备信息设置传递给呈现扩展插件](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)。  
  
 以下示例对用于修改图像呈现扩展插件的默认设置的 XML 结构和语法进行了说明：  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">Image (EMF)</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <ColorDepth>32</ColorDepth>  
                <DpiX>300</DpiX>  
                <DpiY>300</DpiY>  
                <OutputFormat>EMF</OutputFormat>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="configuring-multiple-entries-for-a-rendering-extension"></a>为呈现扩展插件配置多个项  
 可以创建同一呈现扩展插件的多个实例，以支持不同的报表显示选项。 定义的每个实例都可以具有不同的参数值组合。 定义现有呈现扩展插件的新实例时，请确保执行以下操作：  
  
-   为该扩展插件指定唯一名称。  
  
     每个实例都必须具有唯一的 **Name** 属性值。 以下示例使用“IMAGE (EMF Landscape)”和“IMAGE (EMF Portrait)”名称来区分两个实例。  
  
     更改已部署的呈现扩展插件的名称时要谨慎。 以编程方式指定呈现扩展插件的开发人员将使用扩展插件名称来标识要为某个特定的呈现操作使用哪一个实例。 如果在报表服务器上运行自定义 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 应用程序，请确保开发人员知道您是要修改现有扩展插件名称还是要添加新名称。  
  
-   指定唯一的显示名称，以便用户了解输出格式之间的差异。  
  
     若要配置同一扩展插件的多个版本，可以通过为 **OverrideNames**提供一个值来为每个版本提供唯一名称。 否则，该扩展插件的所有版本在报表工具栏上的“导出”选项列表中都具有相同的名称。  
  
 以下示例阐释了当存在采用横向模式以 EMF 格式输出报表的第二个实例时，如何使用默认的图像呈现扩展插件（该插件生成 TIFF 输出）在纵向模式下输出 EMF。 注意，每个扩展插件名称都是唯一的。 测试此示例时，请记住选择不包含交互式功能的报表，如显示/隐藏选项、矩阵或钻取链接（交互式功能在图像呈现扩展插件中不起作用）：  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF Landscape)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Landscape Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>8.5in</PageHeight>  
                <PageWidth>11in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
    <Extension Name="IMAGE (EMF Portrait)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Portait Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>11in</PageHeight>  
                <PageWidth>8.5in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="see-also"></a>另请参阅  
 [RsReportServer.config 配置文件](../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [RSReportDesigner 配置文件](../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [CSV 设备信息设置](../reporting-services/csv-device-information-settings.md)   
 [Excel 设备信息设置](../reporting-services/excel-device-information-settings.md)   
 [HTML 设备信息设置](../reporting-services/html-device-information-settings.md)   
 [图像设备信息设置](../reporting-services/image-device-information-settings.md)   
 [MHTML 设备信息设置](../reporting-services/mhtml-device-information-settings.md)   
 [PDF 设备信息设置](../reporting-services/pdf-device-information-settings.md)   
 [XML 设备信息设置](../reporting-services/xml-device-information-settings.md)  
  
  
