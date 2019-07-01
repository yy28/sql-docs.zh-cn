---
title: 禁用或暂停报表和订阅处理 | Microsoft Docs
ms.date: 06/19/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bfebb45330ef9775a3e707ad244122654a1f582e
ms.sourcegitcommit: 3f2936e727cf8e63f38e5f77b33442993ee99890
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2019
ms.locfileid: "67313996"
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>禁用或暂停报表和订阅处理  
可采用多种方法禁用或暂停 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表和订阅处理。 本主题中的方法从禁用订阅到中断数据源连接，无所不包。 并非所有的方法有两个[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服务器模式。 下表概述方法和支持[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服务器模式：  
  
##  <a name="bkmk_top"></a> 本文内容  
  
||支持的服务器模式|  
|-|---------------------------|  
|[启用和禁用订阅](#bkmk_disable_subscription)|本机模式|  
|[暂停共享计划](#bkmk_pause_schedule)|本机模式和 SharePoint 模式|  
|[禁用共享数据源](#bkmk_disable_shared_datasource)|本机模式和 SharePoint 模式|  
|[通过修改角色分配来阻止访问报表（本机模式）](#bkmk_modify_role_assignment)|本机模式|  
|[从角色中删除管理订阅权限（本机模式）](#bkmk_remove_manage_subscriptions_permission)|本机模式|  
|[禁用传递扩展插件](#bkmk_disable_extensions)|本机模式和 SharePoint 模式|  
  
##  <a name="bkmk_disable_subscription"></a>启用和禁用订阅  
  
>[!TIP]  
>SQL 2016 Reporting Services 中中的新增功能*启用和禁用订阅*。 使用新用户界面选项，可以快速启用和禁用订阅。 已禁用的订阅可以维护自身的其他配置属性（如计划），并能轻松地重新启用。 也可以编程方式启用和禁用订阅，或审核哪些订阅已遭禁用。  
  
  ![订阅页的启用和禁用按钮 ](../../reporting-services/subscriptions/media/disable-or-pause-report-and-subscription-processing/subscription-enable-and-disable-buttons.png)  
  
在 web 门户中，浏览到订阅眖**我的订阅**页或**订阅**单个订阅的页。 选择一个或多个订阅，再单击功能区中的禁用按钮或启用按钮（见上图）。 状态列将分别更改为"已禁用"或"Enabled"。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在中写入一行[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]登录时启用或禁用订阅。 例如，在报表服务器日志文件中：  
  
 `C:\Program Files\Microsoft SQL Server Reporting Services\SSRS\LogFiles\RSPortal_2019_06_20_00_49_22.log`  
  
 你将看到如下行：  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:47:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca disabled at 06/20/2019 01:16:47`  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:51:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca enabled at 06/20/2019 01:16:51`  
  
![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相关内容")：使用 Windows PowerShell 禁用单个订阅  ：使用以下 PowerShell 脚本禁用特定订阅。 更新脚本中的服务器名称和订阅 ID。  
  
```PS  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid";  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 可以使用以下脚本列出所有订阅及其 ID。 更新服务器名称。  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell related content")  使用 Windows PowerShell 列出所有已禁用的订阅：使用以下 PowerShell 脚本列出当前本机模式报表服务器上所有已禁用的订阅。 更新服务器名称。  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell related content")  使用 Windows PowerShell 启用所有已禁用的订阅：使用以下 PowerShell 脚本启用当前已禁用的所有订阅。 更新服务器名称。  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell related content")  使用 Windows PowerShell 禁用所有订阅：使用以下 PowerShell 脚本禁用所有订阅  。  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="bkmk_pause_schedule"></a> 暂停共享计划  
 如果报表或订阅按照某个共享计划运行，您可以通过暂停该计划来阻止这些报表或订阅的处理。 在恢复计划之前，会延迟由该计划驱动的所有报表和订阅处理。  
  
-   SharePoint 模式：在“站点设置” ![SharePoint 设置](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置") 中，选择“管理共享计划”    。 选择计划，并单击“暂停所选计划”  。  
  
-   **本机模式：** 在 web 门户中，选择**设置**按钮![设置按钮](media/ssrs-portal-settings-gear.png)从 web 门户的屏幕，然后选择顶部菜单栏**站点设置**从下拉列表菜单。 选择**计划**选项卡以显示计划页。 选择你想要启用或禁用，并选择的计划旁边的复选框**启用**或**禁用**按钮分别执行所需的操作。 状态列会相应地更新为"已禁用"或"Enabled"。  
  
##  <a name="bkmk_disable_shared_datasource"></a> 禁用共享数据源  
 使用共享数据源的一个优点是您可以通过禁用它来阻止报表或数据驱动订阅运行。 禁用共享数据源会断开报表与其外部源的连接。 禁用共享数据源后，所有原来使用该数据源的报表和订阅将无法再继续访问该数据源。  
  
 请注意，即使数据源不可用，你也仍可加载相应的报表。 该报表不包含任何数据，但具有适当权限的用户可以访问与该报表关联的属性页、安全设置、报表历史记录和订阅信息。  
  
-   **SharePoint 模式：** 若要在 SharePoint 模式报表服务器中禁用共享数据源，请浏览到包含该数据源的文档库。 ![共享数据源图标](../../reporting-services/report-data/media/hlp-16datasource.png "Shared data source icon") 单击数据源，然后清除“启用此数据源”复选框  。  
  
-   **本机模式：** 若要在本机模式报表服务器中禁用共享数据源，请在 Web 门户中打开相应数据源，再取消选中“启用此数据源”  复选框。  
  
##  <a name="bkmk_modify_role_assignment"></a> 通过修改角色分配来阻止访问报表（本机模式）  
使报表不可用的方法之一是，暂时删除提供报表访问权限的角色分配。 无论采用哪种数据源连接，对所有报表都可以使用这种方法。 这种方法只针对目标报表，不会影响其他报表或项的操作。  
  
 若要删除角色分配，请打开**安全**web 门户中报表的页。 如果报表的安全设置是从父报表继承而来，你可以依次选择“自定义安全设置”  和“项安全性”  对话框中的“确认”  ，以创建忽略提供广泛访问权限的角色分配的限制性安全策略（例如，可以删除为每个人提供访问权限的角色分配，而保留为一小部分用户（如管理员）提供访问权限的角色分配）。  
  
##  <a name="bkmk_remove_manage_subscriptions_permission"></a> 从角色中删除管理订阅权限（本机模式）  
 若要阻止用户创建订阅，请从角色中清除“管理单独的订阅”  任务。 删除此任务后，“订阅”页将不可用。 在 Web 门户中，“我的订阅”页显示为空（无法删除它），即使它以前包含订阅，也不例外。 删除与订阅相关的任务会使用户无法创建和修改订阅，但这不会删除现有的订阅。 现有订阅将继续执行，直到你删除它们。 若要删除权限，请执行以下操作：  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 
  
2.  连接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器。  
  
3.  展开“安全性”  节点。  
  
4.  展开**角色**节点，然后选择所需的角色。  
  
5.  右键单击相应角色，并选择“属性”  。  
  
6.  清除**管理单独的订阅**并**管理所有订阅**任务。  
  
7.  单击“确定”  ，以应用更改。

  
##  <a name="bkmk_disable_extensions"></a> 禁用传递扩展插件  
 对于有权创建对某个给定报表的订阅的任何用户，可以使用报表服务器上安装的所有传递扩展插件。 可以自动使用并配置下列传递扩展插件：  
  
-   Windows 文件共享  
  
-   SharePoint 库（只能从 SharePoint 站点使用，该站点与 SharePoint 集成模式报表服务器集成在一起）  
  
 电子邮件传递必须进行配置才能使用。 如果未对它进行配置，它将不可用。 有关详细信息，请参阅[电子邮件设置-Reporting Services 本机模式 （配置管理器）](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)。  
  
 如果要关闭特定的扩展插件，可以在 **RSReportServer.config** 文件中删除与该扩展插件相对应的条目。 有关详细信息，请参阅[Reporting Services Configuration Files](../../reporting-services/report-server/reporting-services-configuration-files.md)并[电子邮件设置-Reporting Services 本机模式 （配置管理器）](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)。  
  
 删除的传递扩展插件在 Web 门户或 SharePoint 站点中不再可用。 删除传递扩展插件可能会使订阅变为非活动状态。 在删除扩展插件之前，请确保删除这些订阅或者将它们配置为使用其他传递扩展插件。  
  
## <a name="see-also"></a>另请参阅  
 [订阅和传递 (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Reporting Services 配置文件](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [配置 Web 门户](../../reporting-services/report-server/configure-web-portal.md)   
 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [报表服务器的 Web 门户（SSRS 本机模式）](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [安全对象](../../reporting-services/security/securable-items.md) 
  
