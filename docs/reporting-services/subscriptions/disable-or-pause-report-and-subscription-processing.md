---
title: 禁用或暂停报表和订阅处理 | Microsoft Docs
ms.custom: ''
ms.date: 09/29/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: subscriptions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 47
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: dfddb0368d8c674c7f0148a395f97088d9143228
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>禁用或暂停报表和订阅处理
  可采用多种方法禁用或暂停 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表和订阅处理。 本主题中的方法从禁用订阅延伸到中断数据源连接。 并非所有方法在两种 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务器模式下都可行。下表概述了各种方法以及支持的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务器模式：  
  
##  <a name="bkmk_top"></a> 本主题内容  
  
||支持的服务器模式|  
|-|---------------------------|  
|[启用和禁用订阅](#bkmk_disable_subscription)|本机模式|  
|[暂停共享计划](#bkmk_pause_schedule)|本机模式和 SharePoint 模式|  
|[禁用共享数据源](#bkmk_disable_shared_datasource)|本机模式和 SharePoint 模式|  
|[通过修改角色分配来阻止访问报表（本机模式）](#bkmk_modify_role_assignment)|本机模式|  
|[从角色中删除管理订阅权限（本机模式）](#bkmk_remove_manage_subscriptions_permission)|本机模式|  
|[禁用传递扩展插件](#bkmk_disable_extensions)|本机模式和 SharePoint 模式|  
  
##  <a name="bkmk_disable_subscription"></a> 启用和禁用订阅  
  
> [!TIP]  
>  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]中的新增功能！ **启用和禁用订阅**。 新用户界面选项允许你快速禁用和启用订阅。 已禁用的订阅将维持自身的其他配置属性（例如计划），并且可以轻松地启用。 你也可以通过编程方式启用和禁用订阅或者审核哪些订阅已禁用。  
  
 ![报表服务订阅功能区](../../reporting-services/subscriptions/media/ssrs-subscription-ribbon.png "报表服务订阅功能区")  
  
 在本机模式报表管理器中，从“我的订阅”  页或单个订阅的“管理”  页浏览到订阅。 在功能区中选择一个或多个订阅，然后单击“禁用”按钮 ![禁用报表服务订阅](../../reporting-services/subscriptions/media/ssrs-disable-subscription.png "禁用报表服务订阅") 或“启用”按钮 ![启用报表服务订阅](../../reporting-services/subscriptions/media/ssrs-enable-subscription.png "启用报表服务订阅")。 禁用的订阅标记有警告图标 ![报表服务订阅的状态警告](../../reporting-services/subscriptions/media/ssrs-subscription-warning.png "报表服务订阅的状态警告")，且状态被列为“已禁用”。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 会在禁用订阅时在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 日志中写入一行，在启用订阅时另外写入一行。 例如，在报表服务器日志文件中：  
  
 `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__10_16_2014_00_02_18.log`  
  
 你将看到如下行：  
  
 `library!ReportServer_0-1!b08!10/16/2014-16:21:14:: i INFO: Call to DisableSubscriptionAction(SubscriptionID=e843bc2b-023e-45a3-ba23-22f9dc9a0934)`  
  
 `library!ReportServer_0-1!2eec!10/16/2014-16:44:18:: i INFO: Call to EnableSubscriptionAction(SubscriptionID=e843bc2b-023e-45a3-ba23-22f9dc9a0934).`  
  
 ![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell related content") 使用 Windows PowerShell 禁用单个订阅：使用以下 PowerShell 脚本禁用特定订阅。 更新服务器名称和订阅 ID。  
  
```  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid”;  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 可以使用以下脚本列出所有订阅及其 ID。 更新服务器名称。  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell related content") 使用 Windows PowerShell 列出所有已禁用的订阅：使用以下 PowerShell 脚本列出当前本机模式报表服务器上所有已禁用的订阅。 更新服务器名称。  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell related content") 使用 Windows PowerShell 启用所有已禁用的订阅：使用以下 PowerShell 脚本启用当前已禁用的所有订阅。 更新服务器名称。  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell related content") 使用 Windows PowerShell 禁用所有订阅：使用以下 PowerShell 脚本禁用所有订阅。  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="bkmk_pause_schedule"></a> 暂停共享计划  
 如果报表或订阅按照某个共享计划运行，您可以通过暂停该计划来阻止这些报表或订阅的处理。 在恢复计划之前，会延迟由该计划驱动的所有报表和订阅处理。  
  
-   SharePoint 模式：在“站点设置” ![SharePoint 设置](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置") 中，选择“管理共享计划”。 选择计划，并单击“暂停所选计划” 。  
  
-   **本机模式：** 在报表管理器中，单击“站点设置” 。 选择计划，然后单击“暂停” 。  
  
##  <a name="bkmk_disable_shared_datasource"></a> 禁用共享数据源  
 使用共享数据源的一个优点是您可以通过禁用它来阻止报表或数据驱动订阅运行。 禁用共享数据源会断开报表与其外部源的连接。 禁用共享数据源后，所有原来使用该数据源的报表和订阅将无法再继续访问该数据源。  
  
 请注意，即使数据源不可用，你也仍可加载相应的报表。 该报表不包含任何数据，但具有适当权限的用户可以访问与该报表关联的属性页、安全设置、报表历史记录和订阅信息。  
  
-   **SharePoint 模式：** 若要在 SharePoint 模式报表服务器中禁用共享数据源，请浏览到包含该数据源的文档库。 ![共享数据源图标](../../reporting-services/report-data/media/hlp-16datasource.png "Shared data source icon") 单击数据源，然后清除“启用此数据源”复选框。  
  
-   **本机模式：** 若要在本机模式报表服务器中禁用共享数据源，请在报表管理器中打开相应的数据源，再清除“启用此数据源”  复选框。  
  
##  <a name="bkmk_modify_role_assignment"></a> 通过修改角色分配来阻止访问报表（本机模式）  
 使报表不可用的方法之一是，暂时删除提供报表访问权限的角色分配。 无论采用哪种数据源连接，对所有报表都可以使用这种方法。 这种方法只针对目标报表，不会影响其他报表或项的操作。  
  
 若要删除角色分配，请在报表管理器中打开报表的“安全属性”页。 如果报表的安全设置是从父报表继承来的，则可以单击“编辑项安全设置”，创建一个忽略提供大范围访问权的角色分配的限制性安全策略。例如，可以删除为 Everyone 提供访问权的角色分配，而保留为一组少量用户（如 Administrators）提供访问权的角色分配。  
  
##  <a name="bkmk_remove_manage_subscriptions_permission"></a> 从角色中删除管理订阅权限（本机模式）  
 若要阻止用户创建订阅，请从角色中清除“管理单独的订阅”  任务。 删除此任务后，“订阅”页将不可用。 在报表管理器中，“我的订阅”页显示为空（不能将它删除），即便它以前包含订阅也是如此。 删除与订阅相关的任务会使用户无法创建和修改订阅，但这不会删除现有的订阅。 现有订阅将继续执行，直到被删除。 若要删除权限，请执行以下操作：  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 图标  
  
2.  连接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器。  
  
3.  展开“安全性”  节点。  
  
4.  选择角色并清除“管理单独的订阅”  任务。  
  
##  <a name="bkmk_disable_extensions"></a> 禁用传递扩展插件  
 对于有权创建对某个给定报表的订阅的任何用户，可以使用报表服务器上安装的所有传递扩展插件。 可以自动使用并配置下列传递扩展插件：  
  
-   Windows 文件共享  
  
-   SharePoint 库（只能从 SharePoint 站点使用，该站点与 SharePoint 集成模式报表服务器集成在一起）  
  
 电子邮件传递必须进行配置才能使用。 如果未对它进行配置，它将不可用。 有关详细信息，请参阅 [为电子邮件传递配置报表服务器 (SSRS Configuration Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)。  
  
 如果要关闭特定的扩展插件，可以在 **RSReportServer.config** 文件中删除与该扩展插件相对应的条目。 有关详细信息，请参阅 [Reporting Services 配置文件](../../reporting-services/report-server/reporting-services-configuration-files.md) 和 [为电子邮件传递配置报表服务器 (SSRS Configuration Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)。  
  
 删除某个传递扩展插件后，该插件在报表管理器或 SharePoint 站点中将不再可用。 删除传递扩展插件可能会使订阅变为非活动状态。 在删除扩展插件之前，请确保删除这些订阅或者将它们配置为使用其他传递扩展插件。  
  
## <a name="see-also"></a>另请参阅  
 [订阅和传递 (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Reporting Services 配置文件](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [配置报表管理器（本机模式）](../../reporting-services/report-server/configure-report-manager-native-mode.md)   
 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [项的“安全性”属性页（报表管理器）](http://msdn.microsoft.com/library/351b8503-354f-4b1b-a7ac-f1245d978da0)  
  
  
