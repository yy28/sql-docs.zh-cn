---
title: 查看 Microsoft Surface 设备和 Apple iOS 设备上的 Reporting Services 报告 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- iPad
- Safari
- SSRS
- Report Viewer [Reporting Services]
- iOS
ms.assetid: 2124bcf5-d60a-475f-a4ae-de6df44d2860
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a3937f227d025da054a28f73fffde4a57dc365c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66098661"
---
# <a name="view-reporting-services-reports-on-microsoft-surface-devices-and--apple-ios-devices"></a>在 Microsoft Surface 设备和 Apple iOS 设备上查看 Reporting Services 报表
  本文介绍 Microsoft Surface 设备和装有 Apple iOS 6 和 Apple Safari 的设备（如 iPad）支持的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能和工作流。  
  
## <a name="view-and-interact-with-reports"></a>查看报表以及与报表交互  
 从 [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)]开始， [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持在 Microsoft Surface 设备和装有 Apple iOS 6 和 Apple Safari 浏览器的设备（如 iPad）上查看报表以及与这些报表执行基本的交互操作。 您还可以使用 Microsoft Surface 设备发布报表。  
  
 ![IPad 桌面](media/videothumbnail.jpg "IPad 桌面")  
观看有关在 iPad 上查看报表的演示。  
  
 您还可以在 Windows Phone 8 设备上查看 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表。  
  
 为了利用在本主题中介绍的功能，请安装以下产品之一：  
  
-   对于本机模式报表服务器，安装 [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] 或更高版本。  
  
     [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)]可从[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=35575)下载。  
  
-   对于 SharePoint 模式报表服务器，请安装适用于 SharePoint 产品的 [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] 外接程序的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 或更高版本。  
  
 **若要在 iPad 设备或 Microsoft Surface 设备上查看报表并与之交互**  
  
1.  确保您可以连接到报表所在的报表服务器或 SharePoint 站点。  
  
2.  通过执行下列操作之一，打开报表。  
  
    -   **从电子邮件启动：** 从[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]订阅创建的电子邮件中，点击报表的 URL。 该报表将在浏览器中打开。  
  
    -   **从报表服务器启动：** 浏览[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Report Server 上的目录，然后点击报表名称以打开报表。  
  
    -   **从 SharePoint 文档库开始：** 浏览到包含[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报表的 SharePoint 文档库，然后点击报表名称。 您可以查看报表和与报表交互。  
  
        > [!IMPORTANT]  
        >  对于 iPad，请确保针对 Safari 的 **“专用浏览”** 属性已禁用。  
  
    -   **SharePoint web 部件：** 如果 web 部件已添加到 SharePoint 页，则可以查看[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报表。  
  
3.  在 Microsoft Surface 设备上，还可以使用报表管理器打开报表。 浏览 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器中的目录，然后轻按报表名称以打开该报表。  
  
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
  
        -   如果要在 Microsoft Surface 设备上查看报表，可以将报表导出为以下格式之一。  
  
            -   具有报表数据的 XML 文件  
  
            -   CSV（逗号分隔）  
  
            -   PDF  
  
            -   MHTML（Web 存档）  
  
            -   Excel  
  
            -   TIFF  
  
            -   Word  
  
        -   如果要在 iPad 上查看报表，可以将报表导出为 TIFF 或 PDF 文件。  
  
## <a name="authentication"></a>Authentication  
 RSWindowsNTLM 身份验证和 RSWindowsBasic 身份验证可用于本机模式下的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 或 iPad。  
  
 通常，建议不要在非 Https 环境中使用 RSWindowsBasic，因为这种类型的身份验证不为传输的凭证提供任何保密性。  
  
 有关 RSWindowsNTLM 和 RSWindowsBasic 身份验证的详细信息，请参阅 [Authentication with the Report Server](security/authentication-with-the-report-server.md)。  
  
## <a name="uploading-reports"></a>上载报表  
 如果您具有适当的权限，可以使用以下方法之一从 Microsoft Surface 设备发布报表。  
  
> [!IMPORTANT]  
>  在 iPad 上不支持这些方法。  
  
-   通过打开一个 SharePoint 文档库，然后轻按 **“上载文档”**，将报表定义文件 (.rdl) 上载到该文档库。  
  
-   通过打开报表管理器，然后轻按 **“上载文件”**，将报表定义文件上载到报表服务器数据库。  
  
## <a name="additional-information"></a>其他信息  
 有关 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 和支持的浏览器的详细信息，请参阅：  
  
-   [规划 Reporting Services 和 Power View 浏览器支持 &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)  
  
 有关 Microsoft 商业智能和移动设备的详细信息，请参阅：  
  
-   [移动设备和 SharePoint 2013](https://technet.microsoft.com/library/fp161351\(v=office.15\).aspx) （https://technet.microsoft.com/library/fp161351(v=office.15).aspx)。  
  
-   SharePoint 2013 （https://technet.microsoft.com/library/fp161353(v=office.15).aspx)）[中支持的移动设备浏览器](https://technet.microsoft.com/library/fp161353\(v=office.15\).aspx)。  
  
-   [在 Apple iPad 设备上查看报表和记分卡（SharePoint Server 2010）](https://technet.microsoft.com/library/hh697482.aspx) （https://technet.microsoft.com/library/hh697482.aspx)。  
  
-   [在 iPad 上查看 Reporting Services 报表（视频）](https://technet.microsoft.com/sqlserver/jj873792.aspx) （https://technet.microsoft.com/sqlserver/jj873792.aspx)。  
  
-   [在 Microsoft Surface RT 设备上查看 Reporting Services 报表（视频）](https://technet.microsoft.com/sqlserver/dn146017)  
  
  
