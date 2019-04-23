---
title: 规划 Reporting Services 和 Power View 浏览器支持 (Reporting Services 2014)
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 58ed105619ca5ad5eadb00271e18ddaa10c6bfe3
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59953953"
---
# <a name="planning-for-reporting-services-and-power-view-browser-support-reporting-services-2014"></a>规划 Reporting Services 和 Power View 浏览器支持 (Reporting Services 2014)
  在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中，可以使用 Web 浏览器查看报表和运行报表管理器。 并非所有浏览器都支持所有的报表功能。 本主题将说明对于报表管理器管理功能、查看报表、Visual Studio 中的报表查看器控件的支持和要求。 本主题还将概述对于支持的浏览器的功能可用性、身份验证要求和脚本要求。  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式 | [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 本机模式  
  
 **本主题内容：**  
  
- [Power View 浏览器方案](#bkmk_powerview)  
  
- [报表管理器浏览器要求 （本机模式）](#bkmk_reportmanager)  
  
- [查看报表的浏览器要求](#bkmk_reportviewer)  
  
- [身份验证要求](#bkmk_authentication)  
  
- [在 Visual Studio 中 ReportViewer Web 服务器控件的浏览器支持](#bkmk_controls)  
  
##  <a name="bkmk_powerview"></a> Power View 浏览器方案

 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 支持的受支持的浏览器和浏览器版本的列表取决于打开的文档类型。 Excel 2013 工作簿和"**.rdlx**"文件使用的不同组件。  
  
|文档类型|环境|浏览器支持|  
|-------------------|-----------------|---------------------|  
|Power View 报表 (.RDLX)|**SharePoint Server：** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] SharePoint 集成模式上的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 和 Power View Web 应用程序。|请参阅[的 Power View 在 SharePoint 服务器和 Reporting Services SharePoint 集成的模式上](#bkmk_powerview_on_SSRS)。|  
|使用 Power View 工作表的 Excel 2013 工作簿|**SharePoint Server:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] Excel Services 中。<br /><br /> **SharePoint Online (Office 365):** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] Excel Web app。|请参阅[联机 Power 视图上 Excel Services 或 SharePoint 上的 Excel Web App](#bkmk_powerview_on_ExcelServices)。|  
  
###  <a name="bkmk_powerview_on_SSRS"></a> SharePoint 服务器和 Reporting Services SharePoint 集成的模式上的 power View  
 下表总结了当用户在具有为 SharePoint 安装和配置的 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 服务应用程序和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序的 SharePoint 场中打开 Power View 报表 (.RDLX) 时支持的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 浏览器版本。  
  
- 此表适用于 SharePoint 2010 和 SharePoint 2013。  
  
- 有关 SharePoint 2013 浏览器支持的详细信息，请参阅[计划在 SharePoint 2013 中的浏览器支持](https://technet.microsoft.com//library/cc263526\(office.15\).aspx)(https://technet.microsoft.com/library/cc263526(office.15).aspx)。  
  
- 有关 SharePoint 2010 浏览器支持的详细信息，请参阅[计划浏览器支持 (SharePoint Server 2010)](https://technet.microsoft.com/library/cc263526\(office.14\).aspx) (https://technet.microsoft.com/library/cc263526(office.14).aspx)。  
  
|**浏览者**|**Windows 8 和 8.1**|**Windows 7**|**Windows Server 2012 和 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6 - 10.9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 （适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 10 （适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 9**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|  
|**Internet Explorer 8**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|  
|**Mozilla Firefox (最新公开发布的版本)**|32 位|32 位|32 位|32 位|32 位|不支持|  
|**Apple Safari (最新公开发布的版本)**|不支持|不支持|不支持|不支持|不支持|32 位、64 位|  
  
> [!NOTE]  
> “32 位”指的是浏览器，而不是操作系统。 例如，在 64 位的 Windows 7 上可以使用 32 位的 Internet Explorer 9。  
  
#### <a name="inprivate-browsing-feature-in-internet-explorer"></a>Internet Explorer 中的 InPrivate 浏览功能

 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 不支持 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 8 和 Internet Explorer 9 中的 InPrivate 浏览功能。 有关 InPrivate 浏览的详细信息，请参阅[什么是 InPrivate 浏览？](http://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing) (http://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing).  
  
###  <a name="bkmk_powerview_on_ExcelServices"></a> 在 Excel Services 或 SharePoint Online 上的 Excel Web App 的 power View

 下表汇总了当用户在运行 Excel Services 的 SharePoint Server 上使用 Power View 工作表打开 Excel 2013 工作簿时支持的 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 的浏览器版本：  
  
-   有关 SharePoint 2013 浏览器支持的详细信息，请参阅[计划在 SharePoint 2013 中的浏览器支持](https://technet.microsoft.com/library/cc263526\(office.15\).aspx)(https://technet.microsoft.com/library/cc263526(office.15).aspx)。  
  
|**浏览者**|**Windows 8 和 8.1**|**Windows 7**|**Windows Server 2012 和 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6 - 10.9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 （适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 10 （适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 9**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|  
|**Internet Explorer 8**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|  
|**Mozilla Firefox (最新公开发布的版本)**|32 位|32 位|32 位|32 位|32 位|32 位、64 位|  
|**Apple Safari (最新公开发布的版本)**|不支持|不支持|不支持|不支持|不支持|32 位、64 位|  
|**Google Chrome (最新公开发布的版本)**|32 位 **(\*)** 有限的时间|32 位 **(\*)** 有限的时间|32 位 **(\*)** 有限的时间|32 位 **(\*)** 有限的时间|32 位 **(\*)** 有限的时间|不支持|  
  
 **(\*)** Chrome 将停止支持 Netscape 插件 API (NPAPI)，由 Silverlight。 Power View 依赖于 Silverlight。  有关详细信息，请参阅 [“NPAPI 最终倒计时”](http://blog.chromium.org/2014/11/the-final-countdown-for-npapi.html)。  
  
##  <a name="bkmk_reportmanager"></a> 报表管理器浏览器要求 （本机模式）

 下面是可以用于运行 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 本机模式报表管理器以便管理报表和报表服务器的支持的浏览器的当前列表。  
  
|浏览者|  
|-------------|  
|Internet Explorer 7 或更新版本且必须启用了脚本撰写功能。|  
|Mozilla FireFox (最新公开发布的版本)|  
|Apple Safari (最新公开发布的版本)|  
|Google Chrome (最新公开发布的版本)|  
  
##  <a name="bkmk_reportviewer"></a> 查看报表的浏览器要求

 以下是报表查看器支持的浏览器和功能的当前列表。 报表查看器支持从 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表管理器和 SharePoint 库查看报表。  
  
|**浏览者**|**Windows 8 和 8.1**|**Windows 7**|**Windows Server 2012 和 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6 - 10.9**|**iOS 6 -7 for iPad**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|----------------------------|  
|**Internet Explorer 11 （适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|不支持|不支持|  
|**Internet Explorer 10 （适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|不支持|不支持|  
|**Internet Explorer 9**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 8**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 7**|不支持|不支持|不支持|不支持|32 位、64 位|不支持|不支持|  
|**Mozilla Firefox (最新公开发布的版本)**|32 位|32 位|32 位|32 位|32 位|不支持|不支持|  
|**Apple Safari (最新公开发布的版本)**|不支持|不支持|不支持|不支持|不支持|32 位、64 位|支持但具有受限功能<sup>(1)</sup>|  
|**Google Chrome (最新公开发布的版本)**|32 位|32 位|32 位|32 位|32 位|不支持|不支持|  
  
 **<sup>(1)</sup>**  支持以下功能：  
  
- 导出为 PDF 和 TIFF 格式。  
  
- 在 iOS 设备上的 Apple Safari 中以交互方式查看报表。 功能支持包括展开/折叠、参数窗格和交互式排序。  
  
- 有关详细信息，请参阅[Microsoft Surface 设备和 Apple iOS 设备上查看 Reporting Services 报表](../../2014/reporting-services/view-reporting-services-reports-surface-ios-devices.md)。  
  
 **注意** 如果从 Macintosh 计算机访问报表服务器，则建议使用 Safari。 如果在使用 SharePoint 产品与集成[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，请参阅[计划浏览器支持 (Windows SharePoint Services)](https://go.microsoft.com/fwlink/?LinkId=183583)。  
  
### <a name="url-access-for-viewing-reports"></a>查看报表的 URL 访问

 若要直接查看报表而不是通过报表管理器查看报表，可以使用 URL 访问链接到报表和报表查看器。 URL 访问支持多种浏览器。  
  
 有关 URL 访问的详细信息，请参阅以下主题：  
  
- [URL 访问参数引用](url-access-parameter-reference.md)  
  
###  <a name="bkmk_authentication"></a> 身份验证要求

 浏览器支持必须由报表服务器处理的特定身份验证方案，以使客户端请求获得成功。 下表标识 Windows 操作系统上运行的各浏览器支持的默认身份验证类型。  
  
|**浏览器类型**|**支持**|**浏览器默认值**|**服务器默认值**|  
|----------------------|------------------|-------------------------|------------------------|  
|**Internet Explorer**|协商、Kerberos、NTLM、基本|Negotiate|是。 默认身份验证设置使用 Internet Explorer。|  
|**Firefox**|NTLM、基本|NTLM|是。 默认身份验证设置使用 Firefox。|  
|**Safari**|基本|基本|是。 默认身份验证设置使用 Safari。|  
|**Chrome**|协商、NTLM、基本|协商|是。 默认身份验证设置使用 Chrome。|  
  
### <a name="script-requirements"></a>脚本要求

 若要使用报表查看器，请将浏览器配置为可以运行脚本。  
  
 如果未启用脚本功能，则打开报表时将显示如下错误消息：  
  
- **在浏览器不支持脚本或已配置为不允许脚本运行。单击此处查看不含脚本的报表**。  
  
 如果选择查看不支持脚本的报表，则报表将会以 HTML 格式呈现，同时不具有报表工具栏和文档结构图等报表查看器功能。  
  
> [!NOTE]  
> 报表工具栏是 HTML 查看器组件的一部分。 默认情况下，该工具栏显示在浏览器窗口中呈现的每个报表的返回页首。 报表查看器提供的功能包括能够在报表中搜索信息、滚动到特定的页以及调整页大小以便查看。 有关报表工具栏或 HTML 查看器的详细信息，请参阅 [HTML Viewer and the Report Toolbar](html-viewer-and-the-report-toolbar.md)。  
  
##  <a name="bkmk_controls"></a> 在 Visual Studio 中 ReportViewer Web 服务器控件的浏览器支持

 ReportViewer Web 服务器控件用于在 ASP.NET Web 应用程序中嵌入报表功能。 这些控件随 Visual Studio 一起提供，并且支持与本主题中所述的其他组件不同的浏览器和浏览器版本。 用于查看应用程序的浏览器类型确定您可以在应用程序中提供的 ReportViewer 功能类型。 使用本主题中提供的表确定哪些支持的浏览器受报表功能的限制以及支持的平台。  
  
 由于支持的浏览器的呈现引擎不同，一些高级报表功能在不同浏览器中可能会以不同方式显示。  例如，文本旋转。  
  
### <a name="scripting-requirements"></a>脚本要求

 使用启用了脚本支持的浏览器。 如果浏览器无法运行脚本，则不能查看报表。  
  
### <a name="browser-requirements-for-viewing-reports-with-the-reportviewer-web-server-controls"></a>使用 ReportViewer Web 服务器控件查看报表的浏览器要求

 对交互式报表功能的支持因浏览器类型而异。 以下支持矩阵显示在各个平台上支持的浏览器类型，所受的限制在“注释”列中列出。  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|**浏览者**|**Windows 8** 和 **Windows 8.1**|**Windows 7**|**Windows Server 2012** 和 **2012 R2**|**Windows Server 2008** 和 **2008 R2**|**Windows Server 2003**|**Mac OS X 10.6 - 10.9**|**说明**|  
|**（适用于台式机的 Internet Explorer 11**|是|是|是|不支持|不支持|不支持|Internet Explorer 支持全部 ReportViewer 功能。|  
|**Internet Explorer 10 （适用于台式机）**|是|是|是|不支持|不支持|不支持|Internet Explorer 支持全部 ReportViewer 功能。|  
|**Internet Explorer 9**|不支持|是|不支持|是|是|是|Internet Explorer 支持全部 ReportViewer 功能。|  
|**Internet Explorer 8.0**|不支持|是|不支持|是|是<sup>1</sup>|不支持|Internet Explorer 支持全部 ReportViewer 功能。 <sup>1</sup>|  
|**Internet Explorer 7.0**|不支持|是|不支持|是|是<sup>1</sup>|不支持|Internet Explorer 支持全部 ReportViewer 功能。 <sup>1</sup>|  
|**Firefox (最新公开发布的版本)**|是|是|是|是|是|不支持|不支持打印和缩放。|  
|**Safari (最新公开发布的版本)**|不支持|不支持|不支持|不支持|不支持|是|不支持打印和缩放。<br /><br /> 在此浏览器中禁用了用于在参数化报表上选择日期的日历控件。 用户必须在参数提示区域中手动键入要使用的日期。|  
|**Chrome (最新公开发布的版本)**|是|是|是|是|是|不支持|不支持打印和缩放。|  
  
 <sup>1</sup>在标准模式下，Internet Explorer 7.0 和 8.0 不显示在报表中的斜线。 如果在报表中使用斜线，请将 ASP.NET 页设置为在 Internet Explorer 怪异模式下运行。 若要执行此操作，找到\<！DOCTYPE > 在 ASP.NET 页中的标记。 如果，如果使用母板页，可以在 .master 文件中查找它。 此标记类似于以下内容：  
  
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
```
  
 替换为\<！DOCTYPE > 以下标记的标记：  
  
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">  
```
  
 在 Internet Explorer 中的兼容性模式的详细信息，请参阅[定义文档兼容性](https://go.microsoft.com/fwlink/?LinkId=180380)(https://go.microsoft.com/fwlink/?LinkId=180380)。  
  
 使用 ReportViewer 控件的详细信息，请参阅[部署报表和 ReportViewer 控件](https://msdn.microsoft.com/library/ms251723.aspx)(https://msdn.microsoft.com/library/ms251723.aspx)。  
  
## <a name="next-steps"></a>后续步骤

 [Reporting Services 工具](tools/reporting-services-tools.md)[报表管理器&#40;SSRS 本机模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md) [HTML 查看器和报表工具栏](html-viewer-and-the-report-toolbar.md) [URL 访问参数引用](url-access-parameter-reference.md)  
