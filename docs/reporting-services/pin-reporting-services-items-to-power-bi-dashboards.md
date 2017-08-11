---
title: "Reporting Services 将项固定到 Power BI 仪表板 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pbi
- dashboard
- pin
- powerbi
- power bi integration
ms.assetid: 1d96c3f7-2fd4-40f7-8d1c-14a7f54cdb15
caps.latest.revision: 23
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ce952f1d25529948bbcc3dbae5f1707af9683b11
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="pin-reporting-services-items-to-power-bi-dashboards"></a>将 Reporting Services 项目固定到 Power BI 仪表板
  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 使用户能够将报表查看器工具栏中的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表项作为新磁贴固定到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 仪表板。   若要固定，你的管理员需要先将报表服务器与 Azure Active Directory 和 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]相集成。  
  
 ![rs_powerbi_icon](../reporting-services/media/ssrs-powerbi-icon.png "rs_powerbi_icon")  
  
 [!INCLUDE[applies](../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 本机模式
  
##  <a name="bkmk_requirements_to_pin"></a> 固定要求  
  
-   配置报表服务器以与 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 集成。 有关详细信息，请参阅 [Power BI 报表服务器集成 (Configuration Manager)](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)相集成。 如果尚未配置报表服务器，你将在工具栏中看不到“固定到 Power BI 仪表板”按钮  。  
  
     ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
-   你可以从固定[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]t 中的报表查看器[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]他，例如`http://myserver/Reports`。  不能从 [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)]、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中的报表设计器，或从报表服务器 URL 固定。  例如`http://myserver/ReportServer`。  
  
-   你的浏览器需要配置为允许从报表服务器站点弹出窗口。  
  
-   如果你想要刷新固定项，需要针对存储的凭据配置报表。  当你固定项时，将自动创建 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 订阅，以管理固定到仪表板的项的数据刷新。  如果报表未使用存储的凭据，则当订阅运行时，你将在“我的订阅”页上看到类似于以下内容的错误消息  。  
  
        PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credential.
 
    请参阅 [在 Reporting Services 数据源中存储凭据](../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)中的“为特定于报表的数据源配置存储凭据（本机模式）”部分  
  
##  <a name="bkmk_supported_items"></a> 可以固定的项  
 以下报表项可以固定到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 仪表板。  不能固定数据区域内嵌套的项。 例如，不能固定 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 表或列表中嵌套的项。  
  
-   图表  
  
-   仪表面板  
  
-   地图  
  
-   映像  
  
-   项需要在报表正文中。  不能固定页眉或页脚中的项。  
  
-   可以固定顶级矩形内的单个项，但不能将所有项作为单个组进行固定。  
  
##  <a name="bkmk_to_pin"></a> 固定报表项  
  
1. 确认你已登录到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]中。 在[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]，选择菜单项**我的设置**并登录。 有关详细信息，请参阅  [我的 Power BI 集成（网站门户）设置](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5) 。

    ![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
2. 导航到包含报表的 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 文件夹，然后查看该报表。  
  
3. 在查看报表时，选择**固定到 Power BI**按钮工具栏。  如果你尚未登录，系统将提示你进行登录。  如果 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 按钮不可见，则报表服务器尚未与 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]集成。 有关详细信息，请参阅 [Power BI 报表服务器集成 (Configuration Manager)](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)相集成。  
  
    ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
4. 选择要固定到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]的报表项。 一次只能固定一个项。  报表查看器将显示你的报表的着色视图，可以固定的报表项将突出显示，而不能固定的项将呈现深色阴影。  
  
    **(1)** 选择包含要固定到的仪表板的组， **(2)** 选择要将项固定到的仪表板，以及 **(3)** 选择希望仪表板中的磁贴进行更新的频率。   ![请注意](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "注意")刷新由[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]订阅和固定项后，你可以编辑订阅和配置不同的刷新计划。  
  
    ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png)  
  
5. 选择**Pin**  
  
    在**Pin 成功**对话框中，您可以选择该链接**在 Power BI 中查看它**以导航到仪表板并查看只是固定的项。  
  
6. 单击“关闭”，使报表返回到普通视图。  
  
##  <a name="bkmk_in_the_dashboard"></a> 在仪表板中

将报表项固定到仪表板后，磁贴看起来与其他仪表板磁贴类似，没有可见指示标明磁贴来自 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]。 下表总结了从报表项填充磁贴属性的方式。  
  
在 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 仪表板上，固定的报表项的行为类似于其他磁贴：

**(1)** 可以将磁贴固定到其他仪表板。

**(2)**中**磁贴详细信息**你将注意到[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报表标题用于磁贴的默认标题。

**(3)** 磁贴副标题基于固定该磁贴的日期和时间或上次从 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]刷新的数据。 刷新计划由你固定报表项时自动创建的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 订阅进行管理。

**(4)** 如果单击磁贴本身， [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 将使用 **(3) 自定义链接** 导航到已注册的报表服务器的 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 页。 从 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]固定项时设置了该链接。 如果你未与报表服务器建立 Internet 连接，你将在浏览器中看到一个错误。  

![ssrs_pinned_tile_details](../reporting-services/media/ssrs-pinned-tile-details.png "ssrs_pinned_tile_details")  
  
##  <a name="bkmk-troubleshoot"></a> 解决问题  
  
-   报表查看器工具栏中**没有 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 按钮：**这指示报表服务器尚未与 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 集成。 有关详细信息，请参阅 [Power BI 报表服务器集成 (Configuration Manager)](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)相集成。  
  
- **无法固定**：当你尝试固定项时，你看到以下错误消息：请参阅 [可以固定的项](#bkmk_supported_items)部分。  
  
      Cannot Pin: There are no report items on this page that you can pin to [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  
  
-   在**仪表板中，** 固定的项显示过时的数据 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] ，它在一段时间内曾经更新过。  用户凭据令牌已过期，你需要重新登录。  向 Azure 和 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 注册的用户凭据，其有效期为 90 天。 在 t[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]他，单击**我的设置**。 有关详细信息，请参阅 [我的 Power BI 集成（网站门户）设置](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5)相集成。  
  
-   在**仪表板中** 固定的项显示过时的数据 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] ，它甚至一次也没有刷新过。  此问题在于报表未配置为使用存储的凭据。 报表必须使用存储的凭据，因为固定报表项的操作会创建 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 订阅以管理磁贴的刷新计划。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 订阅需要存储的凭据。 如果查看“我的订阅”页，你将会看到如下错误消息  ：  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image3, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credentials are not stored in the report server database, or the user data source is configured not to require credentials but the unattended execution account is not specified. (rsInvalidDataSourceCredentialSetting)
  
-   **过期的 Power BI 凭据：**  你尝试固定项，并看到以下错误消息。 在[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]，单击**我的设置**在我的设置页上，单击**登录**。 有关详细信息，请参阅  [我的 Power BI 集成（网站门户）设置](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5) 。  
  
        Cannot Pin : Unexpected Server Error: Missing, invalid or expired Power BI credentials.  
  
-   **无法固定**：如果你尝试将项固定到处于只读状态的仪表板，你将看到类似于以下内容的错误消息：  
  
        Server Error : The item 'Dashboard deleted 015cf022-8e2f-462e-88e5-75ab0a04c4d0' cannot be found. (rsItemNotFound)  
  
##  <a name="bkmk_subscription_management"></a> 订阅管理  
 除了故障排除部分所述的与订阅相关的问题外，以下信息将帮助你维护与 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 相关的订阅。
  
-   **项名称已更改：** 如果重命名或删除了固定的报表项， [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 磁贴将不再更新，并且你将看到如下错误消息。  如果将该项重命名回原始名称，则订阅将重新开始工作，磁贴将按订阅计划进行刷新。  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image1, error: Error: Report item 'Image1' cannot be found.  
  
     此外，还可以编辑订阅属性，并将“报表视觉对象名称”更改为相应的报表项名称  。 ![更改视觉对象用于 power bi 刷新](../reporting-services/media/ssrs-powerbi-subscription-visual.png "更改用于 power bi 刷新视觉对象")  
  
-   **删除磁贴**。 如果你删除中的磁贴[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]，关联的订阅不会删除在[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]并在**我的订阅**页上，你看到类似于以下错误。 你可以删除该订阅。  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image3, error: The item 'Tile deleted af7131d9-5eaf-480f-ba45-943a07d19c9f' cannot be found.  

## <a name="video"></a>视频

<iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="see-also"></a>另请参阅  
 [Power BI 报表服务器集成 (Configuration Manager)](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [我的 Power BI 集成（网站门户）设置](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5)  
 [Power BI 中的仪表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]


