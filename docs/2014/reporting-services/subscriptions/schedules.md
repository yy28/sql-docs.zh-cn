---
title: 计划 | Microsoft Docs
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
- schedules [Reporting Services]
- schedules [Reporting Services], about schedules
- published reports [Reporting Services], schedules
- reports [Reporting Services], scheduling
- subscriptions [Reporting Services], scheduling
- automatic report processing
ms.assetid: ecccd16b-eba9-4e95-b55d-f15c621e003f
caps.latest.revision: 50
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 800dce34cebf45e3962b5226929267afe1fc727f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125064"
---
# <a name="schedules"></a>“计划”
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了共享的计划和报表特定计划，以帮助你控制处理和分发报表。 这两种计划类型之间的区别在于对它们进行定义、存储和管理的方式。 这两种类型的计划的内部构造是相同的。 所有计划都指定一种重复执行类型：每月、每周或每日。 在重复执行类型中，您将为事件发生的频率设置间隔和范围。 无论您创建的是共享计划还是报表特定计划，重复执行模式的类型以及指定那些模式的方式是相同的。  
  
 本主题内容：  
  
-   [你可以使用日程安排做什么](#bkmk_whatyoucando)  
  
-   [比较共享和报表特定计划](#bkmk_compare)  
  
-   [配置数据源](#bkmk_configuredatasources)  
  
-   [将凭据存储和处理帐户](#bkmk_credentials)  
  
-   [如何计划和传递处理的工作方式](#bkmk_how_scheduling_works)  
  
-   [服务器依赖项](#bkmk_serverdependencies)  
  
-   [停止 SQL Server 代理的影响](#bkmk_stoppingagent)  
  
-   [停止报表服务器服务的影响](#bkmk_stoppingservice)  
  
  
##  <a name="bkmk_whatyoucando"></a> 可对计划执行的操作  
 可以使用本机模式下的报表管理器或 SharePoint 模式下的 SharePoint 站点管理页来创建和管理计划。 您可以：  
  
-   计划标准订阅或数据驱动订阅中的报表传递时间。  
  
-   计划报表历史记录，以便按固定的时间间隔向报表历史记录中添加新的快照。  
  
-   计划刷新报表快照数据的时间。  
  
-   计划刷新共享数据集的数据的时间。  
  
-   将缓存报表或共享数据集的过期时间计划在预定义时间，之后就可以刷新该报表。  
  
 如果希望将计划信息用于多个报表或订阅，则可以创建共享计划。 共享计划是单独定义的，然后就可以在需要计划信息的报表、共享数据集和订阅中引用。  
  
 创建计划时，报表会将计划信息保存在报表服务器的数据库中，或者对于 SharePoint 模式，保存在服务应用程序数据库中。 报表服务器还会创建用于触发计划的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。 计划是基于其所在报表服务器的本地时间进行处理的。 其时间格式遵从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 操作系统标准。  
  
 有关如何创建和管理计划的详细信息，请参阅[Create，Modify，and Delete Schedules](create-modify-and-delete-schedules.md)。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供计划操作。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2012 各个版本支持的功能](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473)。  
  
##  <a name="bkmk_compare"></a> 共享计划和报表特定计划的区别  
 两种类型的计划将产生相同的输出：  
  
-   **共享计划** 是可移植的多用途项，包含有现成的计划信息。 由于共享计划是系统级的项，因此创建共享计划需要具有系统级权限。 由于这个原因，您的报表服务器上的可用共享计划通常都是由报表服务器管理员或内容管理员创建的。 共享计划是使用报表管理器或 SharePoint 站点设置在报表服务器上存储和管理的。  
  
     与通过报表属性、共享数据集属性或订阅属性定义的特定计划相比，共享计划更易于管理和维护，具体原因如下：  
  
    -   可以从一个中央位置管理共享计划，如果各个计划操作的运行间隔很短或者与服务器上的其他进程相冲突，这便于比较计划属性以及调整频率和重复执行模式。  
  
    -   使您可以快速适应计算环境的更改。 例如，假定在刷新数据仓库之后有一组在早晨 4:00 运行的 报表。 如果重新计划或延迟了数据刷新操作，则通过更新单个共享计划中的计划信息可以轻易地适应该更改。  
  
    -   如果仅使用共享计划，则可以清楚地知道执行计划操作的时间。 这便于在发生性能问题之前预计和调整服务器负载。 例如，如果决定在特定时间进行计算机备份，则可以调整共享计划在不同的时间运行。  
  
-   **报表特定计划** 在特定的报表、订阅或报表执行操作的上下文中定义，用于确定缓存过期或快照更新的时间。 当您定义订阅或设置报表执行属性时，同时也会创建这些计划。 如果共享计划不能提供所需的频率或重复执行模式，则可以创建报表特定计划。 若要禁止报表运行，必须手动编辑报表特定计划。 报表特定计划可以由各个用户创建。  
  
##  <a name="bkmk_configuredatasources"></a> 配置数据源  
 必须先将报表数据源配置为使用存储的凭据或无人参与的报表处理帐户，才能计划报表的数据或订阅处理。 如果使用存储的凭据，则只能存储一组凭据，运行该报表的所有用户都将使用这组凭据。 凭据可以是 Windows 用户帐户，也可以是数据库用户帐户。  
  
 无人参与的报表处理帐户是在报表服务器上配置的特殊用途的帐户。 当计划操作需要检索外部文件或处理时，报表服务器可以使用该帐户连接到远程计算机。 如果配置该帐户，则可以使用它连接到向报表提供数据的外部数据源。  
  
 若要指定存储的凭据或无人参与的报表处理帐户，请编辑该报表的数据源属性。 如果报表使用共享数据源，则改为编辑共享数据源。  
  
##  <a name="bkmk_credentials"></a> 存储凭据和处理帐户  
 您对计划的处理权限取决于您的角色分配中的任务。 如果使用预定义角色，则作为“内容管理员”和“系统管理员”的用户可以创建和管理任何计划。 如果您使用自定义角色分配，角色分配必须包括支持计划操作的任务。  
  
|执行的操作|包括此任务|本机模式预定义角色|SharePoint 模式组|  
|----------------|-----------------------|----------------------------------|----------------------------|  
|创建、修改或删除共享计划|管理共享计划|系统管理员|所有者|  
|选择共享计划|查看共享计划|系统用户|成员|  
|在用户定义的订阅中创建、修改或删除报表特定计划|管理单独的订阅|浏览者、报表生成器、我的报表、内容管理员|访问者，成员|  
|创建、修改或删除所有其他计划操作的报表特定计划|管理报表历史记录，管理所有订阅，管理报表|内容管理员|所有者|  
  
 有关在纯模式下的安全性的详细信息[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，请参阅[预定义角色](../security/role-definitions-predefined-roles.md)，[授予对本机模式报表服务器的权限](../security/granting-permissions-on-a-native-mode-report-server.md)和[任务和权限](../security/tasks-and-permissions.md). 对于 SharePoint 模式，请参阅 [Reporting Services 中的角色和任务与 SharePoint 组和权限的比较](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
  
##  <a name="bkmk_how_scheduling_works"></a> 计划和传递处理的工作方式  
 计划和传递处理器提供以下功能：  
  
-   维护报表服务器数据库中的事件和通知队列。 对于扩展部署，将在部署中的所有报表服务器之间共享该队列。  
  
-   调用报表处理器以执行报表、处理订阅或清除缓存的报表。 所有作为计划事件的结果发生的报表处理都将作为后台进程执行。 SharePoint 模式利用计时器作业来：  
  
-   调用在订阅中指定的传递扩展插件，以便可以传递报表。  
  
 计划和传递操作的其他方面由与计划和传递处理器配合工作的其他组件和服务进行处理。 具体而言，计划和传递处理器在报表服务器服务中运行，并使用 SQL Server 代理作为计时器来生成预定的事件。 下面分步说明了计划操作如何在 Reporting Services 部署中工作：  
  
1.  计划操作在用户创建计划时定义。 计划定义的日期和时间用来触发报表传递的订阅，刷新快照或使缓存过期。  
  
2.  报表服务器将计划信息保存在报表服务器数据库中。  
  
3.  报表服务器在包含所提供计划信息的 SQL Server 代理中创建相应的作业。 这些作业是使用打开的现有报表服务器数据库连接并通过存储过程创建的。  
  
4.  SQL Server 代理按照计划中指定的日期和时间运行作业。 作业创建的事件将添加到由 Reporting Services 维护的队列中。  
  
5.  该事件会导致报表或订阅进程发生。 当在队列中检测到事件时对事件进行处理，并相应地处理或传递报表。  
  
     在处理事件之前，计划和传递处理器会执行身份验证步骤以验证订阅的所有者有权查看该报表。  
  
 Reporting Services 维护一个针对所有计划操作的事件队列。 它定期轮询队列，检查是否有新事件。 默认情况下，每隔 10 秒扫描一次队列。 您可以通过修改更改间隔`PollingInterval`， `IsNotificationService`，和`IsEventService`RSReportServer.config 文件中的配置设置。 SharePoint 模式还将 RSreporserver.config 用于这些设置，并且值应用于所有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。 有关详细信息，请参阅 [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md)。  
  
##  <a name="bkmk_serverdependencies"></a> 服务器依赖关系  
 计划和传递处理器需要启动报表服务器服务和 SQL Server 代理。 计划和传递处理的功能必须启用通过`ScheduleEventsAndReportDeliveryEnabled`属性**Reporting Services 的外围应用配置**中基于策略的管理方面。 SQL Server 代理和报表服务器服务必须都在运行，才能执行计划的操作。  
  
> [!NOTE]  
>  可以使用 **Reporting Services 的外围应用配置器** 方面临时或永久停止计划操作。 虽然可以创建并部署自定义传递扩展插件，但是计划和传递处理器本身不是可扩展的。 该工具管理事件和通知的方式是不可更改的。 关于关闭功能的详细信息，请参阅 **Turn Reporting Services Features On or Off** 中的 [“预定的事件和传递”](../report-server/turn-reporting-services-features-on-or-off.md)一节。  
  
###  <a name="bkmk_stoppingagent"></a> 停止 SQL Server 代理的影响  
 默认情况下，计划的报表处理将使用 SQL Server 代理。 如果停止该服务，除非通过 <xref:ReportService2010.ReportingService2010.FireEvent%2A> 方法以编程的方式添加请求，否则将不会向队列中添加新的处理请求。 重新启动该服务时，将继续进行创建报表处理请求的作业。 对于过去在 SQL Server 代理脱机期间可能已经发生的报表处理作业，报表服务器不会尝试重新创建这些作业。 如果 SQL Server 代理停止一个星期的时间，则该星期的所有计划操作都将丢失。  
  
> [!NOTE]  
>  对于 SQL Server 代理提供给 Reporting Services 的功能，可以使用通过 <xref:ReportService2010.ReportingService2010.FireEvent%2A> 方法向队列中添加计划事件的自定义代码来替代。  
  
###  <a name="bkmk_stoppingservice"></a> 停止报表服务器服务的影响  
 如果停止报表服务器服务，SQL Server 代理会继续向队列中添加报表处理请求。 来自 SQL Server 代理的状态信息将指示作业成功。 但是，由于报表服务器服务已停止，因此实际上不会发生报表处理。 在您重新启动报表服务器服务之前，请求将在队列中一直累积。 重新启动报表服务器服务后，将按顺序处理队列中的所有报表处理请求。  
  
## <a name="see-also"></a>请参阅  
 [创建、 修改和删除报表历史记录中的快照](../report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [订阅和传递&#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [数据驱动订阅](data-driven-subscriptions.md)   
 [缓存报表 (SSRS)](../report-server/caching-reports-ssrs.md)   
 [报表服务器内容管理&#40;SSRS 本机模式&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [缓存共享数据集&#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)  
  
  