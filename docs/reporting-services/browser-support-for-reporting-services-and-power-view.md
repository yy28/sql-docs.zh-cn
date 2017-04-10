---
title: "Reporting Services 和 Power View 的浏览器支持 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/30/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "显示报表"
  - "脚本 [Reporting Services], 要求"
  - "查看报表"
  - "浏览器 [Reporting Services]"
  - "Web 浏览器 [Reporting Services], 关于浏览器支持"
  - "浏览报表 (Reporting Services)"
  - "组件 [Reporting Services], 浏览器"
  - "Web 浏览器 [Reporting Services]"
ms.assetid: 48a75bbb-0029-4c43-891d-dc8f4fc0ebe1
caps.latest.revision: 121
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 121
---
# Reporting Services 和 Power View 的浏览器支持
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

了解支持哪些浏览器版本用于管理和查看 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]、ReportViewer 控件和 Power View。
  
 **适用于：**[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]本机模式 | [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式  
  
##  <a name="bkmk_webportal"></a> 浏览器要求 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]

以下是 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 当前支持的浏览器的列表。

**Microsoft Windows**  
*Windows 7、8.1、10；Windows Server 2008 R2、2012、2012 R2*
- Microsoft Edge (+)
- Microsoft Internet Explorer 10 或 11
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple iOS**  
*iPhone 和 iPad (iOS 9)*

- Apple Safari (+)

**Google Android**  
*Android 4.4 (KitKat) 或更高版本的手机或平板电脑*

- Google Chrome (+)

 **(+)** 最新公开发布的版本  
  
##  <a name="bkmk_reportviewer"></a> ReportViewer Web 控件 (2015) 的浏览器要求 
 以下是 ReportViewer Web 控件 (2015) 当前支持的浏览器的列表。 报表查看器支持从 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Web 门户和 SharePoint 库中查看报表。  
  
**Microsoft Windows**  
*Windows 7、8.1、10；Windows Server 2008 R2、2012、2012 R2*

- Microsoft Edge (+)
- Microsoft Internet Explorer 10 或 11
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)
  
 **(+)** 最新公开发布的版本  
  
 如果当前使用与 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 相集成的 SharePoint 产品，请参阅[在 SharePoint 2016 中计划浏览器支持](http://technet.microsoft.com//library/cc263526\(v=office.16\).aspx)。  
  
###  <a name="bkmk_authentication"></a> 身份验证要求  
 浏览器支持必须由报表服务器处理的特定身份验证方案，以使客户端请求获得成功。 下表标识 Windows 操作系统上运行的各浏览器支持的默认身份验证类型。  
  
|**浏览器类型**|**支持**|**浏览器默认值**|**服务器默认值**|  
|----------------------|------------------|-------------------------|------------------------|  
|**Microsoft Edge** (+)|协商、Kerberos、NTLM、基本|Negotiate|是。 默认身份验证设置使用 Edge。|  
|**Microsoft Internet Explorer**|协商、Kerberos、NTLM、基本|Negotiate|是。 默认身份验证设置使用 Internet Explorer。|  
|**Google Chrome**(+)|协商、NTLM、基本|Negotiate|是。 默认身份验证设置使用 Chrome。|  
|**Mozilla Firefox**(+)|NTLM、基本|NTLM|是。 默认身份验证设置使用 Firefox。|  
|**Apple Safari**(+)|NTLM、基本|基本|是。 默认身份验证设置使用 Safari。|  
  
 **(+)** 最新公开发布的版本  
  
### 查看报表的脚本要求  
 若要使用报表查看器，请将浏览器配置为可以运行脚本。  
  
 如果未启用脚本功能，则打开报表时将显示如下错误消息：  
  
-   **您的浏览器不支持脚本或已配置为不允许脚本运行。请单击此处在没有脚本的情况下查看此报表**。  
  
 如果选择查看不支持脚本的报表，则报表将会以 HTML 格式呈现，同时不具有报表工具栏和文档结构图等报表查看器功能。  
  
> [!NOTE]  
>  报表工具栏是 HTML 查看器组件的一部分。 默认情况下，该工具栏显示在浏览器窗口中呈现的每个报表的返回页首。 报表查看器提供的功能包括能够在报表中搜索信息、滚动到特定的页以及调整页大小以便查看。 有关报表工具栏或 HTML 查看器的详细信息，请参阅 [HTML Viewer and the Report Toolbar](../reporting-services/html-viewer-and-the-report-toolbar.md)。  
  
##  <a name="bkmk_controls"></a> Visual Studio 中 ReportViewer Web 服务器控件的浏览器支持  
 ReportViewer Web 服务器控件用于在 ASP.NET Web 应用程序中嵌入报表功能。 这些控件随 Visual Studio 一起提供，并且支持与本主题中所述的其他组件不同的浏览器和浏览器版本。 用于查看应用程序的浏览器类型确定您可以在应用程序中提供的 ReportViewer 功能类型。 使用本主题中提供的表确定哪些支持的浏览器受报表功能的限制以及支持的平台。  
  
 使用启用了脚本支持的浏览器。 如果浏览器无法运行脚本，则不能查看报表。  
  
**Microsoft Windows**  
*Windows 7、8.1、10；Windows Server 2008 R2、2012、2012 R2*

- Microsoft Edge (+)
- Microsoft Internet Explorer 10 或 11
- Google Chrome (+)
- Mozilla Firefox (+)
  
 **(+)** 最新公开发布的版本  
  
##  <a name="bkmk_powerview"></a> Power View 浏览器支持  

**Microsoft Windows**  
*Windows 7、8.1、10；Windows Server 2008 R2、2012、2012 R2*

- Microsoft Internet Explorer 10 或 11
- Mozilla Firefox (+)
  
**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)
  
 **(+)** 最新公开发布的版本  
  
 有关 SharePoint 2016 浏览器支持的详细信息，请参阅[在 SharePoint 2013 中计划浏览器支持](http://technet.microsoft.com//library/cc263526\(v=office.16\).aspx)。  
  
## 另请参阅  
[在 Web 门户中查找和查看报表（报表生成器和 SSRS）](http://msdn.microsoft.com/zh-cn/8556807e-f2e2-4a7b-bb1b-ac5ea1872e51)  
[Reporting Services 工具](../reporting-services/tools/reporting-services-tools.md)  
[Web 门户（SSRS 本机模式）](http://msdn.microsoft.com/zh-cn/7349e626-6ed5-4d21-b05f-cf042ad9ad70)  
[HTML 查看器和报表工具栏](../reporting-services/html-viewer-and-the-report-toolbar.md)  
[URL 访问参数引用](../reporting-services/url-access-parameter-reference.md)  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]
