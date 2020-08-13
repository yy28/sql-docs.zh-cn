---
title: HTML 查看器和报表工具栏 | Microsoft Docs
description: 了解 HTML 查看器和报表工具栏，以及如何在报表服务器请求报表时按需查看报表。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- HTML Viewer [Reporting Services]
- report toolbar [Reporting Services]
ms.assetid: cd86b319-babd-45af-a6a4-f659fdcc40c3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 825e169f3819cc19b042715662f4ec554f02d65b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247196"
---
# <a name="html-viewer-and-the-report-toolbar"></a>HTML 查看器和报表工具栏
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供了一个 HTML 查看器，该查看器可用来按需显示从报表服务器请求的报表。 HTML 查看器提供了一个用于以 HTML 格式查看报表的框架。 该查看器包含报表工具栏、参数区域、凭据区域和文档结构图。 HTML 查看器中的报表工具栏包含可用于处理报表的功能（包括导出选项，以便您可以使用 HTML 之外的格式查看报表）。 只有在打开配置为使用参数和文档结构图控件的报表时，才会显示参数区域和文档结构图。  
  
 尽管您不能修改报表工具栏，但是可以配置报表 URL 的参数以在报表中隐藏工具栏。 有关隐藏报表工具栏的详细信息，请参阅 [URL 访问参数引用](../reporting-services/url-access-parameter-reference.md)。  
  
## <a name="report-toolbar"></a>报表工具栏  
 报表工具栏为 HTML 呈现扩展插件中所呈现的报表提供了页面导航、缩放、刷新、搜索、导出、打印和数据馈送功能。  
  
 打印功能是可选的。 如果启用了打印功能，报表工具栏上将显示一个打印机图标。 在首次使用时，单击该打印机图标将下载必须安装的 ActiveX 控件。 在安装该控件后，单击打印机图标将打开“打印”对话框，以便从计算机所配置的打印机中进行选择。 是否可以打印取决于服务器设置和浏览器设置。 有关详细信息，请参阅[使用打印控件从浏览器中打印报表（报表生成器和 SSRS）](../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)和[启用和禁用 Reporting Services 的客户端打印](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  
  
 报表工具栏与下图中所显示的报表工具栏类似。 根据报表功能或可用的呈现选项的不同，您看到的报表工具栏可能会与该图有所不同。  
  
 ![报表工具栏](../reporting-services/media/ssrs-htmlviewer-toolbar.png "报表工具栏")  
  
 下表对报表工具栏的常用功能进行了说明： 每个功能都由您访问该功能时所使用的控件标识。  
  
|图标或控件||目标|  
|------------------------------|-|--------|  
|![页面导航控件](../reporting-services/media/htmlviewer-pagenav.gif "页面导航控件")|**页面导航控件**|打开报表的第一页或最后一页，逐页浏览报表，以及打开报表中的特定页面。 若要查看特定页面，请键入相应的页码，再按 Enter。|  
|![页面显示控件](../reporting-services/media/htmlviewer-pagesize.gif "页面显示控件")|**页面显示控件**|放大或缩小报表页的大小。 除了按比例更改外，还可以选择“页宽”，以使报表页的水平宽度适应浏览器窗口大小，或选择“整页”，以使报表的垂直高度适应浏览器窗口大小********。 **Internet Explorer 5.5 和更高版本支持** “缩放” [!INCLUDE[msCoName](../includes/msconame-md.md)] 选项。|  
|![搜索字段](../reporting-services/media/htmlviewer-search.gif "搜索字段")|**搜索字段**|通过键入要查找的单词或短语（最长不超过 256 个字符）在报表中搜索内容。 搜索不区分大小写，将从当前选择的页或区域开始。 搜索操作中只包括可见内容。 若要搜索随后出现的相同值，请单击 **“下一个”** 。|  
|![导出格式](../reporting-services/media/htmlviewer-export.GIF "导出格式")|**导出格式**|打开一个新的浏览器窗口，并以所选的格式呈现报表。 可用的格式由报表服务器上安装的呈现扩展插件决定。 建议打印时采用 TIFF 格式。 单击 **“导出”** 可以按所选格式查看报表。|  
|![文档结构图图标](../reporting-services/media/htmlviewer-docmap.GIF "文档结构图图标")|**文档结构图图标**|在包含文档结构图的报表中显示或隐藏文档结构图窗格。 文档结构图是一个类似于网站上的导航窗格的报表导航控件。 单击文档结构图中的项，即可导航到特定的组、页或子报表。|  
|![打印机图标](../reporting-services/media/printer-icon.gif "打印机图标")|**打印机图标**|打开“打印”对话框，以便指定打印选项并打印报表。 在首次使用时，单击此图标后将提示您下载打印控件。|  
||**显示图标和隐藏图标**|在包含参数的报表中显示或隐藏参数值字段及 **“查看报表”** 按钮。|  
|![报表工具栏上的浏览器刷新按钮](../reporting-services/media/htmlviewer-refresh.GIF "报表工具栏上的浏览器刷新按钮")|**报表刷新图标**|刷新报表。 实时报表的数据将相应刷新。 缓存报表将从其存储位置重新加载。|  
|![htmlviewer_datafeed](../reporting-services/media/htmlviewer-datafeed.gif "htmlviewer_datafeed")|**数据馈送图标**|基于报表生成了数据馈送。|  
|![ssrs_powerbi_button_reportwviewer](../reporting-services/media/ssrs-powerbi-button-reportwviewer.png "ssrs_powerbi_button_reportwviewer")|**固定到 Power BI 仪表板**|将支持报表项固定到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]。 如果按钮不可见，则报表服务器尚未与 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]集成。  有关详细信息，请参阅 [Power BI 报表服务器集成 (Configuration Manager)](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)相集成。|  
  
### <a name="about-export-formats"></a>关于导出格式  
 从报表工具栏中，可以选择以不同格式查看报表。 可用的格式由报表服务器上安装的呈现扩展插件决定。 如果您选择另一种格式，将使用与您所选的导出格式关联的查看器通过另一个浏览器窗口显示报表。 如果您所选的格式没有适用的查看器，可以选择其他格式。  
  
 采用默认选项安装的报表服务器中包含以下导出格式。 可供您使用的导出格式的列表可能会与下面的列表有些出入。  
  
|导出格式|说明|  
|-------------------|-----------------|  
|XML|以 XML 语法格式查看报表。 以 XML 格式查看的报表将在一个新浏览器窗口中打开。|  
|CSV|以逗号分隔格式查看报表。 报表将在与 CSV 文件类型相关联的应用程序中打开。|  
|PDF|使用客户端 PDF 查看器查看报表。 您必须具有第三方 PDF 查看器（例如，Adobe Acrobat Reader），才可使用此格式。|  
|MHTML|以 MIME 编码的 HTML 格式查看报表，该格式可将图像和链接内容与报表一起保存。|  
|Excel|在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel（.xlsx 文件）中查看报表。|  
|PowerPoint|在 [!INCLUDE[msCoName](../includes/msconame-md.md)] PowerPoint（.pptx 文件）中查看报表。|  
|TIFF 文件|在默认的 TIFF 查看器中查看报表。 对于某些 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 客户端，查看器为 Windows 图片与传真查看器。 选择此格式可以按面向页面的布局查看报表。|  
|Word|在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Word（.docx 文件）中查看报表。|  
  
## <a name="parameters"></a>参数  
 参数是用于选择特定数据的值（具体来说，参数用于完成为报表选择数据的查询或用于筛选结果集）。 报表中常用的参数包括日期、名称和 ID。 在为某个参数指定了值后，报表中将只包含与该值匹配的数据；例如，将根据 Employee ID 参数来显示雇员数据。 参数与报表上的字段相互对应。 指定了参数之后，单击 **“查看报表”** 即可获取相应的数据。  
  
 报表作者可定义对于每个报表都有效的参数值。 报表管理员也可以设置参数值。 若要了解哪些参数值对于您的报表有效，请咨询报表设计者或管理员。  
  
## <a name="credentials"></a>凭据  
 凭据是用于授予数据源访问权限的用户名和密码的值。 指定了凭据之后，单击 **“查看报表”** 即可获取相应的数据。 如果报表要求您登录，那么您有权查看的数据可能与其他用户所看到的数据不同。 因此，两位用户可以运行同一个报表，而获得不同的结果。 另外，某些报表还包含隐藏区域，这些区域将根据用户登录凭据或用户在报表中所做的选择而进行显示。 报表中的隐藏区域不在搜索操作的范围内，因此进行搜索时会生成与报表全部可见时不同的搜索结果。  
  
## <a name="see-also"></a>另请参阅  
 [为报表数据源指定凭据和连接信息](../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [查找、查看和管理报表（报表生成器和 SSRS）](../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [导出报表（报表生成器和 SSRS）](../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
