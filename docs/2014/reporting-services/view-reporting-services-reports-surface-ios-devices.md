---
title: 在 Microsoft Surface 设备和 Apple iOS 设备上查看 Reporting Services 报表 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- iPad
- Safari
- SSRS
- Report Viewer [Reporting Services]
- iOS
ms.assetid: 2124bcf5-d60a-475f-a4ae-de6df44d2860
caps.latest.revision: 21
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 2766644db67f3f677060c90a2addd2123276f1e0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127469"
---
# <a name="view-reporting-services-reports-on-microsoft-surface-devices-and--apple-ios-devices"></a>在 Microsoft Surface 设备和 Apple iOS 设备上查看 Reporting Services 报表
  本文介绍 Microsoft Surface 设备和装有 Apple iOS 6 和 Apple Safari 的设备（如 iPad）支持的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能和工作流。  
  
## <a name="view-and-interact-with-reports"></a>查看报表以及与报表交互  
 从开始[!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)]，[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]在 Microsoft Surface 设备和装有 Apple iOS 6 和 Apple Safari 浏览器，如 iPad 设备上支持与报表交互查看和基本的能力。 您还可以使用 Microsoft Surface 设备发布报表。  
  
 ![IPad 桌面](media/videothumbnail.jpg "IPad 桌面")  
观看有关在 iPad 上查看报表的演示。  
  
 您还可以在 Windows Phone 8 设备上查看 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表。  
  
 为了利用在本主题中介绍的功能，请安装以下产品之一：  
  
-   对于本机模式报表服务器，安装 [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] 或更高版本。  
  
     [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] 可用于从下载[Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=35575)。  
  
-   对于 SharePoint 模式报表服务器上，安装[!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)]或更高版本的[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]用于 SharePoint 产品外接程序。  
  
 **若要查看并与其交互的 iPad 设备或 Microsoft Surface 设备上的报表**  
  
1.  确保您可以连接到报表所在的报表服务器或 SharePoint 站点。  
  
2.  通过执行下列操作之一，打开报表。  
  
    -   **从电子邮件启动：** 通过创建一封电子邮件从[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]订阅，点击报表的 URL。 该报表将在浏览器中打开。  
  
    -   **启动从报表服务器：** 上浏览目录[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报表服务器，然后点击报表名称以打开报表。  
  
    -   **从 SharePoint 文档库启动：** 浏览到 SharePoint 文档库包含[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报告，，然后点击报表名称。 您可以查看报表和与报表交互。  
  
        > [!IMPORTANT]  
        >  对于 iPad，请确保针对 Safari 的 **“专用浏览”** 属性已禁用。  
  
    -   **SharePoint web 部件：** 如果已将 web 部件添加到 SharePoint 页中，你可以查看[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报表。  
  
3.  在 Microsoft Surface 设备上，还可以使用报表管理器打开报表。 浏览目录中的[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报表管理器，，然后点击报表名称以打开报表。  
  
    > [!IMPORTANT]  
    >  iPad 不支持在报表管理器中查看报表。  
  
4.  通过执行以下操作进行滚动和缩放。  
  
    -   若要滚动显示报表，请用手指在屏幕上向上、下、左、右拖动。 这是滑动手势。  
  
    -   若要放大，请将两指置于屏幕上并分开两指。 若要缩小，请将两指置于屏幕上并合拢两指。 这是捏合手势。  
  
5.  通过执行以下操作进行报表导航和交互。  
  
    -   通过轻按加号 (+) 执行折叠操作以及轻按减号 (-) 执行展开操作，折叠和展开报表项以及与组关联的行和列。  
  
    -   通过轻按排序按钮，切换表中行或矩阵中的行列的升序和降序顺序。 排序按钮通常位于列标题中。  
  
    -   通过轻按报表顶端附近的箭头按钮，展开和折叠参数窗格。  
  
    -   通过轻按参数旁边的框或控件，选择参数值。 轻按 **“查看报表”** 将参数值应用到报表中。  
  
    -   通过轻按 **“查找”** 旁边的框，键入搜索项，然后轻按 **“查找”**，可以搜索报表内容。  
  
    -   通过轻按导航按钮或轻按这些按钮旁边的文本框并键入页码，可在报表页之间导航。  
  
    -   通过轻按添加到报表项（如文本框、图像、图表和仪表）的超链接导航到相应的 URL。  
  
    -   通过轻按 **“导出”** 下拉菜单图标，然后轻按文件格式来导出报表。  
  
        -   如果在 Microsoft Surface 设备上查看报表，则可将报表导出为下列格式之一。  
  
            -   具有报表数据的 XML 文件  
  
            -   CSV（逗号分隔）  
  
            -   PDF  
  
            -   MHTML（Web 存档）  
  
            -   “导出”  
  
            -   TIFF  
  
            -   Word  
  
        -   如果在 iPad 中查看报表，则可将报表导出为 TIFF 或 PDF 文件。  
  
## <a name="authentication"></a>身份验证  
 RSWindowsNTLM 身份验证和 RSWindowsBasic 身份验证使用[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]在纯模式和 iPad。  
  
 通常，建议不要在非 Https 环境中使用 RSWindowsBasic，因为这种类型的身份验证不为传输的凭证提供任何保密性。  
  
 有关 RSWindowsNTLM 和 RSWindowsBasic 身份验证的详细信息，请参阅[报表服务器的身份验证](security/authentication-with-the-report-server.md)。  
  
## <a name="uploading-reports"></a>上载报表  
 如果您具有适当的权限，可以使用以下方法之一从 Microsoft Surface 设备发布报表。  
  
> [!IMPORTANT]  
>  在 iPad 上不支持这些方法。  
  
-   通过打开一个 SharePoint 文档库，然后轻按 **“上载文档”**，将报表定义文件 (.rdl) 上载到该文档库。  
  
-   通过打开报表管理器，然后轻按 **“上载文件”**，将报表定义文件上载到报表服务器数据库。  
  
## <a name="additional-information"></a>其他信息  
 有关详细信息[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]和支持的浏览器，请参阅：  
  
-   [Planning for Reporting Services 和 Power View 浏览器支持&#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)  
  
 有关 Microsoft 商业智能和移动设备的详细信息，请参阅：  
  
-   [概述移动设备和 SharePoint 2013](http://technet.microsoft.com/library/fp161351\(v=office.15\).aspx) (http://technet.microsoft.com/library/fp161351(v=office.15).aspx)。  
  
-   [支持在 SharePoint 2013 中的移动设备浏览器](http://technet.microsoft.com/library/fp161353\(v=office.15\).aspx)(http://technet.microsoft.com/library/fp161353(v=office.15).aspx)。  
  
-   [在 Apple iPad 设备 (SharePoint Server 2010) 上查看报表和记分卡](http://technet.microsoft.com/library/hh697482.aspx)(http://technet.microsoft.com/library/hh697482.aspx)。  
  
-   [在 iPad （视频） 上查看 Reporting Services 报表](http://technet.microsoft.com/sqlserver/jj873792.aspx)(http://technet.microsoft.com/sqlserver/jj873792.aspx)。  
  
-   [在 Microsoft Surface RT 设备 （视频） 上查看 Reporting Services 报表](http://technet.microsoft.com/sqlserver/dn146017)  
  
  